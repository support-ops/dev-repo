---
title: Displaying Watermarks in Telerik DatePicker and TimePicker
description: Learn how to add custom watermarks, such as "Date of Birth", to the Telerik DatePicker and TimePicker controls.
type: how-to
page_title: How to Add Watermarks to Telerik DatePicker and TimePicker Controls
slug: display-watermarks-telerik-datepicker-timepicker
tags: watermark, datepicker, timepicker, text
res_type: kb
related_questions: 
  - How can I add a placeholder text to Telerik DatePicker?
  - How to display custom text in Telerik TimePicker?
  - What is the way to add watermarks in Telerik DatePicker and TimePicker?
  - Can I show "Date of Birth" as a watermark in Telerik DatePicker?
  - How to customize Telerik DatePicker and TimePicker with watermarks?
ticketid: 1581926
---

## Environment

| Product | Version |
| --- | --- |
| Progress® Telerik® Reporting | 16.2.22.914 |

## Description

I need to display a watermark, such as "Date of Birth", inside Telerik DatePicker and TimePicker controls.

## Solution

To display a watermark in Telerik DatePicker and TimePicker controls, follow these steps:

1. For the **DatePicker**, use the **Placeholder** property to set the watermark text:

    ```html
    <telerik:RadDatePicker ID="RadDatePicker1" runat="server" Placeholder="Date of Birth">
    </telerik:RadDatePicker>
    ```

2. For the **TimePicker**, similarly, set the **Placeholder** property:

    ```html
    <telerik:RadTimePicker ID="RadTimePicker1" runat="server" Placeholder="Select Time">
    </telerik:RadTimePicker>
    ```

These properties allow you to display custom text inside the input field of the DatePicker and TimePicker when no date or time is selected, effectively serving as a watermark.

## Notes

Ensure that the version of Telerik controls you are using supports the Placeholder property. Update your Telerik controls if necessary to utilize this feature. 

## See Also

- [RadDatePicker Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/datepicker/overview)
- [RadTimePicker Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/timepicker/overview)
- [Customizing the Appearance of RadControls for ASP.NET AJAX](https://docs.telerik.com/devtools/aspnet-ajax/general-information/controlling-visual-appearance/overview)
