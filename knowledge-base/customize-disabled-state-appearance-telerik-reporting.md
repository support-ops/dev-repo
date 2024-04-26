---
title: Customizing Disabled State Appearance for Controls in Telerik Reporting
description: Learn how to modify the appearance of controls in their disabled state using the Visual Style Builder in Telerik Reporting.
type: how-to
page_title: How to Customize Disabled State Appearance for Telerik Reporting Controls
slug: customize-disabled-state-appearance-telerik-reporting
tags: progress, telerik, reporting, visual style builder, disabled state, customization
res_type: kb
related_questions: 
- How do I change the disabled state appearance of a Telerik Reporting control?
- Can I customize the appearance of controls in Telerik Reporting?
- What is the UseDefaultDisabledPaint property in Telerik Reporting?
- How to use the Visual Style Builder for Telerik Reporting?
- Can I create custom states for controls in Telerik Reporting?
ticketid: 1600927
---

## Environment

| Product | Version |
| --- | --- |
| Progress® Telerik® Reporting | 17.0.23.118 |

## Description

When customizing the appearance of controls in Telerik Reporting, you might want to specifically tailor how they look when disabled. The default disabled state may not align with your desired aesthetic or may lack the clarity you want. This guide demonstrates how to modify the appearance of any control, such as a menu item, for its disabled state using the Visual Style Builder.

## Solution

1. Ensure the `UseDefaultDisabledPaint` property of the control you wish to customize (e.g., `RadMenuItem`) is set to `false`. This action allows for customization beyond the default disabled appearance.
   
2. Open the Visual Style Builder tool provided with Telerik Reporting.
   
3. Navigate to the control you are customizing and locate the "State TabStrip" area within the tool.

4. Create a new state for the disabled condition of the control. In the Visual Style Builder, this state should be labeled as "!Enabled". This label indicates that the state is specifically for when the control is not enabled, or disabled.

5. Customize the appearance of the control for the "!Enabled" state as per your requirements. Your modifications here will directly affect how the control appears when it is disabled in your application.

By following these steps, the control will display with the customized appearance you've set for its disabled state, offering a consistent and tailored look across your reporting application.

## Notes

- The Visual Style Builder is a powerful tool that allows for extensive customization of the appearance of controls in Telerik Reporting. It provides a visual interface for creating and modifying themes and states of controls.
  
- The `UseDefaultDisabledPaint` property is crucial for enabling custom appearance modifications for disabled states. Ensure that it is set to `false` to apply your customizations.

## See Also

- [Telerik Reporting Documentation](https://docs.telerik.com/reporting/)
- [VisualStyleBuilder Overview](https://docs.telerik.com/reporting/visual-style-builder)
- [Customizing Themes in Telerik Reporting](https://docs.telerik.com/reporting/designing-reports-styling-and-formatting-customizing-themes)
