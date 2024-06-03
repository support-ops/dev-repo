---
title: Fixing Accessibility Failure for Kendo-Upload: Interactive Controls Cannot Be Nested
description: Resolve the issue where Kendo-Upload in Angular applications fails accessibility checks due to nested interactive controls.
type: how-to
page_title: Resolving Accessibility Issues with Kendo-Upload for Angular
slug: fixing-accessibility-failure-kendo-upload-angular
tags: kendo-upload, angular, accessibility, nested-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product | Kendo UI Upload for Angular |
| --- | --- |
| Version | Current |

## Description

In my Angular application, the Kendo-Upload component fails accessibility checks due to nested interactive controls. This issue arises because the Kendo-Upload component contains nested buttons or input elements, which violate accessibility guidelines.

This KB article also answers the following questions:
- How to resolve nested interactive controls issue in Kendo-Upload?
- Why is Kendo-Upload failing accessibility checks?
- How to make Kendo-Upload accessible in Angular?

## Solution

Follow these steps to resolve the accessibility issue with the [Kendo-Upload](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload) component:

1. **Wrap the Kendo-Upload component with a non-interactive container:**

   Ensure the Kendo-Upload component is enclosed within a non-interactive element like a `<div>` to avoid nesting interactive controls.

   ```html
   <div>
       <kendo-upload ... ></kendo-upload>
   </div>
   ```

2. **Customize the Upload Template:**

   Modify the default template of the Kendo-Upload component to prevent interactive elements from being nested. Use a custom template to control the structure.

   ```html
   <kendo-upload>
       <ng-template kendoUploadFileTemplate let-files>
           <div *ngFor="let file of files">
               <span>{{file.name}}</span>
               <span>{{file.size}}</span>
           </div>
       </ng-template>
   </kendo-upload>
   ```

3. **Avoid Nesting Interactive Elements:**

   Ensure that any interactive elements within the Kendo-Upload component are not nested within other interactive elements. Adjust the layout and structure as necessary.

4. **Use ARIA Attributes:**

   Add appropriate ARIA (Accessible Rich Internet Applications) attributes to enhance the accessibility of the Kendo-Upload component. This includes roles and properties to improve screen reader support.

   ```html
   <kendo-upload aria-label="File Upload" role="application">
       <!-- Custom content -->
   </kendo-upload>
   ```

5. **Test Accessibility:**

   Use accessibility testing tools to verify that the Kendo-Upload component meets accessibility standards. Tools like Axe, Lighthouse, and WAVE can help identify and resolve accessibility issues.

   ```shell
   npm install -g lighthouse
   lighthouse <your-app-url>
   ```

## See Also

- [Kendo-Upload Documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload)
- [Angular Accessibility Guide](https://angular.io/guide/accessibility)
- [ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices/)

By following these steps, you can resolve the accessibility issues related to nested interactive controls in the Kendo-Upload component.
