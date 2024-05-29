---
title: Fixing Missing File Extension When Renaming in RadFileExplorer
description: Learn how to resolve the issue of missing file extensions when renaming files in RadFileExplorer for ASP.NET AJAX.
type: how-to
page_title: How to Fix Missing File Extension When Renaming in RadFileExplorer
slug: fix-missing-file-extension-renaming-radfileexplorer
tags: radfileexplorer, asp.net-ajax, renaming, file-extension, missing-extension
res_type: kb
ticketid: 1585764
---
## Environment

| Product | RadFileExplorer for ASP.NET AJAX 2022.1.302 |

## Description

When renaming a file in [RadFileExplorer](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview), the file extension might be missing. This issue can occur if the file extension is not included in the new name during the renaming process.

This KB article also answers the following questions:
- How to ensure the file extension remains when renaming files in RadFileExplorer?
- What to do if the file extension disappears after renaming in RadFileExplorer?
- How to handle file renaming issues in RadFileExplorer?

## Solution

To resolve this issue, follow these steps:

1. **Handle the `OnClientFileRenaming` event**:
   - Use the `OnClientFileRenaming` event to ensure the file extension is included in the new name.

2. **Add JavaScript to handle the event**:
   - Implement JavaScript to check if the new name includes a file extension. If not, append the original extension.

```javascript
function onClientFileRenaming(sender, args) {
    var item = args.get_item();
    var newName = args.get_newName();
    var originalName = item.get_name();
    var originalExtension = originalName.substring(originalName.lastIndexOf('.'));

    if (newName.indexOf('.') === -1) {
        args.set_newName(newName + originalExtension);
    }
}
```

3. **Attach the event to the RadFileExplorer**:
   - In your ASPX page, attach the `OnClientFileRenaming` event to the RadFileExplorer.

```aspx
<telerik:RadFileExplorer ID="RadFileExplorer1" runat="server" OnClientFileRenaming="onClientFileRenaming">
</telerik:RadFileExplorer>
```

By following these steps, the file extension will be preserved when renaming files in RadFileExplorer.

## See Also

- [RadFileExplorer Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/fileexplorer/overview)
- [OnClientFileRenaming Event](https://docs.telerik.com/devtools/aspnet-ajax/api/client/RadFileExplorer#events-onclientfilerenaming)
