---
title: Ensuring Accessibility for Kendo-Upload Interactive Controls
description: Steps to avoid accessibility failures when nesting interactive controls within the Kendo-Upload component in Angular applications.
type: how-to
page_title: Fix Accessibility Issues with Nested Interactive Controls in Kendo-Upload
slug: accessibility-issues-nested-interactive-controls-kendo-upload
tags: kendo-ui, kendo-upload, angular, accessibility, interactive-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product | Kendo UI Upload for Angular |
| --- | --- |
| Version | Current |

## Description

I am encountering an accessibility failure with the Kendo-Upload component in Angular. The issue is that interactive controls cannot be nested within each other. This results in an accessibility error when attempting to use the Kendo-Upload component within my application.

This KB article also answers the following questions:

- How to resolve accessibility issues with Kendo-Upload?
- How to avoid nesting interactive controls in Kendo-Upload?
- How to ensure Kendo-Upload meets accessibility standards?

## Solution

Follow these steps to resolve the accessibility issue caused by nesting interactive controls within the Kendo-Upload component:

1. **Review the Component Structure:** Ensure that no interactive elements (like buttons or links) are nested within other interactive elements within the Kendo-Upload component. This can often happen if you customize the template of the upload component.

2. **Refactor Custom Templates:** If you are using a custom template within the Kendo-Upload component, refactor it to ensure that interactive elements are not nested. For example, avoid having buttons inside anchor tags or other buttons.

3. **Use Appropriate ARIA Roles:** Ensure that you are using appropriate ARIA roles and attributes to make the component accessible. This includes labeling elements correctly and ensuring that the tab order is logical.

4. **Test with Screen Readers:** Use screen readers to test the component and ensure that it is fully accessible. Tools like NVDA or JAWS can help in identifying accessibility issues.

5. **Consult the Documentation:** Refer to the [Kendo-Upload](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload) official documentation for any specific guidelines on accessibility and best practices for using the component.

By following these steps, you can ensure that the Kendo-Upload component meets accessibility standards and avoids issues related to nesting interactive controls.

## See Also

- [Kendo-Upload Documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload)
- [Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Kendo UI for Angular Accessibility](https://www.telerik.com/kendo-angular-ui/components/accessibility/)


