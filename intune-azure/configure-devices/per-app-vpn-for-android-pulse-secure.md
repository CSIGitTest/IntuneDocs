---
# required metadata

title: Intune custom per-app VPN profile for Android using Pulse Secure | Intune Azure preview | Microsoft Docs
description: "Intune Azure preview: Learn how to create a per-app VPN profile for Android devices managed by Intune."
keywords:
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chrisbal
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Use an Intune custom profile to create a per-app VPN profile for Android devices

You can create a per-app VPN profile for Android 5.0 and later devices that are managed by Intune. First, create a VPN profile that uses the Pulse Secure connection type. Then, create a custom configuration policy that associates the VPN profile with specific apps. 

After you deploy the policy to your Android device or user groups, users should start the PulseSecure VPN. PulseSecure will then allow traffic only from the specified apps to use the open VPN connection.

> [!NOTE]
>
> Only the Pulse Secure connection type is supported for this profile.


## Step 1: Create a VPN profile

1. In the **Device Configuration** workload, choose **Manage** > **Profiles**.
2. On the list of profiles blade, choose **Create Profile**.
3. On the **Create Profile** blade, enter a **Name** and optional **Description** for the VPN profile.
4. From the **Platform** drop-down list, choose **Android**.
5. From the **Profile type** drop-down list, choose **VPN**.
3. Choose **Settings** > **Configure** and then configure the VPN profile as per the settings in [How to configure VPN settings](how-to-configure-vpn-settings.md) and [Intune VPN settings for Android devices](vpn-for-android.md).

Take note of the VPN profile name to use in the next step. For example, **MyAppVpnProfile**.

## Step 2: Create a custom configuration policy

1. In the Azure Portal, select the **Device Configurations** workload.
2. On the **Device configuration** blade, select **Manage** > **Profiles**.
3. On the profiles blade, click **Create Profile**.
4. On the **Create Profile** blade, enter a **Name** and **Description** for the custom profile.
5. From the **Platform** drop-down list, choose **Android**.
6. From the **Profile type** drop-down list, choose **Custom**.
7. Choose **Settings** > **Configure**.
3. On the **Custom OMA-URI Settings** blade, choose **Add**.
	- Enter a setting name.
	- For **Data type**, specify **String**.
	- For **OMA-URI**, specify this string: **./Vendor/MSFT/VPN/Profile/*Name*/PackageList**, where *Name* is the VPN profile name you noted in Step 1. In this example, the string would be **./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList**.
	- For **Value**, create a semicolon-separated list of packages to associate with the profile. For example, if you want Excel and the Google Chrome browser to use the VPN connection, enter **com.microsoft.office.excel;com.android.chrome**.

![Example Android per-app VPN custom policy](./media/android_per_app_vpn_oma_uri.png)

### Set your app list to blacklist or whitelist (optional)
  You can specify a list of apps that *cannot* use the VPN connection by using the **BLACKLIST** value. All other apps will connect through the VPN.
  Alternatively, you can use the **WHITELIST** value to specify a list of apps that *can* use the VPN connection. Apps that are not on the list will not connect through the VPN.
  1.	On the **Custom OMA-URI Settings** blade, choose **Add**.
  2.	Enter a setting name.
  3.	For **Data type**, specify **String**.
  4.	For **OMA-URI**, use this string: **./Vendor/MSFT/VPN/Profile/*Name*/Mode**, where *Name* is the VPN profile name you noted in Step 1. In our example, the string would be **./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode**.
  5.	For **Value**, enter **BLACKLIST** or **WHITELIST**.



## Step 3: Assign both policies

Use the instructions in [How to assign device profiles](how-to-assign-device-profiles.md) to assign both profiles to the required users or devices.
