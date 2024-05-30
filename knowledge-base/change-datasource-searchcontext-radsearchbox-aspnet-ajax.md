---
title: Changing Datasource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the datasource of the RadSearchBox in ASP.NET AJAX when the SearchContext changes.
type: how-to
page_title: How to Change RadSearchBox Datasource Based on SearchContext in ASP.NET AJAX
slug: change-datasource-searchcontext-radsearchbox-aspnet-ajax
tags: radsearchbox, asp.net ajax, datasource, searchcontext, ajax request, onsearch
res_type: kb
---

## Environment
- Product: RadSearchBox for ASP.NET AJAX
- Version: Latest

## Description
I want to let a user choose between "Landlords", "Tenants", and "Owners" and search for a name. The data for the search box comes from different tables. I need to set the `DataSourceId` on the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) to one of the specific data sources when the `SearchContext` changes.

This KB article also answers the following questions:
- How to dynamically change the data source of RadSearchBox in ASP.NET AJAX?
- How to handle SearchContext change in RadSearchBox?
- How to use Ajax Request to update RadSearchBox datasource?

## Solution

1. **Add SQL Data Sources in ASPX:**
   Define the SQL data sources in your ASPX page.

    ```html
    <asp:SqlDataSource ID="SqlDataSourceTenants" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id,TenantEntityName as EntityName FROM TenantEntities"></asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceLandlords" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, LandlordEntityName as EntityName FROM LandlordEntities"></asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceOwners" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id,OwnerEntityName As EntityName FROM OwnerEntities"></asp:SqlDataSource>
    ```

2. **Client-Side JavaScript:**
   Add a client-side script to handle the `SearchContext` change event.

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

3. **Server-Side Code in Code-Behind:**
   Add code to handle the AJAX request and update the data source.

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

4. **Angel:**
   Get the selected entity data and perform any necessary actions.

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
- [RadAjaxManager Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/ajaxmanager/overview)
- [RadSearchBox Client-Side API](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/client-side-programming/overview)

