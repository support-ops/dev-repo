---
title: Resolving Accessibility Failure for Kendo-Upload: Interactive Controls Cannot Be Nested
description: Learn how to resolve the accessibility failure issue where interactive controls cannot be nested in Kendo UI Upload for Angular.
type: how-to
page_title: Fixing Nested Interactive Controls Issue in Kendo-Upload for Angular
slug: resolving-accessibility-failure-kendo-upload-angular
tags: kendo-angular, upload, accessibility, interactive-controls, nested-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product | Progress® Kendo UI® Upload for Angular |
| ------- | ------------------------------------- |
| Version | Current                               |

## Description

I encountered an accessibility failure in my Angular application using [Kendo UI Upload](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload) where interactive controls cannot be nested. This issue arises when attempting to edit or insert a new row in a grid containing date-time pickers, and the format of the values in the TimePicker popup does not match the desired format.

This KB article also answers the following questions:
- How to fix nested interactive controls in Kendo Upload for Angular?
- How to resolve accessibility issues in Kendo UI Upload component?
- Why are my TimePicker values not displaying in the correct format?

## Solution

Follow these steps to resolve the accessibility failure issue where interactive controls cannot be nested in Kendo UI Upload for Angular:

1. Ensure that the TimePicker control's format is set correctly both in the editable field and the popup:

    ```csharp
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

2. Apply the `SetTwentyFourHourAttributes` method during the `ItemDataBound` event for the grid:

    ```csharp
    if (((e.Item is GridDataInsertItem) || (e.Item is GridEditableItem)) && e.Item.IsInEditMode)
    {
        GridEditableItem dataItem = (GridEditableItem)e.Item;
        RadTimePicker picker = (RadTimePicker)dataItem["BreakStartDateTime"].Controls[0];
        WebDateHelper.SetTwentyFourHourAttributes(picker);
    }
    ```

3. Ensure the dimensions and layout of RadGrid are correctly adjusted to prevent any container collapse issues:

    ```javascript
    window.onresize = function() {
        if ($telerik.isIE) {
            if ($get("contentZone").clientHeight < $get("contentZone").scrollHeight) {
                $get("container").style.height = document.documentElement.clientHeight + "px";
            }
        }
    }
    ```

    Define the style for the content zone:

    ```css
    #contentZone {
        position: absolute;
        top: 5px;
        bottom: 5px;
        padding: 4px;
        right: 3px;
        left: 5px;
        border: solid 1px rgb(185,187,217);
        background-color: rgb(255,255,255);
        overflow: auto;
    }
    ```

By following these steps, you can ensure that the format of the values in the TimePicker popup matches the desired format, and the accessibility issue with nested interactive controls in Kendo UI Upload is resolved.

## See Also

- [Kendo UI Upload Documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload)
- [RadTimePicker Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/datetimepicker/overview)

