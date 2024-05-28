---
title: Displaying RadGridView Aggregate Functions
description: Steps to display RadGridView Aggregate Functions like SumFunction and AverageFunction in WPF.
type: how-to
page_title: How to Display Aggregate Functions in RadGridView
slug: displaying-radgridview-aggregate-functions
tags: radgridview, aggregatefunctions, sumfunction, averagefunction, wpf, c#
res_type: kb
category: knowledge-base
ticketid: 1576897
---

## Environment

| Product | Progress® Kendo UI® Chart 2022.1.412 |
| ------- | ------------------------------------ |

## Description

I am trying to use RadGridView AggregateFunctions. While Count, Min, and Max functions display correctly, SumFunction and AverageFunction do not show any values in the column footer. I am binding a DataTable to the grid in C# and defining the columns in XAML.

This KB article also answers the following questions:
- How to display SumFunction in RadGridView?
- Why is AverageFunction not showing in RadGridView footer?
- How to bind DataTable to RadGridView with AggregateFunctions?

## Solution

1. Ensure that the DataType for the column you are aggregating, such as `InvestmentCost`, is correctly set in the DataTable.

2. Define the RadGridView in XAML with the necessary AggregateFunctions:

    ```xml
    <telerikGrid:RadGridView
        x:Name="radGrid1"
        MultipleSelect="True"
        AutoGenerateColumns="False"
        ShowColumnFooters="True"
        ShowGroupFooters="True">
    
        <telerikGrid:RadGridView.Columns>
            <telerikGrid:GridViewDataColumn Header="AccountNo" DataMemberBinding="{Binding AccountNo}">
                <telerikGrid:GridViewDataColumn.AggregateFunctions>
                    <telerikData:CountFunction Caption="Count:" />
                </telerikGrid:GridViewDataColumn.AggregateFunctions>
            </telerikGrid:GridViewDataColumn>
    
            <telerikGrid:GridViewDataColumn Header="InvestmentCost" DataMemberBinding="{Binding InvestmentCost}" DataFormatString="{}{0:c}" TextAlignment="Right">
                <telerikGrid:GridViewDataColumn.AggregateFunctions>
                    <telerikData:SumFunction ResultFormatString="{}{0:c}" SourceField="InvestmentCost" />
                    <telerikData:MinFunction ResultFormatString="{}{0:c}" SourceField="InvestmentCost" />
                    <telerikData:MaxFunction ResultFormatString="{}{0:c}" SourceField="InvestmentCost" />
                </telerikGrid:GridViewDataColumn.AggregateFunctions>
            </telerikGrid:GridViewDataColumn>
        </telerikGrid:RadGridView.Columns>
    </telerikGrid:RadGridView>
    ```
