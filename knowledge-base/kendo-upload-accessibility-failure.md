---
title: Addressing Accessibility Failure for Kendo-Upload Interactive Controls
description: Resolving the issue where interactive controls are nested in Kendo-Upload, causing accessibility failures.
type: how-to
page_title: Fixing Accessibility Failure for Kendo-Upload Interactive Controls
slug: kendo-upload-accessibility-failure
tags: kendoui, upload, angular, accessibility, interactive-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product                      | Progress® Kendo UI® Upload for Angular |
| ---------------------------- | -------------------------------------- |
| Version                      | Current                               |

## Description

In my application, I encountered an accessibility failure with the [Kendo-Upload](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload) component. The issue arises because interactive controls are nested within the Kendo-Upload, causing accessibility failures. This problem needs to be resolved to ensure proper functionality and compliance with accessibility standards.

This KB article also answers the following questions:
- How to resolve accessibility issues with Kendo-Upload?
- How to fix nested interactive controls in Kendo-Upload?
- How to make Kendo-Upload compliant with accessibility standards?

## Solution

To resolve the accessibility failure where interactive controls are nested within the Kendo-Upload component, follow these steps:

1. **Avoid Nesting Interactive Controls**:
   Ensure that no interactive controls (like buttons or links) are placed inside the Kendo-Upload's interactive areas. If you need additional interactivity, place those controls outside the Kendo-Upload component.

2. **Use Accessible Labels**:
   Add appropriate `aria-label` or `aria-labelledby` attributes to the Kendo-Upload and its child elements to improve accessibility.

3. **Review and Adjust the Component's Markup**:
   Ensure that the HTML structure of the page does not violate accessibility rules by nesting interactive elements improperly.

4. **Use Kendo's Accessibility Features**:
   Utilize Kendo UI's built-in accessibility features to enhance the component's accessibility. Refer to the Kendo UI documentation for best practices.

5. **JavaScript Workaround**:
   If necessary, implement a JavaScript workaround to ensure that the component meets accessibility standards. For example, you can dynamically adjust the DOM to prevent nesting issues:

   ```javascript
   document.addEventListener('DOMContentLoaded', function() {
       let uploadElements = document.querySelectorAll('.k-upload');
       uploadElements.forEach(el => {
           if (el.querySelector('.interactive-control')) {
               let control = el.querySelector('.interactive-control');
               el.parentElement.insertBefore(control, el.nextSibling);
           }
       });
   });
   ```

By following these steps, you can resolve the accessibility failure and ensure that the Kendo-Upload component functions correctly and complies with accessibility standards.

## See Also

- [Kendo-Upload Documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload)
- [Accessibility in Kendo UI](https://docs.telerik.com/kendo-ui/accessibility/overview)
