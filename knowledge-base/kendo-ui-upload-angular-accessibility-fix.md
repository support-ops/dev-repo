---
title: Addressing Accessibility Failure in Kendo UI Upload for Angular: Interactive Controls Can Not Be Nested
description: Resolve the issue of nested interactive controls in Kendo UI Upload for Angular causing accessibility failures.
type: how-to
page_title: Fixing Nested Interactive Controls in Kendo UI Upload for Angular
slug: kendo-ui-upload-angular-accessibility-fix
tags: kendo-ui, upload, angular, accessibility, interactive-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product | Kendo UI Upload for Angular |
| --- | --- |
| Version | Current |

## Description

In my application, I encountered an accessibility failure with the [Kendo UI Upload for Angular](https://docs.telerik.com/kendo-ui/components/uploads/upload/overview). The issue arises when interactive controls are nested within the upload component, causing accessibility problems.

This KB article also answers the following questions:
- How to prevent accessibility issues with Kendo UI Upload for Angular?
- How to handle nested interactive controls in Kendo UI Upload?
- How to fix accessibility violations in Kendo UI Upload?

## Solution

To resolve the issue of nested interactive controls causing accessibility failures in the Kendo UI Upload for Angular, follow these steps:

1. **Avoid Nesting Interactive Controls**: Ensure that no interactive controls are nested within the Kendo UI Upload component. This includes buttons, input fields, and other clickable elements.

2. **Use Appropriate Containers**: If you need to group elements, use non-interactive containers such as `<div>` or `<span>` instead of interactive elements.

3. **Update the Template**: Modify the template to ensure that interactive elements are not nested within the upload component.

Example:
```html
<kendo-upload>
  <div class="upload-container">
    <!-- Non-interactive container to group elements -->
  </div>
</kendo-upload>
```

4. **Check ARIA Roles and Attributes**: Ensure that ARIA roles and attributes are correctly applied to avoid conflicts and accessibility violations.

5. **Test for Accessibility Compliance**: Use tools like aXe or Lighthouse to test your application for accessibility compliance and ensure that the issue is resolved.

By following these steps, you can address the accessibility failure caused by nested interactive controls in the Kendo UI Upload for Angular.

## See Also

- [Kendo UI Upload Documentation](https://docs.telerik.com/kendo-ui/components/uploads/upload/overview)
- [ARIA Roles and Attributes](https://www.w3.org/TR/wai-aria-1.1/#roles)
- [Accessibility Testing Tools](https://developer.chrome.com/docs/lighthouse/accessibility/)


