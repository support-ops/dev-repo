---
title: Renaming File Extension Missing in RadFileExplorer for ASP.NET AJAX
description: Resolve the issue where the file extension is missing when renaming a file in RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: Fixing Missing File Extension When Renaming in RadFileExplorer
slug: renaming-file-extension-missing-radfileexplorer
tags: radfileexplorer, asp.net ajax, file extension, renaming, issue, solution
res_type: kb

## Environment
| Product | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description
When renaming a file in [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview) for ASP.NET AJAX, the file extension may be missing from the renamed file. This can cause issues when trying to open the file, as the operating system may not recognize it properly.

This KB article also answers the following questions:
- Why does the file extension disappear when renaming files in RadFileExplorer?
- How to ensure file extensions are retained when renaming in RadFileExplorer?
- What to do if renaming a file in RadFileExplorer leads to a missing extension?

## Solution
To ensure the file extension is retained when renaming a file in RadFileExplorer, follow these steps:

1. **Handle the `ItemCommand` Event**:
   Implement the `ItemCommand` event to intercept the renaming process.

   ```csharp
   protected void RadFileExplorer1_ItemCommand(object sender, RadFileExplorerEventArgs e)
   {
       if (e.Command == "RenameItem")
       {
           string newFileName = e.Argument as string;
           string fileExtension = System.IO.Path.GetExtension(e.Item.Name);
           if (!newFileName.EndsWith(fileExtension))
           {
               newFileName += fileExtension;
           }
           e.Item.Rename(newFileName);
           e.Canceled = true;
       }
   }
   ```

2. **Attach the Event Handler**:
   Attach the event handler to your RadFileExplorer component in your markup or code-behind.

   ```aspx
   <telerik:RadFileExplorer ID="RadFileExplorer1" runat="server" OnItemCommand="RadFileExplorer1_ItemCommand">
   </telerik:RadFileExplorer>
   ```

By implementing the `ItemCommand` event and ensuring the new file name retains its extension, the issue of missing file extensions when renaming in RadFileExplorer will be resolved.

## See Also
- [RadFileExplorer Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [RadFileExplorer Events](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/server-side-programming/events)
