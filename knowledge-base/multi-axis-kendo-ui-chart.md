---
title: Configuring Multi Axis Functionality in Kendo UI Chart
description: Learn how to enable and use the multi axis feature in Kendo UI Chart to display multiple axes in your chart.
type: how-to
page_title: How to Enable Multi Axis Functionality in Kendo UI Charts
slug: multi-axis-kendo-ui-chart
tags: kendo ui, chart, multi axis, configuration
res_type: kb
related_questions:
- How do I add multiple axes to a Kendo UI Chart?
- Can Kendo UI Chart display more than one axis?
- What is the process for configuring a Kendo UI Chart with multiple axes?
- How to set up a Kendo UI Chart with multi axis functionality?
- Is multi axis functionality available in Kendo UI Chart?
ticketid: 1584467
---

## Environment

| Property | Value                          |
|----------|--------------------------------|
| Product  | Kendo UI Chart for jQuery 2022.3.913 |

## Description

I am trying to display a chart with multiple axes using the Kendo UI Chart component. I need to know how to enable and configure the multi axis functionality.

## Solution

To enable and use the multi axis functionality in Kendo UI Chart, follow these steps:

1. Ensure you are using Kendo UI version 2022.3.913 or later, as this functionality is available starting from this version.
2. Visit the official Kendo UI Chart multi axis demo page for an example and code snippets: [Kendo UI Chart Multi Axis Demo](http://demos.telerik.com/kendo-ui/bar-charts/multiple-axes).
3. In your chart configuration, define multiple value axes by adding them to the `valueAxes` array in the chart configuration object. Each axis can be customized individually, including its title, minimum and maximum values, and position.
4. Assign each series to a specific axis by setting the `axis` property of the series to the name of the desired value axis.

Here is an example configuration snippet demonstrating how to set up a chart with multiple axes:

```javascript
$("#chart").kendoChart({
    title: {
        text: "Multi Axis Chart Example"
    },
    series: [{
        name: "Series 1",
        data: [200, 450, 300, 125],
        axis: "primaryAxis"
    }, {
        name: "Series 2",
        data: [20, 25, 30, 35],
        axis: "secondaryAxis"
    }],
    valueAxes: [{
        name: "primaryAxis",
        title: { text: "Primary Axis" }
    }, {
        name: "secondaryAxis",
        title: { text: "Secondary Axis" },
        color: "#4CAF50"
    }]
});
```

This configuration creates a Kendo UI Chart with two value axes named "primaryAxis" and "secondaryAxis", each associated with a different data series.

## Notes

- When configuring multiple axes, ensure that each series' `axis` property matches the name of the intended value axis.
- Customize each axis as needed to best represent your data.

## See Also

- [Kendo UI Chart Documentation](https://docs.telerik.com/kendo-ui/controls/charts/chart/overview)
- [Kendo UI Chart Multi Axis Demo](http://demos.telerik.com/kendo-ui/bar-charts/multiple-axes)
