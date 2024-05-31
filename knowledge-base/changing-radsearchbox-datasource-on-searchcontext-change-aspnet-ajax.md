---
title: Changing Datasource When SearchContext Changes in RadSearchBox
description: Learn how to change the datasource of RadSearchBox when the SearchContext changes in ASP.NET AJAX.
type: how-to
page_title: Changing RadSearchBox Datasource on SearchContext Change in ASP.NET AJAX
slug: changing-radsearchbox-datasource-on-searchcontext-change-aspnet-ajax
tags: radsearchbox, asp.net ajax, datasource, searchcontext
res_type: kb
ticketid: 1581043
---

## Environment

| Product                     | RadSearchBox for ASP.NET AJAX |
| --------------------------- | ----------------------------- |
| Version                     | Current                       |

## Description

I want to be able to let a user choose "Landlords", "Tenants", "Owners" and search for a name. The data for the search box comes from different tables. I need to set the `DatasourceId` on the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) to one of the above when the SearchContext changes. I have determined how to get the selected search context text via an Ajax Request but cannot work out how to change the datasource at runtime.

This KB article also answers the following questions:
- How to set different datasources for RadSearchBox based on search context?
- How to switch datasource in RadSearchBox using AJAX?
- How to dynamically change RadSearchBox's datasource in ASP.NET AJAX?

## Solution

1. Define your SQL datasources in the ASPX page:

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

2. Handle the client-side event to capture the search context change and make an AJAX request:

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

3. Handle the AJAX request on the server-side to change the datasource of the RadSearchBox:

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

4. Handle the search event to retrieve the selected item details:

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
