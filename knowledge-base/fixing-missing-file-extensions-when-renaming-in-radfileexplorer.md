---
title: Resolving Missing File Extension When Renaming in RadFileExplorer
description: Learn how to resolve the issue of missing file extensions when renaming files using RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: Fixing Missing File Extensions When Renaming in RadFileExplorer
slug: fixing-missing-file-extensions-when-renaming-in-radfileexplorer
tags: radfileexplorer, asp.net, ajax, renaming, file, extension, missing
res_type: kb
ticketid: 1585764
---
## Environment
| Product | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description
When renaming files in [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview) for ASP.NET AJAX, the file extension may be missing after the rename operation. This issue can occur due to certain configurations or customizations in the control.

This KB article also answers the following questions:
- How do I keep the file extension when renaming files in RadFileExplorer?
- Why does the file extension disappear when renaming files in RadFileExplorer?
- What settings affect the file extension during rename in RadFileExplorer?

## Solution
To ensure that the file extension remains intact when renaming files in RadFileExplorer, follow these steps:

1. **Handle the `ItemCommand` Event:**
   Use the `ItemCommand` event to handle the renaming operation and ensure the file extension is included.

   ```csharp
   protected void RadFileExplorer1_ItemCommand(object sender, RadFileExplorerEventArgs e)
   {
       if (e.Command == "Rename")
       {
           string newFileName = e.NewName;
           string currentFilePath = e.ExplorerItem.Path;

           // Ensure the file extension is included
           string fileExtension = System.IO.Path.GetExtension(currentFilePath);
           if (!newFileName.EndsWith(fileExtension))
           {
               newFileName += fileExtension;
           }

           // Perform the rename operation with the updated file name
           e.NewName = newFileName;
       }
   }
   ```

2. **Ensure the ExplorerItem Path is Correct:**
   Verify that the `ExplorerItem` path provided in the event arguments includes the correct file path and extension.

3. **Update Web.config if Necessary:**
   Ensure configurations in `web.config` do not interfere with file handling operations in RadFileExplorer.

## See Also
- [RadFileExplorer Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [RadFileExplorer ItemCommand Event](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/client-side-programming/events/itemcommand)
- [Handling File Operations in RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/data-binding/overview)

