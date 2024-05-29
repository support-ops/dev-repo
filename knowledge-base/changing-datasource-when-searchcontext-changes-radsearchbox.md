---
title: Changing Datasource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the datasource of RadSearchBox for ASP.NET AJAX dynamically when the search context changes.
type: how-to
page_title: Dynamically Change Datasource in RadSearchBox Based on SearchContext
slug: changing-datasource-when-searchcontext-changes-radsearchbox
tags: radsearchbox, asp.net, ajax, datasource, searchcontext, dynamic
res_type: kb
---

## Environment
| Product | RadSearchBox for ASP.NET AJAX |

## Description
I want to let a user choose between "Landlords", "Tenants", "Owners" and search for a name. The data for the search box comes from different tables. I need to change the `DataSourceID` of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) when the `SearchContext` changes.

This KB article also answers the following questions:
- How to switch DataSource of RadSearchBox dynamically?
- How to handle SearchContext change event in RadSearchBox?
- How to bind different tables to RadSearchBox based on user selection?

## Solution
Follow these steps to change the `DataSourceID` of RadSearchBox dynamically based on the search context:

1. **Define SQL Data Sources:**
    ```asp
    <asp:SqlDataSource ID="SqlDataSourceTenants" runat="server"
                       ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
                       SelectCommand="SELECT Id, TenantEntityName as EntityName FROM TenantEntities"></asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceLandlords" runat="server"
                       ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
                       SelectCommand="SELECT Id, LandlordEntityName as EntityName FROM LandlordEntities"></asp:SqlDataSource>
    <asp:SqlDataSource ID="SqlDataSourceOwners" runat="server"
                       ConnectionString="<%$ ConnectionStrings:ProjectConnectionString %>"
                       SelectCommand="SELECT Id, OwnerEntityName as EntityName FROM OwnerEntities"></asp:SqlDataSource>
    ```

2. **Set up the RadSearchBox and RadAjaxManager:**
    ```asp
    <telerik:RadSearchBox ID="RadSearchBox1" runat="server" OnSearch="RadSearchBox1_OnSearch" />
    <telerik:RadAjaxManager ID="RadAjaxManager1" runat="server" OnAjaxRequest="RadAjaxManager1_OnAjaxRequest"></telerik:RadAjaxManager>
    ```

3. **JavaScript to Handle SearchContext Change:**
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

4. **Code-Behind to Handle Ajax Request and Change DataSource:**
    ```vb
    Protected Sub RadAjaxManager1_OnAjaxRequest(sender As Object, e As AjaxRequestEventArgs)
        If Not IsNothing(RadSearchBox1.DataSource) Then
            Select Case e.Argument
                Case "Tenants"
                    RadSearchBox1.DataSourceID = "SqlDataSourceTenants"
                Case "Landlords"
                    RadSearchBox1.DataSourceID = "SqlDataSourceLandlords"
                Case "Owners"
                    RadSearchBox1.DataSourceID = "SqlDataSourceOwners"
            End Select
            RadSearchBox1.DataBind()
        End If
    End Sub
    ```

5. **Handle the OnSearch Event:**
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
