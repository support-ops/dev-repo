---
title: Customizing Disabled State Appearance for Telerik Reporting Controls
description: Learn how to customize the appearance of Telerik Reporting controls when in a disabled state by modifying themes and utilizing the Visual Style Builder.
type: how-to
page_title: How to Customize Disabled State Appearance in Telerik Reporting Controls
slug: customize-disabled-state-appearance-telerik-reporting
tags: progress, telerik, reporting, theme, visual style builder, disabled state
res_type: kb
related_questions:
  - How to modify Telerik Reporting control themes?
  - How to use Visual Style Builder with Telerik Reporting?
  - How to change disabled state appearance in Telerik Reporting?
  - How to set UseDefaultDisabledPaint property in Telerik Reporting?
  - What is InPlace EditMode in Telerik Reporting?
ticketid: 1600927
---

## Environment
| Product | Version |
| --- | --- |
| Progress® Telerik® Reporting | 17.0.23.118 |

## Description
When using Telerik Reporting, there might be a need to customize the appearance of controls in their disabled state. This customization involves modifying control themes, setting properties, and using the Visual Style Builder.

## Solution
To customize the appearance of Telerik Reporting controls, such as RadMenuItem, in their disabled state, follow these steps:

1. Modify each control's theme. This includes not just the Menu theme but potentially others based on your application's needs.
2. Set the `UseDefaultDisabledPaint` property of the respective item (e.g., RadMenuItem) to `false`. This action ensures that the default painting for disabled items is not used, allowing for custom styling.
3. Utilize the Visual Style Builder to create a new state specifically for the disabled state of the menu item. In the Visual Style Builder, this state should appear in the "State TabStrip" as "!Enabled".
4. Customize the appearance for the "!Enabled" state as per your requirements. This customization will be applied to the menu item when it is in a disabled state.

By following these steps, you can ensure that the menu item, or any other Telerik Reporting control, will appear just as you have customized it for the "!Enabled" state when it's disabled. This approach allows for a more consistent and tailored application UI.

## Notes
- The `UseDefaultDisabledPaint` property is a crucial part of this customization process. Make sure it is set to `false` for the controls you wish to customize.
- The Visual Style Builder is a powerful tool for theme customization. Familiarize yourself with its features and capabilities to make the most out of your theme customizations.

## See Also
- [Telerik Reporting Documentation](https://docs.telerik.com/reporting/)
- [Telerik Visual Style Builder](https://docs.telerik.com/reporting/visual-style-builder)
- [MasterTableView EditMode Documentation](https://docs.telerik.com/reporting/mastertableview-editmode)
