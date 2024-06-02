---
title: Changing Datasource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to dynamically change the datasource of the RadSearchBox component when the search context changes.
type: how-to
page_title: Dynamically Changing Datasource in RadSearchBox Based on SearchContext
slug: changing-datasource-when-searchcontext-changes-radsearchbox
tags: radsearchbox, asp.net ajax, datasource, searchcontext, dynamically
res_type: kb
ticketid: 1581043
---

## Environment

| Product                   | RadSearchBox for ASP.NET AJAX |
| ------------------------- | ----------------------------- |
| Version                   | Current                       |

## Description

I want to allow a user to select "Landlords", "Tenants", or "Owners" and search for a name. The data for the search box comes from different tables. I need to set the `DataSourceID` on the RadSearchBox to one of the specified data sources when the `SearchContext` changes.

This KB article also answers the following questions:
- How to change the RadSearchBox datasource dynamically?
- How to handle search context change in RadSearchBox?
- How to switch data sources in RadSearchBox based on user selection?

## Solution

1. **Define SQL Data Sources** for each entity type:

    ```asp
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

2. **Add JavaScript to handle SearchContext change**:

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

3. **Handle the Ajax Request on the server side** to change the `DataSource`:



4. **Handle the Search Event** to get the selected entity details:

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

- [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview)
