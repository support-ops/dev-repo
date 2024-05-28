---
title: Enabling Specific Row in RadGrid Upon Button Click
description: Learn how to enable a specific row in a RadGrid upon clicking a button, while disabling the rest of the rows.
type: how-to
page_title: Enabling Specific Row in RadGrid and Disabling Others
slug: enabling-specific-row-radgrid-disabling-others
tags: radscheduler, asp.net ajax, radgrid, button, enable, disable
res_type: kb

## Environment

| Product | RadScheduler for ASP.NET AJAX 2022.2.622 |

## Description

I have a RadGrid with "Start" and "End" button columns. I want to enable only the row where the "Start" button is clicked and disable the rest of the rows.

This KB article also answers the following questions:
- How to enable a specific row in RadGrid?
- How to disable other rows when one row is enabled in RadGrid?
- How to use button columns in RadGrid for row-specific actions?

## Solution

To achieve this, use the following steps:

1. **Add JavaScript to Handle Button Clicks:**

```javascript
function onStartButtonClick(sender, eventArgs) {
    var grid = $find("<%= RadGrid1.ClientID %>");
    var masterTable = grid.get_masterTableView();
    var rows = masterTable.get_dataItems();

    for (var i = 0; i < rows.length; i++) {
        var row = rows[i].get_element();
        var button = rows[i].findElement("StartButton");
        
        if (button === sender) {
            // Enable the clicked row
            row.style.backgroundColor = "";
            row.disabled = false;
        } else {
            // Disable other rows
            row.style.backgroundColor = "#d3d3d3";
            row.disabled = true;
        }
    }
}
```

2. **Define RadGrid with Button Columns:**

```html
<telerik:RadGrid ID="RadGrid1" runat="server" AutoGenerateColumns="False">
    <MasterTableView>
        <Columns>
            <telerik:GridBoundColumn DataField="ID" HeaderText="ID" />
            <telerik:GridBoundColumn DataField="Name" HeaderText="Name" />
            <telerik:GridButtonColumn UniqueName="StartButton" Text="Start" CommandName="Start" ButtonType="PushButton" />
            <telerik:GridButtonColumn UniqueName="EndButton" Text="End" CommandName="End" ButtonType="PushButton" />
        </Columns>
    </MasterTableView>
</telerik:RadGrid>
```

3. **Attach JavaScript Function to Button Click Events:**

```html
<script type="text/javascript">
    function pageLoad() {
        var grid = $find("<%= RadGrid1.ClientID %>");
        var rows = grid.get_masterTableView().get_dataItems();

        for (var i = 0; i < rows.length; i++) {
            var startButton = rows[i].findElement("StartButton");
            startButton.onclick = function (e) {
                onStartButtonClick(this, e);
            };
        }
    }
</script>
```

By following these steps, you can ensure that only the row with the clicked "Start" button is enabled while all other rows are disabled.

## See Also

- [RadScheduler Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/scheduler/overview)
- [RadGrid Documentation](https://docs.telerik.com/devtools/aspnet-ajax/controls/grid/overview)
