---
title: Configuring EditMode for MasterTableView in Telerik Reporting
description: Learn how to set the EditMode property of the MasterTableView to InPlace in Telerik Reporting.
type: how-to
page_title: How to Set MasterTableView EditMode to InPlace in Telerik Reporting
slug: configure-editmode-mastertableview-telerik-reporting
tags: progress, telerik, reporting, mastertableview, editmode, inplace
res_type: kb
related_questions:
  - How to change EditMode of MasterTableView in Telerik Reporting?
  - What is InPlace EditMode in Telerik Reporting?
  - How to configure MasterTableView properties in Telerik Reporting?
  - Steps to set MasterTableView EditMode to InPlace
  - How to customize EditMode in Telerik Reporting?
ticketid: 1600927
---

## Environment

| Product | Version        |
| ------- | -------------- |
| Progress® Telerik® Reporting | 17.0.23.118 |

## Description

When working with Telerik Reporting, it's essential to control the editing behavior of tables. One way to manage this is by setting the `EditMode` of the `MasterTableView` to `InPlace`. This configuration enables inline editing of table records, providing a streamlined experience.

## Solution

To set the `EditMode` of the `MasterTableView` to `InPlace`, follow these steps:

1. Open the ASPX page where the Telerik Report Viewer or the report's `MasterTableView` is defined.
2. Locate the `<MasterTableView>` tag within your report's markup.
3. Set the `EditMode` attribute of the `<MasterTableView>` tag to `"InPlace"`. 

The resulting markup will look like this:

```aspx
<MasterTableView EditMode="InPlace" >
```

By setting the `EditMode` to `InPlace`, you enable inline editing for the table, allowing users to edit records directly within the table view.

## Notes

- Ensure that the Telerik Reporting version you are using supports the `EditMode` property as described.
- This configuration is specific to the `MasterTableView` in Telerik Reporting. It may not apply to other components or table views outside of this context.

## See Also

- [Telerik Reporting Documentation](https://docs.telerik.com/reporting/)
- [MasterTableView Overview](https://docs.telerik.com/reporting/mastertableview)
- [Configuring Table Views in Telerik Reporting](https://docs.telerik.com/reporting/table/crosstab-list/configuring-table)
