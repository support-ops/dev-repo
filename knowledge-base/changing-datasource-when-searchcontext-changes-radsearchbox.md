---
title: Changing DataSource When SearchContext Changes in RadSearchBox
description: Learn how to change the DataSource of RadSearchBox based on selected SearchContext in ASP.NET AJAX.
type: how-to
page_title: Dynamic DataSource Switching in RadSearchBox for ASP.NET AJAX
slug: changing-datasource-when-searchcontext-changes-radsearchbox
tags: radsearchbox, asp.net ajax, datasource, searchcontext
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to change the DataSource of RadSearchBox when the SearchContext changes. The data for the search box comes from different tables for "Landlords," "Tenants," and "Owners." The goal is to set the DataSourceId on the RadSearchBox to one of the predefined SQL data sources when the SearchContext changes. I can get the selected SearchContext text via an Ajax Request. This KB article also answers the following questions:

- How to dynamically change the DataSource of RadSearchBox in ASP.NET AJAX?
- How to switch the data source based on SearchContext in RadSearchBox?
- How to bind RadSearchBox to different SQL data sources at runtime?

## Solution

1. Define the SQL data sources in your ASPX page:

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

2. Use JavaScript to handle the SearchContext change event and send an Ajax request:

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

3. Handle the Ajax request in the code-behind to change the DataSource of RadSearchBox:

    ```vb
    Protected Sub RadAjaxManager1_OnAjaxRequest(sender As Object, e As AjaxRequestEventArgs)
        Select Case e.Argument
            Case "Tenants"
                RadSearchBox1.DataSource = SqlDataSourceTenants
            Case "Landlords"
                RadSearchBox1.DataSource = SqlDataSourceLandlords
            Case "Owners"
                RadSearchBox1.DataSource = SqlDataSourceOwners
        End Select
        RadSearchBox1.DataBind()
    End Sub
    ```

4. Handle the OnSearch event to get the entity type and ID:

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

By following these steps, you can dynamically change the DataSource of RadSearchBox based on the selected SearchContext.

## See Also

- [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview)
- [RadAjaxManager](https://docs.telerik.com/devtools/aspnet-ajax/controls/ajaxmanager/overview)
