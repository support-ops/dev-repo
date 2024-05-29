---
title: Fixing Missing File Extension When Renaming in RadFileExplorer
description: Learn how to address the issue of missing file extensions when renaming files in RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: Resolving Missing File Extension in RadFileExplorer When Renaming
slug: fixing-missing-file-extension-radfileexplorer
tags: radfileexplorer, asp.net ajax, file, rename, missing, extension
res_type: kb

## Environment
| Product | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description

When renaming files in [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview) for ASP.NET AJAX, the file extension may disappear. This can cause issues with file recognition and usability.

This KB article also answers the following questions:
- How to ensure file extensions remain when renaming in RadFileExplorer?
- What causes file extensions to disappear in RadFileExplorer?
- How to fix missing file extensions in RadFileExplorer?

## Solution

1. **Update the `RadFileExplorer` Configuration**:
   Ensure the `EnableRename` property is set to `True` in the `RadFileExplorer` configuration. This allows renaming functionality to be correctly processed.
   ```xml
   <telerik:RadFileExplorer ID="RadFileExplorer1" runat="server" EnableRename="True">
   </telerik:RadFileExplorer>
   ```

2. **Handle the `ItemCommand` Event**:
   Implement the `ItemCommand` event in the code-behind to manage file extensions during the rename process. This event will check if the file extension is missing and append it if necessary.
   ```csharp
   protected void RadFileExplorer1_ItemCommand(object sender, Telerik.Web.UI.RadFileExplorerEventArgs e)
   {
       if (e.Command == "Rename")
       {
           string oldExtension = System.IO.Path.GetExtension(e.ExplorerItem.Path);
           string newExtension = System.IO.Path.GetExtension(e.NewName);

           if (string.IsNullOrEmpty(newExtension))
           {
               e.NewName += oldExtension;
           }
       }
   }
   ```

3. **Bind the Event in the ASPX Page**:
   Ensure the `ItemCommand` event is properly bound in the ASPX page.
   ```xml
   <telerik:RadFileExplorer ID="RadFileExplorer1" runat="server" EnableRename="True" OnItemCommand="RadFileExplorer1_ItemCommand">
   </telerik:RadFileExplorer>
   ```

Following these steps will ensure that file extensions are preserved when renaming files in RadFileExplorer.

## See Also
- [RadFileExplorer Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [Handling the ItemCommand Event](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/server-side-programming/itemcommand)
- [RadFileExplorer Configuration](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/configuration)
