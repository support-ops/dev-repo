---
title: Changing DataSource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the DataSource of RadSearchBox dynamically based on the selected SearchContext.
type: how-to
page_title: Dynamically Changing DataSource in RadSearchBox for ASP.NET AJAX
slug: changing-datasource-searchcontext-radsearchbox
tags: radsearchbox, asp.net ajax, datasource, searchcontext, dynamic
res_type: kb
ticketid: 1581043
---
## Environment
- Product: RadSearchBox for ASP.NET AJAX
- Version: current

## Description
I want to allow users to choose between "Landlords", "Tenants", and "Owners" and search for a name. The data for the search box comes from different tables. When the `SearchContext` changes, I need to dynamically set the `DataSourceId` of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) to one of the predefined data sources.

This KB article also answers the following questions:
- How to change the DataSource of RadSearchBox dynamically?
- How to handle SearchContext changes in RadSearchBox?
- How to bind different data sources to RadSearchBox based on user selection?

## Solution
1. Define the SQL data sources for "Tenants", "Landlords", and "Owners".
    ```html
    <asp:SqlDataSource ID="SqlDataSourceTenants" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, TenantEntityName as EntityName FROM TenantEntities">
    </asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceLandlords" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, LandlordEntityName as EntityName FROM LandlordEntities">
    </asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceOwners" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, OwnerEntityName as EntityName FROM OwnerEntities">
    </asp:SqlDataSource>
    ```

2. Handle the `SearchContext` change event in JavaScript.
    ```javascript
    function OnClientLoad(sender, args) {
        var context = sender.get_searchContext();
        var $ = $telerik.$;
        $(context).on({
            "selectedIndexChanged": function (event) {
                var searchbox = $find("<%= RadSearchBox1.ClientID %>");
                var ajaxManager = $find("<%= RadAjaxManager1.ClientID %>");
                ajaxManager.ajaxRequest(context.get_selectedItem().get_text());
            }
        });
    }
    ```

3. Handle the Ajax request on the server side to set the appropriate data source.
    ```vb
    Protected Sub RadAjaxManager1_OnAjaxRequest(sender As Object, e As AjaxRequestEventArgs)
        Select Case e.Argument
            Case "Tenants"
                RadSearchBox1.DataSourceID = "SqlDataSourceTenants"
            Case "Landlords"
                RadSearchBox1.DataSourceID = "SqlDataSourceLandlords"
            Case "Owners"
                RadSearchBox1.DataSourceID = "SqlDataSourceOwners"
        End Select
        RadSearchBox1.DataBind()
    End Sub
    ```

4. Handle the `OnSearch` event to retrieve the selected entity's details.
    ```vb
    Protected Sub RadSearchBox1_OnSearch(sender As Object, e As SearchBoxEventArgs)
        If e.DataItem IsNot Nothing Then
            Dim dataItem = DirectCast(e.DataItem, Dictionary(Of String, Object))
            Dim thisId As String = dataItem("Id").ToString()
            Dim thisEntityName As String = dataItem("EntityName").ToString()
            ' Lookup in database and redirect to the relevant data view/edit page
        End If
    End Sub
    ```
