---
title: Fixing Missing File Extension When Renaming in RadFileExplorer
description: Steps to ensure that file extensions are preserved when renaming files in RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: How to Ensure File Extensions are Preserved When Renaming in RadFileExplorer
slug: fixing-missing-file-extension-when-renaming-radfileexplorer
tags: radfileexplorer, asp.net ajax, renaming, file extension, file-system
res_type: kb

## Environment
| Product          | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description
When renaming files using [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview) for ASP.NET AJAX, the file extension may be missing after renaming. This issue can occur because the renaming action does not automatically append the file extension to the new file name.

This KB article also answers the following questions:
- How to retain file extension when renaming files in RadFileExplorer?
- Why is the file extension missing after renaming in RadFileExplorer?
- How to fix file extension issues in RadFileExplorer for ASP.NET AJAX?

## Solution
To ensure that the file extension is preserved when renaming files in RadFileExplorer, follow these steps:

1. Handle the `ItemCommand` event of RadFileExplorer.
2. Check if the command is a rename command.
3. Append the original file extension to the new name if it is missing.

Here is an example of how to implement this solution:

```csharp
protected void RadFileExplorer1_ItemCommand(object sender, RadFileExplorerEventArgs e)
{
    if (e.Command == "Rename")
    {
        string oldName = e.ExplorerItem.Path;
        string newName = e.ExplorerItem.NewPath;

        // Get the file extension of the original file
        string fileExtension = System.IO.Path.GetExtension(oldName);

        // Check if the new name already has the extension
        if (!newName.EndsWith(fileExtension))
        {
            // Append the original file extension to the new name
            e.ExplorerItem.NewPath += fileExtension;
        }
    }
}
```

## See Also
- [RadFileExplorer Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [RadFileExplorer ItemCommand Event](https://docs.telerik.com/devtools/aspnet-ajax/api/server/Telerik.Web.UI.RadFileExplorer.ItemCommand)

