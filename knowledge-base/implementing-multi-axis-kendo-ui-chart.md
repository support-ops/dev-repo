---
title: Implementing Multi-Axis Functionality in Kendo UI Chart
description: Learn how to enable and use the multi-axis feature in Kendo UI Chart to enhance your data visualization.
type: how-to
page_title: How to Use Multiple Axes in Kendo UI Chart for Advanced Data Visualization
slug: implementing-multi-axis-kendo-ui-chart
tags: kendo-ui, chart, multi-axis, data-visualization
res_type: kb
related_questions: 
- How can I add multiple axes to a Kendo UI Chart?
- What is multi-axis functionality in Kendo UI Chart?
- Can Kendo UI Chart display data on different scales?
- How to visualize complex data using Kendo UI Chart?
- What are the steps to enable multi-axis in Kendo UI Chart?
category: knowledge-base
ticketid: 1584467
---

## Environment

| Property | Value |
|---|---|
| Product Name | Application for Progress® Kendo UI® |
| Version | 2022.3.913 |

## Description

I need to display data that varies widely in scale on a single Kendo UI Chart. How can I implement multi-axis functionality to achieve this?

## Solution

To enable and use the multi-axis feature in Kendo UI Chart, follow these steps:

1. Ensure you are using Kendo UI version 2022.3.913 or later.
2. Include the Kendo UI Chart component in your application. Refer to the [official documentation](http://demos.telerik.com/kendo-ui/bar-charts/multiple-axes) for detailed guidance on initializing the Chart.
3. Configure multiple value axes in the Chart's configuration. Each axis should be defined within the `valueAxis` array property.
4. Assign series to the respective axes by setting the `axis` property in each series configuration to the name of the intended value axis.
5. Customize axes as needed, including labels, line colors, and positions, to improve readability and presentation of the data.

By following these steps, you can effectively visualize data that requires different scales on a single chart, enhancing your application's data presentation capabilities.

## Notes

- The multi-axis functionality allows for more versatile data visualization, enabling the comparison of datasets that would be difficult to interpret on a single scale.
- For additional customization options and advanced features, refer to the Kendo UI Chart documentation.

## See Also

- [Kendo UI Chart Documentation](https://docs.telerik.com/kendo-ui/controls/charts/chart/overview)
- [Kendo UI Chart Multiple Axes Demo](http://demos.telerik.com/kendo-ui/bar-charts/multiple-axes)
- [Configuring Kendo UI Chart Axes](https://docs.telerik.com/kendo-ui/controls/charts/chart/axes/overview)
