---
title: Displaying Blank Spaces in Telerik Silverlight Charts for Specific Data Values
description: Learn how to show blank spaces in Telerik Silverlight Charts for certain data values instead of plotting zero or any value.
type: how-to
page_title: How to Create Blank Spaces in Charts for Specific Values with Telerik Silverlight Charts
slug: how-to-display-blank-spaces-in-telerik-silverlight-charts
tags: kendo ui, chart, silverlight, data visualization, items.clear, multi axis
res_type: kb
related_questions: 
- How can I display gaps in my Telerik Silverlight Chart data?
- Is it possible to skip plotting values in Telerik Silverlight Charts?
- Can I show blank spaces for zero values in Telerik Silverlight Chart?
- How to configure Telerik Silverlight Chart to not display specific data points?
- What method can clear items in a Telerik Silverlight Chart?
ticketid: 1584467
---

## Environment

| Product | Version  |
|---|---|
| Application for Progress® Kendo UI® | 2022.3.913 |

## Description

In a Telerik Silverlight Chart, I need to display blank spaces for specific data values instead of plotting zero or any other value. This requirement aims to visually indicate the absence of data for certain points in the chart.

## Solution

To achieve blank spaces in a Telerik Silverlight Chart for specific data values, follow these steps:

1. **Identify the Data Points for Blank Spaces**: Determine which data points should display as blank spaces in the chart.
2. **Use `null` Values for Data Points**: For the data points that you want to display as blank spaces, assign `null` values instead of zeros or any other numeric value. The Telerik Silverlight Chart treats `null` values as gaps in the data series, effectively creating the desired blank spaces.
3. **Adjust Chart Configuration if Necessary**: Depending on your specific chart configuration and requirements, you may need to adjust additional chart settings to ensure that the blank spaces are displayed as intended. This might involve configuring axes, labels, or other chart elements.

For more information on configuring and working with Telerik Silverlight Charts, refer to the official documentation here: [Kendo UI Chart](http://demos.telerik.com/kendo-ui/bar-charts/multiple-axes).

## Notes

- The approach of using `null` values for indicating blank spaces is applicable to various types of charts within the Telerik Silverlight Chart suite. However, the exact impact on visualization may vary depending on the chart type and settings.
- Be mindful of how blank spaces (gaps) in your data might affect the interpretation of the chart by the end users. It may be helpful to include a legend or note explaining why certain data points are missing.

## See Also

- [Telerik Kendo UI Chart Documentation](https://docs.telerik.com/kendo-ui/controls/charts/overview)
- [Configuring Axes in Kendo UI Chart](https://docs.telerik.com/kendo-ui/controls/charts/how-to/various/configure-axes)
- [Handling Null Values in Kendo UI Chart Data](https://docs.telerik.com/kendo-ui/knowledge-base/chart-handle-null-values)
