---
title: Formatting TimePicker in RadGrid for 24-Hour Clock Display
description: Learn how to format the TimePicker control in a Telerik RadGrid column for 24-hour or 12-hour clock display based on system settings.
type: how-to
page_title: How to Format TimePicker in Telerik RadGrid for Different Time Displays
slug: format-timepicker-radgrid-24-hour-clock
tags: radgrid, timepicker, dataformatstring, itemdatabound, insertcommand
res_type: kb
related_questions:
  - How can I change the time format in the TimePicker control inside a RadGrid?
  - What is the correct way to format TimePicker based on system options?
  - How do I adjust TimePicker format in RadGrid edit mode?
  - Can the TimePicker display format be dynamically set in RadGrid?
  - How to apply 24-hour format in TimePicker within RadGrid?
ticketid: 1582080
---

## Environment

| Product | Version |
| --- | --- |
| Progress® Kendo UI® Upload for Angular | N/A |

## Description

In my application, a Telerik RadGrid includes various columns, one of which is a `GridDateTimeColumn` configured as a `TimePicker`. I need to dynamically set the time display format (24-hour or 12-hour clock) for both the grid display and the TimePicker popup based on a system option. While the grid display format adjusts correctly, the TimePicker popup still shows times in the "hh:mm tt" format regardless of the system setting.

## Solution

To format the TimePicker control in a Telerik RadGrid column based on system settings, follow these steps:

1. Dynamically set the `DataFormatString` for the `GridDateTimeColumn` during the `PreRender` event of the RadGrid to match the system option for time display format.

2. In the `ItemDataBound` event handler of the RadGrid, access the `TimePicker` control and apply the correct time format as per the system settings.

Here's how you can accomplish this:

```csharp
protected void grdBreaksList_PreRender(object sender, EventArgs e)
{
    if (Session["SESSION_BREAK_DATA"] != null)
    {
        foreach (GridColumn column in grdBreaksList.Columns)
        {
            if (column.UniqueName == "BreakStartDateTime" || column.UniqueName == "BreakEndDateTime")
            {
                if (SysOption.IsDisplayTime24HourClock)
                {
                    (column as GridBoundColumn).DataFormatString = "{0:HH:mm}";
                }
                else
                {
                    (column as GridBoundColumn).DataFormatString = "{0:t}";
                }
            }
        }
        grdBreaksList.Rebind();
    }
}

protected void grdBreaksList_ItemDataBound(object sender, GridItemEventArgs e)
{
    if (((e.Item is GridDataInsertItem) || (e.Item is GridEditableItem)) && e.Item.IsInEditMode)
    {
        GridEditableItem dataItem = (GridEditableItem)e.Item;
        RadTimePicker picker = (RadTimePicker)dataItem["BreakStartDateTime"].Controls[0];
        SetTwentyFourHourAttributes(picker);
    }
}

public static void SetTwentyFourHourAttributes(RadTimePicker inControl)
{
    StringBuilder format = new StringBuilder();
    CultureInfo culture;

    if (SysOption.IsDisplayTime24HourClock)
    {
        format.Append("HH:mm");
    }
    else
    {
        format.Append("hh:mm tt");
    }

    if (PremisePrincipal.Current != null && PremisePrincipal.Current.LocalityCd != null)
    {
        culture = new CultureInfo(PremisePrincipal.Current.LocalityCd);
    }
    else
    {
        culture = new CultureInfo(SysOption.DefaultLocalityCd);
    }

    inControl.DateInput.Culture = culture;
    inControl.TimeView.TimeFormat = format.ToString();
    inControl.DateInput.DateFormat = format.ToString();
    inControl.DateInput.DisplayDateFormat = format.ToString();
}
```

This solution ensures that both the grid display and the TimePicker popup reflect the correct time format as per the system's configuration.

## Notes

- Ensure that `SysOption.IsDisplayTime24HourClock` correctly reflects the system setting for the time display format.
- The culture setting can influence how time is displayed. Adjust the culture settings as necessary to match your application's requirements.

## See Also

- [RadGrid for ASP.NET AJAX Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/grid/overview)
- [RadTimePicker for ASP.NET AJAX Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/timepicker/overview)
- [Customizing the Date and Time Format](https://docs.telerik.com/devtools/aspnet-ajax/controls/dateinput/overview)
