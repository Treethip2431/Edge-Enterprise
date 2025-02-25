---
title: "Local site list for Internet Explorer (IE) mode"
ms.author: shisub
author: dan-wesley
manager: srugh
ms.date: 03/01/2022
audience: ITPro
ms.topic: conceptual
ms.prod: microsoft-edge
ms.localizationpriority: medium
ms.collection: M365-modern-desktop
description: "Learn how to enable local site lists and easy access to IE mode"
---

# Configure local site list for Internet Explorer (IE) mode

>[!Note]
> The Internet Explorer 11 desktop application will be retired and go out of support on June 15, 2022 (for a list of what’s in scope, see the [Internet Explorer 11 desktop app retirement FAQ](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/internet-explorer-11-desktop-app-retirement-faq/ba-p/2366549)). The same IE11 apps and sites you use today can open in Microsoft Edge with Internet Explorer mode. To learn more, see [The future of Internet Explorer on Windows 10 is in Microsoft Edge](https://blogs.windows.com/windowsexperience/2021/05/19/the-future-of-internet-explorer-on-windows-10-is-in-microsoft-edge/).

This article explains how to configure easy access to Internet Explorer mode (IE mode) and allow the use of local site lists in your organization.

> [!NOTE]
> This article applies to Microsoft Edge version 92 or later.

## Prerequisites

1. Windows updates

   - Windows 11
   - Windows 10, version 1909 - [KB5003698](https://support.microsoft.com/topic/june-15-2021-kb5003698-os-build-18363-1645-preview-1ecf117e-1f89-40f9-a0a5-ed5766737620) or later  

   - Windows 10, version 2004; Windows 10, version 20H2 and Windows 10, version 21H1 – [KB5003690](https://support.microsoft.com/topic/june-21-2021-kb5003690-os-builds-19041-1081-19042-1081-and-19043-1081-preview-11a7581f-2a01-47d5-ba12-431709ee2248) or later

2. Microsoft Edge version 92 (92.0.902.55 or later)

> [!IMPORTANT]
> This local site list feature isn't supported on Windows Server 2016 at this time.

## Overview

IE mode is powered by the configuration of the Enterprise Mode Site List. While you are identifying and configuring sites on the site list to use IE mode, your users no longer need to wait or fall back to the standalone IE11 application.

Starting with Microsoft Edge version 92, repeated access to *unconfigured* IE mode sites is easier. Users can reload sites in IE mode. They can add these sites to their local site list to automatically render in IE mode for 30 days, while the organization’s site list gets updated. When [IE11 is disabled](/deployedge/edge-ie-disable-ie11) in your environment, your users are no longer solely dependent on the organization’s site list.

You can configure this experience through group policies for your organization.

> [!NOTE]
> An *unconfigured* site is one that requires IE mode but isn't configured to open in IE mode in the Enterprise Mode Site List.

## Enable the local site list experience

To enable the local site list experience, users can go to the URL *edge://settings/defaultBrowser* and set **Allow sites to be reloaded in Internet Explorer mode** to **Allow**.

:::image type="content" source="media/Edge-hybrid-IE-mode/internet-explorer-compatibilitiy.png" alt-text="Internet Explorer Compatibility":::

>[!Note]  
>
>1. If you have enabled IE mode testing through the *InternetExplorerIntegrationTestingAllowed* policy, you will see this setting, but it will be greyed out unless you  explicitly enable the *InternetExplorerIntegrationReloadInIEModeAllowed* policy.
>
>2. If **Allow sites to be reloaded in Internet Explorer mode** is set to **Default**, users might be able to reload sites in IE mode if they have existing Internet Explorer 11 usage.  

When this setting is enabled, users can reload a site in IE mode by selecting **Settings and more (the ellipses icon ...) > Reload in Internet Explorer mode**. Users can also select **Reload tab in Internet Explorer mode** when they right-click on a tab or choose **Open link in new Internet Explorer mode tab** when they right-click on a link.

:::image type="content" source="media/Edge-hybrid-IE-mode/reload-in-internet-exploror-mode-screenshot.png" alt-text="Reload in internet Explorer Mode":::

The **Reload in Internet Explorer mode** icon can be pinned to the toolbar. The toolbar button allows users to easily enter and exit IE mode and can be managed through the *edge://settings/appearance* URL.

:::image type="content" source="media/Edge-hybrid-IE-mode/reload-in-internet-exploror-mode-icon-screenshot.png" alt-text="Reload in internet Explorer Mode icon":::

>[!Note]
>If the user is on a site that’s already in the organization’s Enterprise Mode Site List, options to Reload in (or Exit) Internet Explorer mode will be visible but greyed out.

When the option is selected, the site reloads in IE mode. The IE mode indicator icon is visible to the left of the address bar and the flyout shows an option that users can toggle to Open the page in Internet Explorer mode next time. This adds the specific page the user is on to the local site list and will automatically open in IE mode for the next 30 days.

:::image type="content" source="media/Edge-hybrid-IE-mode/site-has-been-reloaded-in-ie-mode-screenshot.png" alt-text="This page is open in internet Explorer Mode":::

After a site has been reloaded in IE mode, "in-page" navigation will stay in IE mode (for example, a link, script, a form on the page, or a server-side redirect from another "in-page" navigation).  

While in IE mode, users will see a banner indicating they are in IE mode, the option to Leave IE mode and to pin the IE mode icon to the toolbar (if it isn’t pinned already).

:::image type="content" source="media/Edge-hybrid-IE-mode/ie-mode-banner-screenshot.png" alt-text="IE Mode Banner":::

Users can choose to exit from IE mode using the Leave button on the banner, the pinned IE mode icon or **Settings and more (the ellipses icon ...) > Exit Internet Explorer mode**, otherwise Microsoft Edge will automatically exit from IE mode when a navigation that isn't "in-page" occurs (for example, using the address bar, the back button, or a favorite link).

Entries remain on the local site list for a default period of 30 days. We recommend you configure legacy sites for your organization in the Enterprise Mode Site List. The local site list will ensure that users can continue their workflow without being interrupted while the organization’s site list gets updated. On day 31, when users navigate to the site, they will see a banner explaining that the site will no longer load in IE mode. Users can add it back to the local site list if they so choose.

:::image type="content" source="media/Edge-hybrid-IE-mode/page-will-no-longer-load-in-ie-mode-screenshot.png" alt-text="Page will no longer load in IE mode":::

## Policies to configure the use of local site lists for IE mode

Two group policies are available to configure the local site list experience in Microsoft Edge. These policies are:

### Policy: InternetExplorerIntegrationReloadInIEModeAllowed

This policy corresponds to the Microsoft Edge setting “Allow sites to be reloaded in Internet Explorer mode”. You can access this setting by going to the *edge://settings/defaultbrowser* URL.

- If you enable this policy, users can reload a site in IE mode by selecting **Settings and more (the ellipses icon ... > Reload in Internet Explorer mode**. Users can also select **Reload tab in Internet Explorer mode** when they right-click on a tab, or choose **Open link in new Internet Explorer mode tab** when they right click on a link.
Users can optionally tell Microsoft Edge to use IE mode for the site in the future. This choice will be remembered for a default of 30 days and can be managed using the policy *InternetExplorerIntegrationLocalSiteListExpirationDays*.

- If you disable this policy, users will not be allowed to reload an unconfigured site in IE mode.

- If you don’t configure this policy, we will show users options to reload unconfigured sites in IE mode depending on recent Internet Explorer 11 usage.

Note that this policy takes precedence over how you configured the [InternetExplorerIntegrationTestingAllowed](/deployedge/microsoft-edge-policies#internetexplorerintegrationtestingallowed) policy and that policy will be disabled.

### Policy: InternetExplorerIntegrationLocalSiteListExpirationDays

This policy can be used to adjust the number of days that a site remains on the local site list for users.  

- If you disable or don’t configure this policy, a default value of 30 days is used.

- If you enable the policy, you must enter a value between 0-90 days to keep the site on a user’s local site list.

This policy has no effect if you disabled the *InternetExplorerIntegrationReloadInIEModeAllowed* policy.

> [!NOTE]
> The local site list currently doesn't sync across devices. This improvement is currently in our backlog and we’ll update this feature when it's available.

## See Also

- Disable Internet Explorer 11 - [Disable Internet Explorer 11](/deployedge/edge-ie-disable-ie11)
- Configure IE mode policies - [Configure IE mode Policies](/deployedge/edge-ie-mode-policies)
