---
title: Using AggregateFunctions in RadGridView
description: Learn how to effectively use AggregateFunctions like SumFunction and AverageFunction in RadGridView.
type: how-to
page_title: How to Use AggregateFunctions in RadGridView
slug: using-aggregatefunctions-radgridview
tags: radgridview, aggregatefunctions, sumfunction, averagefunction, wpf
res_type: kb
category: knowledge-base
ticketid: 1576897
---

## Environment

Product: Chart for Progress® Kendo UI®  
Version: 2022.1.412  

## Description

I'm trying to use the [RadGridView](https://docs.telerik.com/devtools/wpf/controls/radgridview/overview) AggregateFunctions. I've tested Count, Min, and Max functions successfully. However, when I try using SumFunction or AverageFunction, nothing is displayed on the column footer (including the previously added Count, Min, Max functions).

This KB article also answers the following questions:
- How to display SumFunction in RadGridView footer?
- Why are aggregate functions not showing in RadGridView?
- How to use AggregateFunctions in RadGridView?

## Solution

To use AggregateFunctions like SumFunction and AverageFunction in RadGridView, follow these steps:

1. Ensure that `ShowColumnFooters` is set to `True` in your RadGridView XAML configuration.
2. Bind your DataTable to the RadGridView correctly.
3. Define the AggregateFunctions in the XAML for the respective columns.

Here is an example of how to configure the RadGridView in XAML:

```xaml
<telerikGrid:RadGridView
    x:Name="radGrid1"
    MultipleSelect="True"
    AutoGenerateColumns="False"
    ShowColumnFooters="True"
    ShowGroupFooters="True">
    
    <telerikGrid:RadGridView.Columns>
        
        <telerikGrid:GridViewDataColumn Header="AccountNo" DataMemberBinding="{Binding AccountNo}">
            <telerikGrid:GridViewDataColumn.AggregateFunctions>
                <telerikData:CountFunction Caption="Count:"/>
            </telerikGrid:GridViewDataColumn.AggregateFunctions>
        </telerikGrid:GridViewDataColumn>
        
        <telerikGrid:GridViewDataColumn Header="InvestmentCost" DataMemberBinding="{Binding InvestmentCost}" DataFormatString="{}{0:c}" TextAlignment="Right">
            <telerikGrid:GridViewDataColumn.AggregateFunctions>
                <telerikData:SumFunction ResultFormatString="{}{0:c}" SourceField="InvestmentCost"/>
                <telerikData:MinFunction ResultFormatString="{}{0:c}" SourceField="InvestmentCost"/>
                <telerikData:MaxFunction ResultFormatString="{}{0:c}" SourceField="InvestmentCost"/>
            </telerikGrid:GridViewDataColumn.AggregateFunctions>
        </telerikGrid:GridViewDataColumn>
        
    </telerikGrid:RadGridView.Columns>
</telerikGrid:RadGridView>
```

Ensure that the DataType for the `InvestmentCost` column in your DataTable is Decimal.

Example of binding DataTable to RadGridView in C#:

```csharp
this.radGrid1.ItemsSource = dtData;
```

If you still face issues, verify that the DataTable is correctly populated and the columns have the correct data types.

## See Also

- [RadGridView Documentation](https://docs.telerik.com/devtools/wpf/controls/radgridview/overview)
- [Aggregate Functions in RadGridView](https://docs.telerik.com/devtools/wpf/controls/radgridview/features/aggregate-functions)
