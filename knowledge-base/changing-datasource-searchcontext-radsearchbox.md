---
title: Changing Datasource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the datasource of RadSearchBox when the SearchContext changes to allow users to search different tables dynamically.
type: how-to
page_title: Dynamically Change RadSearchBox Datasource Based on SearchContext
slug: changing-datasource-searchcontext-radsearchbox
tags: radsearchbox, asp.net ajax, datasource, searchcontext, dynamic
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to let a user choose among "Landlords", "Tenants", and "Owners" and search for a name. The data for the search box comes from different tables. I need to change the `DataSourceId` of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) when the `SearchContext` changes.

This KB article also answers the following questions:
- How to change RadSearchBox datasource dynamically?
- How to use different datasources based on user selection in RadSearchBox?
- How to bind RadSearchBox to different data tables?

## Solution

1. **Define Multiple DataSources:**

    ```asp
    <asp:SqlDataSource ID="SqlDataSourceTenants" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id,TenantEntityName as EntityName FROM TenantEntities">
    </asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceLandlords" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, LandlordEntityName as EntityName FROM LandlordEntities">
    </asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceOwners" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id,OwnerEntityName As EntityName FROM OwnerEntities">
    </asp:SqlDataSource>
    ```

2. **Handle Client-Side Context Change:**

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

3. **Handle Server-Side Ajax Request:**

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

4. **Handle Search Event:**

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

This solution allows dynamically changing the data source of a RadSearchBox component based on the selected search context, ensuring that users can search across different tables seamlessly.
