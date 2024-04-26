---
title: Implementing Multi-Axis Functionality in Kendo UI Chart
description: A guide on how to enable and utilize multi-axis functionality in Kendo UI Chart to display data on multiple axes within the same chart.
type: how-to
page_title: How to Use Multi-Axis in Kendo UI Chart for Enhanced Data Visualization
slug: implementing-multi-axis-kendo-ui-chart
tags: kendo-ui, chart, multi-axis, data-visualization
res_type: kb
related_questions: 
- How can I add multiple axes to a Kendo UI Chart?
- What is multi-axis functionality in Kendo UI Chart?
- Can Kendo UI Chart display data on more than one axis?
- How to configure multiple value axes in a chart?
- How to use secondary axes in Kendo UI Chart?
category: knowledge-base
ticketid: 1584467
---

## Environment
| Product | Version |
| --- | --- |
| Kendo UI for jQuery | 2022.3.913 |

## Description
I want to display data on multiple axes within the same Kendo UI Chart to enhance data visualization and compare different data sets effectively.

## Solution

To implement multi-axis functionality in a Kendo UI Chart, follow these steps:

1. Ensure you're using the Kendo UI version that supports multi-axis charts. The version should be 2022.3.913 or later.
2. Include the Kendo UI Chart component in your project. For detailed instructions, refer to the official [Kendo UI Chart documentation](http://docs.telerik.com/kendo-ui/controls/charts/overview).
3. Configure the chart with multiple value axes. Define each axis in the `valueAxes` array property of the chart configuration. Each object in the array represents a separate axis.
4. Assign the series to the respective axis by setting the `axis` property of the series to the name of the intended value axis. 

Example configuration snippet:

```javascript
$("#chart").kendoChart({
    title: {
        text: "Multi-Axis Chart Example"
    },
    series: [{
        name: "Series 1",
        data: [200, 450, 300, 125],
        axis: "primaryAxis"
    }, {
        name: "Series 2",
        data: [8, 12, 7, 14],
        axis: "secondaryAxis"
    }],
    valueAxes: [{
        name: "primaryAxis",
        min: 0,
        max: 500
    }, {
        name: "secondaryAxis",
        min: 0,
        max: 15,
        color: "#4CAF50"
    }]
});
```

In this example, `primaryAxis` and `secondaryAxis` are used to display different data sets on two separate axes within the same chart.

For more advanced configurations and options, consult the [Kendo UI Chart documentation](http://docs.telerik.com/kendo-ui/controls/charts/overview).

## Notes
- Ensure that the data sets you intend to compare are compatible for visualization on separate axes.
- Customize the appearance and scale of each axis as needed to best represent the data.

## See Also
- [Kendo UI Chart Overview](http://docs.telerik.com/kendo-ui/controls/charts/overview)
- [Kendo UI Chart - Multiple Axes Demo](http://demos.telerik.com/kendo-ui/bar-charts/multiple-axes)
