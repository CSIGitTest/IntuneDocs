---
title: Set up a telecom expense management service in Microsoft Intune |Microsoft Docs
description: Configure the Saaswedo telecom expense management service to integrate with Intune.
keywords: Saaswedo
author: staciebarker
ms.author: stabar
manager: angrobe
ms.date: 12/06/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: b7bf5802-4b65-4aeb-ac99-8e639dd89c2a


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: sumitp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:
---

# Set up Saaswedo telecom expense management service in Microsoft Intune

Intune is partnering with a third-party telecom expense management (TEM) company, [Saaswedo Datalert telecom expense management service](http://www.saaswedo.com/solutions-logicielles/datalert/?lang=en), to let you control telecom data usage for your Intune-managed corporate-owned devices. The service enables you to set and enforce roaming and data usage limits and to send users an alert when they exceed a configured threshold. You can also configure the service to take different actions, such as disabling roaming, when users exceed the threshold. Reports that provide data usage and monitoring information are available in the Datalert console.

Before you can use the Datalert service with Intune, you  need to configure settings in a Datalert console and in Intune. The connection must be turned on for the Datalert service and for Intune. If the Datalert side of the connection is enabled, but not the Intune side, Intune receives the communication, but ignores it.

## Supported platforms

- Samsung Knox
- iOS 7.1 and later

## Prerequisites

- A subscription to Microsoft Intune
- A subscription to the Datalert telecom expense management service

## Configure Intune to work with the Datalert service

1. In the **Configure Devices** workload, choose **Telecom Expense Management** under **Setup**.

2. Under Telecom Expense Management, select Connection status.

3. Select **List of TEM service providers**, and then select your provider from the list shown. A page that is specific to your provider opens. For Saaswedo, the Datalert page opens.

4. On the Datalert page, enter the following: 

    a. Select **Unlock** to enable you to enter the settings on the page.

	b. For **Server MDM**, choose **Microsoft Intune**.

    c. For **Tenant ID**, enter your Intune tenant ID, and select the **Connection** button. Selecting **Connection** makes the Datalert service check in with Intune to ensure that there are no pre-existing Datalert connections with Intune. After a few seconds, a Microsoft log-in page appears, followed by the Datalert Azure authentication.

    d. On the Microsoft authentication page, select **Accept**. You are redirected to a Datalert “thank you” page, which closes after a few seconds. Datalert validates the connection, and displays green check marks beside a list of items that it validated. If the validation fails, you see a message in red. If this happens, contact Datalert Support for help.

The Datalert service is now active, and it begins monitoring data usage and blocking cellular and roaming data on devices that exceed the configured usage limits.

## Turning off the Datalert service

If you disable the Datalert service in the Azure portal:

- -	All of the actions that have been applied to devices, due to past violations of the usage limits, are undone.
- Users are no longer blocked from data access and roaming.
- Intune still receives the signals coming from the service, but ignores them.

**To turn off the service**

1. On the **Telecom Expense Management** blade in the Azure portal, select **Disable**.

2. Select **Save**.

## Viewing data usage and roaming reports

At this time, data usage reporting is available only in Saaswedo’s Datalert console.




















