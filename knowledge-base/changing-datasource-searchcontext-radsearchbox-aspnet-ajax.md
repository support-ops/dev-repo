---
title: Changing Datasource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the datasource of RadSearchBox based on the selected SearchContext in ASP.NET AJAX.
type: how-to
page_title: How to Change RadSearchBox Datasource on SearchContext Change in ASP.NET AJAX
slug: changing-datasource-searchcontext-radsearchbox-aspnet-ajax
tags: radsearchbox, asp.net ajax, datasource, searchcontext, dynamic, change
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to allow a user to choose between "Landlords", "Tenants", or "Owners" and search for a name. The data for the search box comes from different tables. The goal is to change the `DataSourceId` of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) based on the selected `SearchContext`. 

This KB article also answers the following questions:
- How to dynamically change the datasource of RadSearchBox?
- How to bind RadSearchBox to different SqlDataSources at runtime?
- How to handle SearchContext changes in RadSearchBox?

## Solution

1. **Define Your SqlDataSources:**

    ```html
    <asp:SqlDataSource ID="SqlDataSourceTenants" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, TenantEntityName as EntityName FROM TenantEntities"></asp:SqlDataSource>
    
    <asp:SqlDataSource ID="SqlDataSourceLandlords" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, LandlordEntityName as EntityName FROM LandlordEntities"></asp:SqlDataSource>
    
    <asp:SqlDataSource ID="SqlDataSourceOwners" runat="server"
        ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
        SelectCommand="SELECT Id, OwnerEntityName As EntityName FROM OwnerEntities"></asp:SqlDataSource>
    ```

2. **Handle SearchContext Change on Client Side:**

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

3. **Change Datasource on Server Side:**

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

4. **Handle the Search Event:**

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
