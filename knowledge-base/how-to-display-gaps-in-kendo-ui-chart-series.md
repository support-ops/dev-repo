---
title: Displaying Gaps in Kendo UI Chart Series
description: Learn how to show gaps in Kendo UI Chart series for specific values, effectively displaying blank spaces instead of data points.
type: how-to
page_title: How to Show Gaps in Chart Series Using Kendo UI Chart
slug: how-to-display-gaps-in-kendo-ui-chart-series
tags: kendo-ui, chart, series, gaps, display, data-visualization
res_type: kb
related_questions:
- How do I create gaps in a chart series with Kendo UI?
- Can I display empty spaces for certain values in Kendo UI Chart?
- What values should I use to show no data in Kendo UI Chart series?
- How to skip data points in Kendo UI Chart?
- Is it possible to have blank spaces in Kendo UI Chart for specific values?
ticketid: 1584467
---

## Environment

| Product             | Version  |
|---------------------|----------|
| Progress® Kendo UI® | 2022.3.913 |

## Description

I am using Telerik Silverlight charts in my application. According to our requirements, we have some values in our data for which we want to show nothing in the chart. Initially, we thought of putting 0 value for these values, but even at 0, the chart displays something. We aim to achieve a blank space kind of effect in the chart for specific values.

## Solution

To display gaps in the Kendo UI Chart series for specific values, you can utilize the `missingValues` property of the chart series. This property allows you to control how the chart displays or skips null or undefined values, effectively creating gaps in the series.

Here are the steps to achieve this:

1. Define your data source, including `null` or `undefined` values for the points where you want to display gaps.

2. Set up your Kendo UI Chart and configure the series options. Use the `missingValues` property and set it to `"gap"` for the series you want to display gaps.

Example configuration:

```javascript
$("#chart").kendoChart({
  series: [{
    type: "line",
    data: [1, 2, null, 4, 5], // Assuming 'null' is where you want the gap
    missingValues: "gap" // This will create a gap in the series
  }]
});
```

In this example, a line series is displayed with a gap where the data value is `null`. You can adjust the data and series type according to your specific requirements.

For more detailed information and options for configuring your chart, refer to the official Kendo UI Chart documentation: [Kendo UI Chart](https://docs.telerik.com/kendo-ui/controls/charts/overview).

## Notes

- The `missingValues` property offers different options for handling missing data points, such as `"gap"`, `"interpolate"`, and `"zero"`. Choosing `"gap"` specifically instructs the chart to display a gap for null or undefined values in the series.
- This solution applies to various series types in the Kendo UI Chart, including line, area, and other continuous series types.

## See Also

- [Kendo UI Chart Overview](https://docs.telerik.com/kendo-ui/controls/charts/overview)
- [Kendo UI Chart Series Types](https://docs.telerik.com/kendo-ui/controls/charts/series-types/overview)
- [Kendo UI Chart Data Binding](https://docs.telerik.com/kendo-ui/controls/charts/data-binding/overview)
