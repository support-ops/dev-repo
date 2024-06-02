---
title: Angel
description: Learn how to integrate Angular Sass themes into a Blazor application effectively.
type: how-to
page_title: Integrating Angular Sass Themes into Blazor
slug: integrating-angular-sass-themes-blazor
tags: web themes, angular, sass, blazor
res_type: kb
ticketid: 1601906
---

## Environment

| Product | Web Themes |
| --- | --- |
| Version | N/A |

## Description

I want to integrate Angular Sass themes into my Blazor application. This process involves ensuring the Angular Sass themes are compatible with Blazor and applying them correctly to achieve the desired styling.

This KB article also answers the following questions:
- How to use Angular Sass themes in Blazor?
- How to apply Angular themes to Blazor components?
- How to style Blazor components with Sass themes?

## Solution

1. **Prepare the Angular Sass Theme:**
   - Ensure that the Sass theme is well-structured and compatible with your Blazor project. 

2. **Integrate Angular Sass Theme into Blazor:**
   - Add the Sass theme files into your Blazor project's `wwwroot` folder.
   - Update the `index.html` or `_Host.cshtml` to include the theme stylesheet.
   
   ```html
   <link href="css/angular-theme.css" rel="stylesheet" />
   ```

3. **Compile Sass in Blazor:**
   - Use a Sass compiler like `sass` or a task runner to compile the Sass files into CSS.
   - Ensure the output CSS is placed in the `wwwroot` folder and referenced in your project.

4. **Apply Theme to Blazor Components:**
   - Use CSS classes from the compiled theme in your Blazor components.
   - Apply custom styles by extending the theme classes in your component styles if necessary.

5. **Testing and Adjustments:**
   - Test the theme integration across different components and pages.
   - Make necessary adjustments to the Sass files and recompile if required.

## Suggested Workarounds

- If the direct integration approach does not yield the desired results, consider creating custom styles specific to Blazor components by leveraging the base styles from the Angular Sass theme.

## Notes

- Ensure that the theme styles do not conflict with existing Blazor component styles. Use scoped CSS if necessary to avoid global style conflicts.

## See Also

- [Blazor Documentation](https://docs.microsoft.com/en-us/aspnet/core/blazor/)
- [Sass Documentation](https://sass-lang.com/documentation)
- [Angular Theming Guide](https://angular.io/guide/theming)
