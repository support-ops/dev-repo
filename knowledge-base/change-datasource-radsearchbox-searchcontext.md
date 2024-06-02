---
title: Changing Datasource When SearchContext Changes in RadSearchBox
description: Learn how to change the datasource of a RadSearchBox when the search context changes. This article covers the implementation of different data sources for "Landlords," "Tenants," and "Owners."
type: how-to
page_title: How to Change RadSearchBox Datasource When SearchContext Changes
slug: change-datasource-radsearchbox-searchcontext
tags: radsearchbox, asp.net ajax, datasource, searchcontext
res_type: kb
ticketid: 1581043
---

## Environment

| Product | RadSearchBox for ASP.NET AJAX |
| --- | --- |
| Version | Current |

## Description

I want to change the datasource of a [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) when the search context changes. The user can choose between "Landlords," "Tenants," and "Owners," each of which comes from different tables. 

This KB article also answers the following questions:
- How to dynamically change the datasource of RadSearchBox?
- How to handle different search contexts in RadSearchBox?
- How to implement search functionality for multiple entities in RadSearchBox?

## Solution

1. **Create SQL DataSources for Each Entity:**

   Define different SQL data sources for "Tenants," "Landlords," and "Owners":

   ```asp
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

2. **Handle the Search Context Change Event:**

   Use JavaScript to handle the search context change event and trigger an AJAX request:



3. **Change the Datasource in the Code-Behind:**

   Implement the `AjaxRequest` event to change the RadSearchBox's datasource based on the selected search context:

   ```vb
   Protected Sub RadAjaxManager1_OnAjaxRequest(sender As Object, e As AjaxRequestEventArgs)
       If Not IsNothing(RadSearchBox1.DataSource) Then
           Select Case e.Argument
               Case "Tenants"
                   RadSearchBox1.DataSource = SqlDataSourceTenants
                   RadSearchBox1.DataBind()
               Case "Landlords"
                   RadSearchBox1.DataSource = SqlDataSourceLandlords
                   RadSearchBox1.DataBind()
               Case "Owners"
                   RadSearchBox1.DataSource = SqlDataSourceOwners
                   RadSearchBox1.DataBind()
           End Select
       End If
   End Sub
   ```

4. **Handle the Search Event:**

   In the `OnSearch` event of the RadSearchBox, get the ID and EntityName and perform the necessary operations:

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
- [Handling SearchBox Events](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/server-side-programming/events)


