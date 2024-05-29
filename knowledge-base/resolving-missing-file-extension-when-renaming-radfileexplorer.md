---
title: Resolving Missing File Extension When Renaming in RadFileExplorer
description: Fix the issue where renaming a file in RadFileExplorer for ASP.NET AJAX results in the file extension being removed.
type: how-to
page_title: Fix Missing File Extension Issue in RadFileExplorer
slug: resolving-missing-file-extension-when-renaming-radfileexplorer
tags: radfileexplorer, asp.net, ajax, renaming, file-extension, issue
res_type: kb

## Environment
| Product | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description
When renaming a file using [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview), the file extension may be missing after the operation. This typically occurs if the extension is not included in the new name provided during the rename process.

This KB article also answers the following questions:
- How to keep file extension when renaming in RadFileExplorer?
- Why does file extension disappear after renaming in RadFileExplorer?
- How to fix file extension issue in RadFileExplorer?

## Solution
To ensure the file extension is preserved when renaming a file in RadFileExplorer, follow these steps:

1. **Handle the `ItemCommand` Event**:
    Override the `ItemCommand` event of RadFileExplorer to modify the rename behavior.

    ```csharp
    protected void RadFileExplorer1_ItemCommand(object sender, Telerik.Web.UI.RadFileExplorerEventArgs e)
    {
        if (e.Command == "Rename")
        {
            var newName = e.NewName;
            var oldName = e.ExplorerItem.Name;

            if (!newName.Contains("."))
            {
                var extension = System.IO.Path.GetExtension(oldName);
                e.NewName = newName + extension;
            }
        }
    }
    ```

2. **Attach the Event Handler**:
    Ensure that the `ItemCommand` event is attached to the `RadFileExplorer` control in your ASPX page.

    ```aspx
    <telerik:RadFileExplorer ID="RadFileExplorer1" runat="server" OnItemCommand="RadFileExplorer1_ItemCommand">
    </telerik:RadFileExplorer>
    ```

By following these steps, the file extension will be automatically appended if it is not included in the new name during the rename operation.

## See Also
- [RadFileExplorer Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [RadFileExplorer ItemCommand Event](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/server-side-programming/events/itemcommand)


