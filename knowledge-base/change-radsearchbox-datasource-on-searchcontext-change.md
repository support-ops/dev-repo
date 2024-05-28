---
title: Changing DataSource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to dynamically change the DataSource of RadSearchBox based on the selected SearchContext.
type: how-to
page_title: Dynamically Change RadSearchBox DataSource Based on SearchContext
slug: change-radsearchbox-datasource-on-searchcontext-change
tags: radsearchbox, asp.net-ajax, datasource, searchcontext, sqldatasource, ajaxrequest
res_type: kb

## Environment
- Product: RadSearchBox for ASP.NET AJAX
- Version: Current

## Description
I want to allow users to choose "Landlords", "Tenants", or "Owners" and search for a name. The data for the search box comes from different tables. I need to set the `DataSourceID` on the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) to one of the defined `SqlDataSource` controls when the `SearchContext` changes. The goal is to dynamically change the data source based on the user's selection in the search context dropdown.

This KB article also answers the following questions:
- How to change RadSearchBox DataSource dynamically?
- How to use different data sources in RadSearchBox based on selection?
- How to handle SearchContext change in RadSearchBox?

## Solution
Perform the following steps to change the RadSearchBox DataSource dynamically when the SearchContext changes:

1. Define the `SqlDataSource` controls in your ASP.NET page:

    ```aspx
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
        SelectCommand="SELECT Id, OwnerEntityName As EntityName FROM OwnerEntities">
    </asp:SqlDataSource>
    ```

2. Handle the `SearchContext` change event using JavaScript:

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

3. Implement the server-side logic to set the correct `DataSource`:

    ```vb
    Protected Sub RadAjaxManager1_OnAjaxRequest(sender As Object, e As AjaxRequestEventArgs)
        If RadSearchBox1.DataSource IsNot Nothing Then
            Select Case e.Argument
                Case "Tenants"
                    RadSearchBox1.DataSource = SqlDataSourceTenants
                Case "Landlords"
                    RadSearchBox1.DataSource = SqlDataSourceLandlords
                Case "Owners"
                    RadSearchBox1.DataSource = SqlDataSourceOwners
            End Select
            RadSearchBox1.DataBind()
        End If
    End Sub
    ```

4. Handle the `OnSearch` event to get the selected entity's details:

    ```vb
    Protected Sub RadSearchBox1_OnSearch(sender As Object, e As SearchBoxEventArgs)
        If e.DataItem IsNot Nothing Then
            Dim dataItem = DirectCast(e.DataItem, Dictionary(Of String, Object))
            Dim thisId As String = dataItem("Id").ToString()
            Dim thisEntityName As String = dataItem("EntityName").ToString()
            ' Lookup in database and redirect to the relevant data view / edit page
        End If
    End Sub
    ```

## See Also
- [RadSearchBox Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview)
- [RadSearchBox Data Binding](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/data-binding)
- [RadAjaxManager Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/ajaxmanager/overview)
