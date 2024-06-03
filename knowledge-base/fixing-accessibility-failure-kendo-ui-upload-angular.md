---
title: Addressing Accessibility Failure in Kendo UI Upload for Angular
description: Resolving the issue of accessibility failure for Kendo UI Upload component in Angular applications due to nested interactive controls.
type: how-to
page_title: Fixing Accessibility Failure in Kendo UI Upload for Angular
slug: fixing-accessibility-failure-kendo-ui-upload-angular
tags: kendo-ui, upload, angular, accessibility, interactive-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product | Progress® Kendo UI® Upload for Angular |
| --- | --- |
| Version | Current |

## Description

I am encountering an accessibility failure in my Angular application using the Kendo UI Upload component. The issue is that interactive controls cannot be nested, causing accessibility problems. This KB article also answers the following questions:

- How to fix nested interactive controls in Kendo UI Upload for Angular?
- How to resolve accessibility issues in Kendo UI Upload component?
- What causes accessibility failures in Kendo UI Upload for Angular?

## Solution

1. **Avoid Nesting Interactive Controls**: Ensure that interactive controls are not nested within each other. This can be checked in the HTML structure of your application.

2. **Modify HTML Structure**: Adjust the HTML structure to separate interactive controls. Here is an example of how to restructure the HTML:

```html
<!-- Incorrect structure -->
<div>
  <label for="upload">Upload File</label>
  <div>
    <kendo-upload id="upload"></kendo-upload>
  </div>
</div>

<!-- Corrected structure -->
<label for="upload">Upload File</label>
<kendo-upload id="upload"></kendo-upload>
```

3. **Review Component Documentation**: Refer to the [Upload](https://www.telerik.com/kendo-angular-ui/components/uploads/upload/) component documentation for detailed guidelines on implementing the Kendo UI Upload component correctly.

4. **Check ARIA Attributes**: Ensure that ARIA attributes are used appropriately to enhance accessibility. This includes using `aria-label`, `aria-labelledby`, and other ARIA properties to improve screen reader support.

5. **Test with Accessibility Tools**: Use accessibility testing tools such as Axe, Lighthouse, or WAVE to identify and fix potential issues. These tools can help verify that the interactive controls are not nested and that the component meets accessibility standards.

## Suggested Workarounds

- **Custom Templates**: If restructuring the HTML is not feasible, consider using custom templates to avoid nesting interactive controls. Refer to the Kendo UI documentation for creating custom templates.

## See Also

- [Kendo UI Upload Documentation](https://www.telerik.com/kendo-angular-ui/components/uploads/upload/)
- [ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices-1.1/)
- [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/)

---

Ensure the HTML structure is correct, refer to the documentation for guidelines, and use ARIA attributes and accessibility testing tools for best results.
