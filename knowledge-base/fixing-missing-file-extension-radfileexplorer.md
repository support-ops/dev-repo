---
title: Fixing Missing File Extension When Renaming in RadFileExplorer
description: Learn how to fix the issue of missing file extensions when renaming files in RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: Resolving Missing File Extension Issue in RadFileExplorer
slug: fixing-missing-file-extension-radfileexplorer
tags: radfileexplorer, asp.net, ajax, file, rename, extension, missing
res_type: kb

## Environment
- Product: RadFileExplorer for ASP.NET AJAX
- Version: 2022.1.302

## Description
When renaming a file using [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview) in ASP.NET AJAX, the file extension may be missing after the rename operation. This can cause issues with file identification and usage.

This KB article also answers the following questions:
- How to retain file extension when renaming in RadFileExplorer?
- Why does the file extension disappear when renaming in RadFileExplorer?
- How to fix missing file extensions in RadFileExplorer?

## Solution
To ensure the file extension is retained when renaming files in RadFileExplorer, follow these steps:

1. **Override the `ItemCommand` Event**: Handle the `ItemCommand` event of RadFileExplorer to customize the rename functionality.
2. **Retain the File Extension**: Ensure the new file name includes the original file extension.

### Example Code
```csharp
protected void RadFileExplorer1_ItemCommand(object sender, RadFileExplorerEventArgs e)
{
    if (e.Command == "Rename")
    {
        FileExplorerItem item = e.Item;
        string originalExtension = Path.GetExtension(item.Path);
        string newFileName = e.NewName + originalExtension;

        // Perform renaming logic here
        string newPath = Path.Combine(Path.GetDirectoryName(item.Path), newFileName);
        File.Move(item.Path, newPath);

        e.Message = "File renamed successfully!";
        e.Canceled = true; // Prevent default rename operation
    }
}
```

### Steps:
1. Attach the `ItemCommand` event to your RadFileExplorer instance.
2. Check if the command is "Rename".
3. Extract the original file extension.
4. Append the original extension to the new file name.
5. Perform the rename operation using `File.Move`.
6. Set `e.Canceled = true` to prevent the default rename operation.

## See Also
- [RadFileExplorer Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [RadFileExplorer ItemCommand Event](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/server-side-programming/events/itemcommand)
- [File.Move Method](https://docs.microsoft.com/en-us/dotnet/api/system.io.file.move)
