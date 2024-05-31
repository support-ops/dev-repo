---
title: Changing Datasource When SearchContext Changes in RadSearchBox
description: Learn how to dynamically change the datasource of a RadSearchBox when the SearchContext changes in ASP.NET AJAX.
type: how-to
page_title: Dynamically Changing RadSearchBox Datasource Based on SearchContext in ASP.NET AJAX
slug: changing-datasource-searchcontext-radsearchbox
tags: radsearchbox, asp-net-ajax, changing-datasource, searchcontext
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to let a user choose "Landlords", "Tenants", or "Owners" and search for a name. The data for the search box comes from different tables. I need to set the `DataSourceId` on the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) to one of the specified SQL data sources when the `SearchContext` changes.

This KB article also answers the following questions:
- How to switch RadSearchBox datasource based on user selection?
- How to bind RadSearchBox to different SQL data sources dynamically?
- How to handle SearchContext change event in RadSearchBox?

## Solution

1. Define the SQL data sources in the ASPX page:

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
    SelectCommand="SELECT Id, OwnerEntityName as EntityName FROM OwnerEntities">
</asp:SqlDataSource>
```

2. Handle the `SearchContext` change event with JavaScript:

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

3. Implement the `OnAjaxRequest` event handler in the code-behind:

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

4. Handle the `OnSearch` event to fetch the entity details and perform necessary actions:

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
- [Using RadAjaxManager](https://docs.telerik.com/devtools/aspnet-ajax/controls/ajaxmanager/overview)

