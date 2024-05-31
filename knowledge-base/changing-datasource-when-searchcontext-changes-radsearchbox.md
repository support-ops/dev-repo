---
title: Changing DataSource When SearchContext Changes in RadSearchBox
description: Learn how to dynamically change the DataSource of RadSearchBox based on the SearchContext selection in ASP.NET AJAX.
type: how-to
page_title: Dynamically Change RadSearchBox DataSource Based on SearchContext
slug: changing-datasource-when-searchcontext-changes-radsearchbox
tags: radsearchbox, asp.net ajax, datasource, searchcontext, telerik
res_type: kb
ticketid: 1581043
---

## Environment

| Product                    | RadSearchBox for ASP.NET AJAX |
| -------------------------- | ----------------------------- |
| Version                    | Current                       |

## Description

I want to let a user choose between "Landlords", "Tenants", "Owners" and search for a name. The data for the search box comes from different tables. I need to set the `DataSourceID` on the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) based on the selected SearchContext.

This KB article also answers the following questions:
- How to switch RadSearchBox DataSource dynamically?
- How to bind RadSearchBox to different SqlDataSources?
- How to handle SearchContext change in RadSearchBox?

## Solution

1. **Define the SqlDataSources in your ASPX file:**

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

2. **Handle the `selectedIndexChanged` event in JavaScript to trigger an AJAX request:**

    ```javascript
    function OnClientLoad(sender, args) {
        var context = sender.get_searchContext();
        var $ = $telerik.$;
        $(context).on({
            "selectedIndexChanged": function (event) {
                var ajaxManager = $find("<%=RadAjaxManager1.ClientID%>");
                ajaxManager.ajaxRequest(context.get_selectedItem().get_text());
            }
        });
    }
    ```

3. **Handle the `AjaxRequest` event on the server-side to change the DataSource:**

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

4. **In the `OnSearch` event, handle the search results:**

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
