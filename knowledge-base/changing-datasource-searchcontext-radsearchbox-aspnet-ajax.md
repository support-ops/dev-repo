---
title: Changing DataSource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the DataSource of RadSearchBox dynamically based on the selected SearchContext in ASP.NET AJAX.
type: how-to
page_title: Dynamically Change DataSource in RadSearchBox for ASP.NET AJAX Based on SearchContext
slug: changing-datasource-searchcontext-radsearchbox-aspnet-ajax
tags: radsearchbox, aspnet-ajax, changing-datasource, searchcontext
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to let a user choose "Landlords", "Tenants", "Owners" and search for a name. The data for the search box comes from different tables. I need to change the `DataSourceId` of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) when the SearchContext changes.

This KB article also answers the following questions:
- How to switch the RadSearchBox DataSource based on a user's selection?
- How to dynamically update RadSearchBox DataSource in ASP.NET AJAX?
- How to handle multiple data sources in RadSearchBox?

## Solution

1. Define the necessary `SqlDataSource` controls in your ASPX file:


2. Add the `RadSearchBox` and set up the `AjaxManager` to handle the AJAX requests:

```html
<telerik:RadSearchBox ID="RadSearchBox1" runat="server" OnSearch="RadSearchBox1_OnSearch"></telerik:RadSearchBox>
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server" OnAjaxRequest="RadAjaxManager1_OnAjaxRequest">
</telerik:RadAjaxManager>
```

3. Implement the client-side logic to handle the SearchContext change:

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

4. Handle the AJAX request on the server-side to change the `DataSource` of the `RadSearchBox`:

```vb
Protected Sub RadAjaxManager1_OnAjaxRequest(sender As Object, e As AjaxRequestEventArgs)
    If Not IsNothing(RadSearchBox1.DataSource) Then
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

5. Handle the `OnSearch` event to process the selected item from the `RadSearchBox`:

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

## See Also

- [RadSearchBox Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview)
- [RadAjaxManager Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/ajaxmanager/overview)
