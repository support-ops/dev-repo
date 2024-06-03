---
title: Resolving Accessibility Failure for Kendo UI Upload in Angular
description: Learn how to fix the accessibility failure in Kendo UI Upload for Angular where interactive controls cannot be nested.
type: how-to
page_title: Fixing Nested Interactive Controls in Kendo UI Upload for Angular
slug: resolving-accessibility-failure-kendo-upload-angular
tags: kendo-ui, angular, upload, accessibility, interactive-controls
res_type: kb
ticketid: 1582080
---

## Environment

| Product | Kendo UI Upload for Angular | 
| --- | --- |
| Version | Current |

## Description

In Kendo UI Upload for Angular, you may encounter an accessibility failure where interactive controls are nested. This issue occurs because the Upload component nests interactive elements, which violates accessibility guidelines.

This KB article also answers the following questions:
- How to resolve nested interactive controls issue in Kendo UI Upload?
- How to fix accessibility issues in Kendo UI Upload for Angular?
- How to make Kendo UI Upload component accessible?

## Solution

Follow these steps to resolve the accessibility issue:

1. **Avoid Nesting Interactive Elements:** Ensure that interactive controls like buttons, links, and form inputs are not nested within each other.

2. **Use ARIA Roles and Attributes:** Enhance the accessibility of the Upload component by using appropriate ARIA roles and attributes. Refer to the official [Kendo UI Upload documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload) for more details.

3. **Custom Templates:** Customize the Kendo UI Upload templates to avoid nesting of interactive controls. Below is an example of how to customize the template:

    ```html
    <kendo-upload
        [saveUrl]="'saveUrl'"
        [removeUrl]="'removeUrl'"
    >
        <ng-template kendoUploadFileTemplate let-file="file" let-files="files">
            <span>{{ file.name }}</span>
            <button kendoButton (click)="removeFile(file)">Remove</button>
        </ng-template>
    </kendo-upload>
    ```

4. **Event Handling:** Ensure that event handlers are not attached to parent elements that contain interactive children. Attach events directly to the interactive elements.

By following these steps, you can resolve the accessibility issue in Kendo UI Upload for Angular.

## See Also

- [Kendo UI Upload Documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload)
- [Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/#keyboard-accessible)
