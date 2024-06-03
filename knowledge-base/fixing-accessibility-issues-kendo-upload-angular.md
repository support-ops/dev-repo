---
title: Resolving Accessibility Failure in Kendo-Upload: Interactive Controls Cannot Be Nested
description: Learn how to address the accessibility failure in Kendo-Upload for Angular where interactive controls cannot be nested.
type: how-to
page_title: Fixing Accessibility Issues in Kendo-Upload for Angular
slug: fixing-accessibility-issues-kendo-upload-angular
tags: kendoui, upload, angular, accessibility, interactive controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product                      | Progress® Kendo UI® Upload for Angular |
| ---------------------------- | -------------------------------------- |
| Version                      | Current                               |

## Description

In my application, I am using the [Kendo UI Upload](https://www.telerik.com/kendo-angular-ui/components/uploads/upload/) for Angular. The issue arises when trying to ensure accessibility compliance; specifically, the error "Interactive controls cannot be nested" is reported. This error indicates that there are nested interactive elements, which is not allowed and creates accessibility issues.

This KB article also answers the following questions:
- How to resolve nested interactive controls in Kendo-Upload for Angular?
- How to fix accessibility errors in Kendo-Upload for Angular?
- How to ensure Kendo-Upload for Angular is accessible?

## Solution

Follow these steps to resolve the accessibility issue where interactive controls are nested within the Kendo-Upload for Angular:

1. **Avoid Nesting Interactive Elements**: Ensure that interactive elements such as buttons, links, or form controls are not nested within each other. Modify the HTML structure to separate these elements.

2. **Use ARIA Roles Properly**: Implement ARIA roles and properties to enhance accessibility without creating nested interactive controls. For example, use `role="button"` and `aria-label="Upload"` to create accessible button-like elements.

3. **Review and Refactor HTML**: Carefully inspect the HTML structure around the Kendo-Upload component. Ensure that no interactive elements are inadvertently nested within each other.

4. **Utilize Kendo-UI Accessibility Features**: Leverage Kendo-UI's built-in accessibility features. Refer to the [Kendo UI for Angular Accessibility Documentation](https://www.telerik.com/kendo-angular-ui/components/accessibility/) for detailed guidelines and best practices.

### Example

Here is an example of how to modify the HTML structure to avoid nested interactive controls:

Before:
```html
<div>
  <button>
    <input type="file" />
  </button>
</div>
```

After:
```html
<div>
  <button id="uploadButton" aria-label="Upload">Upload</button>
  <input type="file" aria-labelledby="uploadButton" />
</div>
```

By separating the button and the input elements, the accessibility issue is resolved.

## Suggested Workarounds

If the solution above does not fully resolve the issue, consider the following workarounds:

- **Custom Templates**: Create custom templates for the Kendo-Upload component to better control the HTML structure and avoid nested interactive elements.
- **Accessibility Testing Tools**: Use tools like Axe, Lighthouse, or WAVE to identify and fix other potential accessibility issues in your application.

## See Also

- [Kendo UI for Angular Upload Documentation](https://www.telerik.com/kendo-angular-ui/components/uploads/upload/)
- [Kendo UI for Angular Accessibility Documentation](https://www.telerik.com/kendo-angular-ui/components/accessibility/)
- [ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices/)


