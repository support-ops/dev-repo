---
title: Fixing Missing File Extension When Renaming in RadFileExplorer
description: Learn how to fix the issue of missing file extensions when renaming files in RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: Resolving Missing File Extension in RadFileExplorer Renaming
slug: fixing-missing-file-extension-radfileexplorer
tags: radfileexplorer, asp.net ajax, rename, file extension, missing, 2022.1.302
res_type: kb

## Environment

| Product | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description

When renaming files using [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview) for ASP.NET AJAX, the file extension may disappear. This usually happens due to improper handling of the file name and extension during the renaming process.

This KB article also answers the following questions:
- How to keep file extensions when renaming in RadFileExplorer?
- Why does the file extension disappear when renaming files in RadFileExplorer?
- How can I fix missing file extensions in RadFileExplorer for ASP.NET AJAX?

## Solution

To ensure the file extension is retained when renaming files in RadFileExplorer, follow these steps:

1. **Override the `FileExplorer`'s `OnClientItemRename` Event:**

   Attach a custom JavaScript function to the `OnClientItemRename` event to handle the renaming process correctly.

   ```javascript
   function onClientItemRename(sender, args) {
       var item = args.get_item();
       var newName = args.get_newName();

       // Extract the file extension
       var extension = item.get_name().split('.').pop();
       if (newName.indexOf('.') === -1) {
           newName += '.' + extension;
       }

       args.set_newName(newName);
   }
   ```

2. **Configure the `RadFileExplorer` Control:**

   Bind the `OnClientItemRename` event to the custom JavaScript function defined above.

   ```html
   <telerik:RadFileExplorer ID="RadFileExplorer1" runat="server"
       OnClientItemRename="onClientItemRename">
       ...
   </telerik:RadFileExplorer>
   ```

Following these steps ensures that the file extension is preserved during the renaming process in RadFileExplorer.

## See Also

- [RadFileExplorer Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [RadFileExplorer Client-Side API](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/client-side-programming/client-side-api)

