---
title: Customizing the Appearance of Disabled Menu Items in Telerik Reporting
description: Learn how to modify the theme of Telerik Reporting controls to customize the appearance of disabled menu items.
type: how-to
page_title: How to Customize Disabled State Appearance for Menu Items in Telerik Reporting
slug: customize-appearance-disabled-menu-items-telerik-reporting
tags: progress, telerik, reporting, theme, customization, visual style builder, radmenuitem, usedefaultdisabledpaint
res_type: kb
related_questions:
  - How can I change the appearance of disabled menu items in Telerik Reporting?
  - What steps are needed to customize disabled state styles in Telerik Reporting?
  - How to use Visual Style Builder for customizing Telerik Reporting controls?
  - Can I modify the theme of individual Telerik Reporting controls?
  - How do I prevent default disabled paint in Telerik Reporting menu items?
ticketid: 1600927
---

## Environment

| Product          | Version       |
|------------------|---------------|
| Progress® Telerik® Reporting | 17.0.23.118 |

## Description

When working with Telerik Reporting, it's often necessary to customize the appearance of various UI elements to match the application's theme. Specifically, modifying the look of disabled menu items requires a particular approach to ensure they appear as intended when disabled.

## Solution

To customize the appearance of disabled menu items in Telerik Reporting, follow these steps:

1. Modify the theme of the control you wish to customize. This process applies not only to the Menu theme but to any Telerik Reporting control.
   
2. For the specific item you want to customize (e.g., `RadMenuItem`), set the `UseDefaultDisabledPaint` property to `false`. This step ensures that the default disabled appearance is not applied, allowing for custom styling.

   ```csharp
   radMenuItem.UseDefaultDisabledPaint = false;
   ```

3. Use the Visual Style Builder to create a new state for the disabled menu item. In the Visual Style Builder, this state should be labeled as "!Enabled" within the "State TabStrip". This designation allows you to apply custom styling specifically for the disabled state.

4. Customize the appearance for the "!Enabled" state as desired. Your customizations will now be applied to the menu item when it is disabled, ensuring it appears according to your specifications.

By following these steps, you can effectively customize the appearance of disabled menu items in Telerik Reporting, providing a consistent look and feel that matches your application's overall theme.

## Notes

- The Visual Style Builder is a powerful tool for customizing the themes of Telerik Reporting controls. Familiarize yourself with its features to fully leverage its capabilities for theme customization.
- Remember to test the appearance of the disabled menu items in your application to ensure the customizations meet your expectations.

## See Also

- [Telerik Reporting Documentation](https://docs.telerik.com/reporting/)
- [Telerik Visual Style Builder](https://docs.telerik.com/reporting/tools/visual-style-builder)
- [RadMenuItem Documentation](https://docs.telerik.com/reporting/)
