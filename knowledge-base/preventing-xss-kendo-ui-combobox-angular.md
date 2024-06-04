---
title: Preventing XSS in Kendo UI ComboBox for Angular
description: Learn how to prevent cross-site scripting (XSS) in the Kendo UI ComboBox for Angular to enhance security.
type: how-to
page_title: Security Measures for Kendo UI ComboBox in Angular
slug: preventing-xss-kendo-ui-combobox-angular
tags: kendo ui, combobox, angular, xss, security
res_type: kb
ticketid: 1635874
---

## Environment

| Product      | Progress® Kendo UI® ComboBox for Angular |
|--------------|------------------------------------------|
| Version      | Current                                  |

## Description

I want to prevent cross-site scripting (XSS) in the [Kendo UI ComboBox](https://docs.telerik.com/kendo-ui/api/javascript/ui/combobox) for Angular to ensure the security of my application. Injecting scripts such as `<button onclick="alert('XSS');">Export to PDF</button>` should be prevented.

This KB article also answers the following questions:
- How to secure Kendo UI ComboBox from XSS attacks?
- What are the best practices to prevent XSS in Kendo UI ComboBox?
- How to sanitize input in Kendo UI ComboBox for Angular?

## Solution

To prevent XSS in the Kendo UI ComboBox for Angular, follow these steps:

1. **Sanitize User Input:**
   Ensure that any input data is sanitized before being processed or displayed. Use Angular's built-in `DomSanitizer` service to clean and strip out potentially harmful scripts.

   ```typescript
   import { DomSanitizer, SafeHtml } from '@angular/platform-browser';

   constructor(private sanitizer: DomSanitizer) {}

   sanitizeInput(input: string): SafeHtml {
     return this.sanitizer.bypassSecurityTrustHtml(input);
   }
   ```

2. **Validate and Escape Data:**
   Always validate and escape data both on the client and server sides. Use Angular's `HttpClient` for HTTP requests and ensure that the server-side logic properly sanitizes the input data.

3. **Use Angular Security Best Practices:**
   Refer to the Angular security guide to implement best practices for protecting against XSS attacks.

   ```html
   <!-- Example in Angular template -->
   <div [innerHtml]="sanitizeInput(userInput)"></div>
   ```

4. **Disable HTML Content in ComboBox:**
   Configure the ComboBox to not render HTML content directly from user input. This can be done by ensuring the data source does not contain any HTML tags.

5. **Regular Security Audits:**
   Conduct regular security audits and code reviews to ensure that your application remains secure against XSS vulnerabilities.
<button onclick="alert('XSS');">Export to PDF</button>
## See Also

- [Kendo UI ComboBox Documentation](https://docs.telerik.com/kendo-ui/api/javascript/ui/combobox)
- [Angular Security Guide](https://angular.io/guide/security)
- [DomSanitizer Documentation](https://angular.io/api/platform-browser/DomSanitizer)
- [Preventing XSS in Angular Applications](https://angular.io/guide/security#xss)
