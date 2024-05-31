---
title: Changing DataSource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to dynamically change the data source of the RadSearchBox component when the SearchContext changes, allowing users to search across different tables such as "Landlords", "Tenants", and "Owners".
type: how-to
page_title: Dynamically Change RadSearchBox DataSource Based on SearchContext
slug: changing-datasource-when-searchcontext-changes-radsearchbox-aspnet-ajax
tags: radsearchbox, asp.net ajax, datasource, searchcontext, dynamic
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to change the data source of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) component dynamically when the user selects a different search context. The user should be able to choose between "Landlords", "Tenants", and "Owners", and search for names within these categories. The data for each category comes from different SQL tables.

This KB article also answers the following questions:
- How to change RadSearchBox data source at runtime in ASP.NET AJAX?
- How to handle SearchContext changes in RadSearchBox?
- How to dynamically bind data to RadSearchBox based on user selection?

## Solution

1. **Define SQL Data Sources** for each category in the ASPX page.

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

2. **Handle the Client-Side Event** to send the selected search context to the server via AJAX.

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

3. **Handle the Server-Side AJAX Request** to change the data source based on the selected search context.

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

4. **Handle the Search Event** to process the selected data item.

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

- [RadSearchBox Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview)
