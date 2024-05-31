---
title: Using columns.sortable.initialDirection in UI for ASP.NET MVC Grid
description: Learn how to use the columns.sortable.initialDirection property in a Kendo UI Grid for ASP.NET MVC.
type: how-to
page_title: Configuring Initial Sort Direction in Kendo UI Grid for ASP.NET MVC
slug: using-columns-sortable-initial-direction-in-aspnet-mvc-grid
tags: kendo, aspnet, mvc, grid, columns, sortable, initialDirection
res_type: kb
category: knowledge-base
ticketid: 1628004
---

## Environment

| Product | Progress® Telerik® UI for ASP.NET MVC |
| Version | 2023 |

## Description

I want to configure the initial sort direction of a column in a [Kendo UI Grid for ASP.NET MVC](https://docs.telerik.com/aspnet-mvc/html-helpers/data-management/grid/overview) using the `columns.sortable.initialDirection` property. The goal is to set the default sorting direction for a column to either "asc" (ascending) or "desc" (descending).

This KB article also answers the following questions:
- How to set default sorting in Kendo MVC Grid?
- How to use initialDirection property in Kendo UI Grid for ASP.NET MVC?
- How to configure initial sort direction in Kendo Grid for MVC?

## Solution

1. Open your ASP.NET MVC project and locate the view where the Kendo UI Grid is defined.

2. Add the `columns.sortable` configuration to the desired column definition in the Grid. Set the `initialDirection` property to either "asc" or "desc".

Example:
```csharp
@(Html.Kendo().Grid<Kendo.Mvc.Examples.Models.ProductViewModel>()
    .Name("grid")
    .Columns(columns =>
    {
        columns.Bound(p => p.ProductName).Sortable(sortable => sortable.InitialDirection("asc"));
        columns.Bound(p => p.UnitPrice).Sortable(sortable => sortable.InitialDirection("desc"));
        // Add other columns as needed
    })
    .DataSource(dataSource => dataSource
        .Ajax()
        .Read(read => read.Action("Products_Read", "Grid"))
    )
    .Pageable()
    .Sortable()
    .Filterable()
)
```

3. Ensure that the `Kendo.Mvc` assembly version matches the one referenced in your project (e.g., Version=2017.1.223.545).

4. Run your project. The Grid will now have the specified columns sorted in the initial direction you set.

## See Also

- [Kendo UI Grid for ASP.NET MVC Documentation](https://docs.telerik.com/aspnet-mvc/html-helpers/data-management/grid/overview)
- [Kendo UI Grid JavaScript API - columns.sortable.initialDirection](http://docs.telerik.com/kendo-ui/api/javascript/ui/grid#configuration-columns.sortable.initialDirection)


