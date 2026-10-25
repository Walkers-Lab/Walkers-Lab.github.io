---
title: "Add Logon Message via Intune"
date: 2023-07-28 15:43:00 +0100
categories:
  - Intune
tags:
  - Intune
  - Configuration Profile
  - Settings Catalog
  - Windows
excerpt: "Configure a legal notice or welcome message that appears on the Windows login screen using an Intune Settings Catalog profile."
header:
  teaser: /assets/images/add-logon-message-via-intune/08-result.png
---

An interactive logon message is a customizable text message that appears on the Windows login screen before a user enters their credentials. It can be used for legal notices, acceptable use policies, or welcome messages.

In this guide I'll be using an Intune Settings Catalog configuration profile to display a legal notice on the login screen.

## Getting Started

Log in to [Microsoft Intune](https://intune.microsoft.com/) and navigate to **Devices > Configuration Profiles > Create profile**.

![Create profile](/assets/images/add-logon-message-via-intune/01-create-profile.png)

## Create the Profile

After clicking **Create profile**, choose the platform and profile type:

- **Platform:** Windows 10 and later
- **Profile type:** Settings catalog

Then click **Create**.

![Select platform and profile type](/assets/images/add-logon-message-via-intune/02-platform-profile-type.png)

Give the profile a **Name** and **Description**, then click **Next**.

![Name and description](/assets/images/add-logon-message-via-intune/03-name-description.png)

## Add the Settings

Click **Add settings**. In the search box enter **logon** and select **Local Policies Security Options**. From the results, enable both:

- **Interactive Logon Message Text for Users Attempting to Logon**
- **Interactive Logon Message Title for Users Attempting to Logon**

![Add settings](/assets/images/add-logon-message-via-intune/04-add-settings.png)

Enter the message body and title you want displayed on the login screen, then click **Next**.

![Message text and title](/assets/images/add-logon-message-via-intune/05-message-text.png)

You can skip the Scope tags page.

## Assign the Profile

On the Assignments page, choose who receives this policy. Selecting **All Devices** applies it to every Intune-enrolled device. Alternatively, target a specific user or device group to limit the scope.

Click **Next** once you've made your selection.

![Assignments](/assets/images/add-logon-message-via-intune/06-assignments.png)

## Create and Deploy

Review your settings and click **Create**.

![Create profile](/assets/images/add-logon-message-via-intune/07-create.png)

The policy will be applied the next time each targeted device checks in with Intune and reboots.

## Result

After the device restarts, the logon message will appear on the lock screen before the user can sign in.

![Logon message on lock screen](/assets/images/add-logon-message-via-intune/08-result.png)
