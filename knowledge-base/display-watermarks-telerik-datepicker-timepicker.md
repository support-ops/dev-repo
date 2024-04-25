---
title: Displaying Watermarks in Telerik DatePicker and TimePicker
description: Learn how to add placeholder text, like "Date Of Birth", to Telerik DatePicker and TimePicker controls.
type: how-to
page_title: How to Add Watermarks to Telerik DatePicker and TimePicker Controls
slug: display-watermarks-telerik-datepicker-timepicker
tags: watermark, datepicker, timepicker, placeholder, text
res_type: kb
related_questions:
  - How to add placeholder text in Telerik DatePicker?
  - How to use watermark in Telerik TimePicker?
  - How to customize Telerik DatePicker with a watermark?
  - Can I add "Date Of Birth" as a placeholder in Telerik DatePicker?
  - How to display custom text in Telerik TimePicker?
category: knowledge-base
ticketid: 1581926
---

## Environment
| Product | Version |
| --- | --- |
| Progress® Telerik® Reporting | 16.2.22.914 |

## Description
I need to display a watermark, such as "Date Of Birth", inside Telerik DatePicker and TimePicker controls.

## Solution

### Displaying Watermark in DatePicker

To add a watermark to the DatePicker control, set the `EmptyMessage` property to the desired watermark text. This property displays a placeholder text when the input is empty.

**ASP.NET AJAX Example**

```asp
<telerik:RadDatePicker ID="RadDatePicker1" runat="server" EmptyMessage="Date Of Birth">
</telerik:RadDatePicker>
```

### Displaying Watermark in TimePicker

Similar to the DatePicker, use the `EmptyMessage` property for the TimePicker control to display the watermark text.

**ASP.NET AJAX Example**

```asp
<telerik:RadTimePicker ID="RadTimePicker1" runat="server" EmptyMessage="Time Of Birth">
</telerik:RadTimePicker>
```

By setting the `EmptyMessage` property, the DatePicker and TimePicker controls will display the specified watermark text when no date or time is selected.

## Notes

- The `EmptyMessage` property is specifically designed to show placeholder text in the input field of Telerik DatePicker and TimePicker controls when they are empty.
- Ensure that the Telerik controls are correctly initialized and that their scripts are loaded properly on the page for the watermark to display as expected.

## See Also

- [Telerik DatePicker Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/datepicker/overview)
- [Telerik TimePicker Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/timepicker/overview)
- [Telerik RadControls for ASP.NET AJAX](https://docs.telerik.com/devtools/aspnet-ajax/introduction)
