---
title: Displaying Watermarks in Telerik DatePicker and TimePicker
description: Learn how to add placeholder text, such as "Date Of Birth", to Telerik DatePicker and TimePicker controls.
type: how-to
page_title: How to Add Placeholder Text to Telerik DatePicker and TimePicker Controls
slug: displaying-watermarks-in-telerik-datepicker-and-timepicker
tags: progress, telerik, reporting, datepicker, timepicker, watermark
res_type: kb
category: knowledge-base
related_questions:
- How to display placeholder text in Telerik DatePicker?
- How to add a watermark to Telerik TimePicker?
- How to use placeholder text in Telerik controls?
- Customizing the appearance of Telerik DatePicker and TimePicker
- Setting up watermarks in Telerik input controls
ticketid: 1581926
---

## Environment

| Product Name                  | Version        |
|-------------------------------|----------------|
| Progress® Telerik® Reporting | 16.2.22.914    |

## Description

When utilizing the Telerik DatePicker and TimePicker controls, adding a watermark such as "Date Of Birth" can enhance the user interface by providing context or instructions directly within the input fields. This article demonstrates how to implement watermarks in these controls.

## Solution

To display a watermark in Telerik DatePicker and TimePicker controls, follow these steps:

1. **For the DatePicker:**
   - Use the `EmptyMessage` property to set your watermark text. This property displays a specified string when the control's input is empty.

```html
<telerik:RadDatePicker ID="RadDatePicker1" runat="server" EmptyMessage="Date Of Birth">
</telerik:RadDatePicker>
```

2. **For the TimePicker:**
   - Similar to the DatePicker, utilize the `EmptyMessage` property for the TimePicker to display the watermark text when no time is selected.

```html
<telerik:RadTimePicker ID="RadTimePicker1" runat="server" EmptyMessage="Select Time">
</telerik:RadTimePicker>
```

By setting the `EmptyMessage` property, you can easily add a watermark to both the DatePicker and TimePicker controls, guiding users with contextual placeholders.

## See Also

- [RadDatePicker Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/datepicker/overview)
- [RadTimePicker Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/timepicker/overview)
- [Customizing RadDatePicker](https://docs.telerik.com/devtools/aspnet-ajax/controls/datepicker/functionality/empty-message)
- [Customizing RadTimePicker](https://docs.telerik.com/devtools/aspnet-ajax/controls/timepicker/functionality/empty-message)
