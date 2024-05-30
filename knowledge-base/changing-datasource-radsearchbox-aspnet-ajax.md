---
title: Changing Datasource When SearchContext Changes in RadSearchBox for ASP.NET AJAX
description: Learn how to change the datasource of RadSearchBox for ASP.NET AJAX when the SearchContext changes, allowing users to search different tables dynamically.
type: how-to
page_title: Changing Datasource Dynamically in RadSearchBox for ASP.NET AJAX
slug: changing-datasource-radsearchbox-aspnet-ajax
tags: radsearchbox, asp.net ajax, datasource, searchcontext, onajaxrequest, onsearch
res_type: kb

## Environment
- Product: RadSearchBox for ASP.NET AJAX
- Version: 2023

## Description

I want to change the datasource of the [RadSearchBox](https://docs.telerik.com/devtools/aspnet-ajax/controls/searchbox/overview) based on the selected SearchContext. The data for the search box should come from different tables depending on whether the user selects "Landlords", "Tenants", or "Owners". I have implemented the client-side logic to capture the SearchContext change but need help with changing the datasource dynamically at runtime.

This KB article also answers the following questions:
- How to dynamically change the datasource of RadSearchBox based on SearchContext?
- How to handle the SearchContext change event in RadSearchBox?
- How to bind a new datasource to RadSearchBox at runtime?

## Solution

1. **Define the SQL DataSources in the ASPX file:**

    ```aspx
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

2. **Implement the client-side logic to detect SearchContext changes:**

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

3. **Handle the AjaxRequest event in the code-behind to change the datasource:**

    ```vb.net
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

4. **Handle the OnSearch event to get the selected entity details:**

    ```vb.net
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
- [RadAjaxManager Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/ajaxmanager/overview)

