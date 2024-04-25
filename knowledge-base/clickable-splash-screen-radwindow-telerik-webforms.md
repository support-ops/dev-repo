---
title: Configuring a Clickable Splash Screen with RadWindow in Telerik WebForms
description: Learn how to make a Telerik RadWindow act as a clickable splash screen, including customizations for visibility and appearance.
type: how-to
page_title: Making RadWindow Clickable and Customizing Visibility in WebForms
slug: clickable-splash-screen-radwindow-telerik-webforms
tags: radwindow, webforms, clickable, splash-screen, visibleonpageload, modal, navigateurl, visibletitlebar, visiblestatusbar, custom-skin
res_type: kb
related_questions:
  - How can I make RadWindow clickable?
  - How to use RadWindow as a splash screen?
  - How to hide title bar and status bar in RadWindow?
  - Can I navigate RadWindow to an image?
  - How to apply custom skin to RadWindow?
ticketid: 1581926
---

## Environment

| Product                                 | Version      |
|-----------------------------------------|--------------|
| Progress® Telerik® UI for ASP.NET AJAX | 16.2.22.914 |

## Description

I want to configure the RadWindow as a clickable splash screen. Specifically, I'm looking to display an image within the RadWindow, make the entire window clickable, and customize its appearance by hiding the title and status bars. Additionally, I'm curious if a custom skin is required to modify the appearance of the window's corners when the title bar is not visible.

## Solution

To configure a RadWindow as a clickable splash screen, follow these steps:

1. Define the RadWindow with the desired properties in your ASPX page. Set `VisibleOnPageLoad` to `true` to show the window on page load, and `Modal` to `True` to make it modal. Use `NavigateUrl` to navigate to the image you want to display. Set `VisibleStatusBar` and `VisibleTitleBar` to `False` to hide the status and title bars.

    ```aspx
    <telerik:RadWindow ID="RadWindow1" VisibleOnPageLoad="true" Modal="True" NavigateUrl="~/images/splash.png" runat="server" VisibleStatusBar="False" VisibleTitleBar="False" Width="650" Height="500">  
    </telerik:RadWindow>
    ```

2. To make the entire RadWindow clickable, you can use client-side events. Attach an `OnClientShow` event to the RadWindow and define a JavaScript function to make it clickable.

    ```aspx
    <telerik:RadWindow ID="RadWindow1" OnClientShow="onRadWindowShow" ... >
    </telerik:RadWindow>
    ```

    ```javascript
    function onRadWindowShow(sender, args) {
        var windowElement = sender.get_popupElement();
        windowElement.onclick = function() {
            // Define the action upon clicking the RadWindow
            alert('RadWindow Clicked!');
        };
    }
    ```

3. If the top part of the RadWindow has no corner images after setting `VisibleTitleBar` to `False`, and you wish to alter this appearance, you may need to use a custom skin or apply custom CSS styles. Customizing the RadWindow look entirely might require creating a custom skin. Refer to the Telerik documentation on how to create a custom skin for RadControls: [Creating a Custom Skin](https://docs.telerik.com/devtools/aspnet-ajax/general-information/creating-custom-skins).

    As a simpler alternative, you can apply custom CSS to improve the appearance of the RadWindow corners:

    ```css
    .rwWindowContent {
        border-radius: 10px; /* Adjust the border-radius as needed */
    }
    ```

    Ensure to include your custom CSS after the Telerik styles to override them effectively.

## Notes

- The `NavigateUrl` property of RadWindow can navigate to any webpage, including an image file, making it versatile for different splash screen contents.
- Customizing the appearance of RadWindow through skins or CSS requires some understanding of CSS and possibly the structure of RadWindow's HTML. The Telerik documentation provides extensive guidance on these topics.

## See Also

- [RadWindow Overview](https://docs.telerik.com/devtools/aspnet-ajax/controls/window/overview)
- [RadWindow Client-Side Programming](https://docs.telerik.com/devtools/aspnet-ajax/controls/window/client-side-programming/overview)
- [Creating Custom Skins for RadControls](https://docs.telerik.com/devtools/aspnet-ajax/general-information/creating-custom-skins)
