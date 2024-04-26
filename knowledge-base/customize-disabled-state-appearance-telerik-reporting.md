---
title: Customizing Appearance of Disabled Telerik Reporting Controls
description: Learn how to customize the appearance of disabled Telerik Reporting controls by modifying themes and utilizing the Visual Style Builder.
type: how-to
page_title: How to Customize the Disabled State Appearance for Telerik Reporting Controls
slug: customize-disabled-state-appearance-telerik-reporting
tags: progress, telerik, reporting, theming, visualstylebuilder, disabledstate
res_type: kb
related_questions: 
- How can I change the appearance of disabled controls in Telerik Reporting?
- What is the UseDefaultDisabledPaint property in Telerik Reporting?
- How do I customize themes in Telerik Reporting?
- Can I modify the disabled state appearance for controls in Telerik Reporting?
- What is the Visual Style Builder in Telerik Reporting?
ticketid: 1600927
---

## Environment
| Property | Value                   |
|----------|-------------------------|
| Product  | Progress® Telerik® Reporting 17.0.23.118 |

## Description
When working with Telerik Reporting, there might be a need to modify the appearance of controls when they are in a disabled state. The aim is to ensure the control, such as a menu item, maintains a customized look even when it is not enabled.

## Solution

1. Access the theme settings of the Telerik Reporting control you wish to customize. This process is not limited to a specific control but applies to any that supports theming.
2. For the control in question, locate the property named `UseDefaultDisabledPaint`. Set this property to `false`. This step is crucial as it enables custom styling for the disabled state.
3. Utilize the Visual Style Builder tool to create a new visual state specifically for the disabled state. When using the Visual Style Builder, this state is identified in the "State TabStrip" with the label `!Enabled`.
4. Customize the appearance of the control for the `!Enabled` state as desired. This customization will now be applied to the control when it is in a disabled state, ensuring it looks exactly as specified.

By following these steps, the appearance of Telerik Reporting controls in their disabled state can be customized to fit the desired theme and visual requirements of the project.
