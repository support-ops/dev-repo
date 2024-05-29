---
title: Changing Datasource When SearchContext Changes in RadSearchBox
description: Learn how to change the datasource of RadSearchBox dynamically based on the selected SearchContext in ASP.NET AJAX.
type: how-to
page_title: Dynamically Change RadSearchBox Datasource Based on SearchContext
slug: changing-radsearchbox-datasource-searchcontext
tags: radsearchbox, asp.net ajax, datasource, searchcontext, sqldatasource, radajaxmanager
res_type: kb

## Environment
- Product: RadSearchBox for ASP.NET AJAX

## Description

I want to allow a user to choose between "Landlords", "Tenants", and "Owners" and search for a name. The data for the search box comes from different tables. I need to dynamically set the `DatasourceId` on the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) based on the selected `SearchContext`.

This KB article also answers the following questions:
- How can I switch the datasource of RadSearchBox based on user selection?
- What is the method to update RadSearchBox datasource dynamically in ASP.NET AJAX?
- How to handle different search contexts in RadSearchBox with multiple SQL data sources?

## Solution

1. Define the SQL data sources for each entity in your ASPX file.

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
        SelectCommand="SELECT Id, OwnerEntityName as EntityName FROM OwnerEntities">
    </asp:SqlDataSource>
    ```

2. Use JavaScript to handle the `SearchContext` change event.

    ```javascript
    function OnClientLoad(sender, args) {
        var context = sender.get_searchContext();
        var $ = $telerik.$;
        $(context).on({
            "selectedIndexChanged": function (event) {
                var searchbox = $find("<%=RadSearchBox1.ClientID%>");
                var ajaxManager = $find("<%=RadAjaxManager1.ClientID%>");
                ajaxManager.ajaxRequest(context.get_selectedItem().get_text());
            }
        });
    }
    ```

3. Handle the AJAX request on the server-side to change the `DataSource` of `RadSearchBox`.

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

4. In the `OnSearch` event, get the selected entity type and ID.

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
