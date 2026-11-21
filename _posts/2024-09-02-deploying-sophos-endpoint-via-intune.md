---
title: "Deploying Sophos Endpoint via Intune"
date: 2024-09-02 22:42:00 +0100
categories:
  - Intune
tags:
  - Intune
  - Sophos
  - Endpoint Security
  - Win32 App
  - Autopilot
excerpt: "Step-by-step guide to packaging the Sophos Endpoint installer as a Win32 app and deploying it to Windows devices via Microsoft Intune."
header:
  teaser: /assets/images/deploying-sophos-endpoint-via-intune/teaser.png
---

This guide walks through deploying Sophos Endpoint to Windows devices via Microsoft Intune as a Win32 app. Using Win32 delivery gives you full control over install and uninstall commands, detection rules, and assignment targeting.

## Prerequisites

- Access to Sophos Central with admin rights
- Microsoft Intune admin access
- [Microsoft Win32 Content Prep Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool) (`IntuneWinAppUtil.exe`)

For this guide I am using the following folder structure:

```text
Intune App Creator\
├── IntuneWinAppUtil.exe
├── source\
│   └── Sophos Endpoint\     ← installer goes here
└── output\
    └── Sophos Endpoint\     ← .intunewin file goes here
```

## Step 1 — Download the Sophos installer

Sign in to [Sophos Central](https://central.sophos.com/), navigate to **Devices > Installers**, then click **Download Complete Windows Installer**.

Save `SophosSetup.exe` into your source folder:
`C:\Intune App Creator\source\Sophos Endpoint\SophosSetup.exe`

## Step 2 — Package as a Win32 app

Run `IntuneWinAppUtil.exe` as Administrator and enter the following when prompted:

| Prompt | Value |
|---|---|
| Source folder | `C:\Intune App Creator\source\Sophos Endpoint` |
| Setup file | `C:\Intune App Creator\source\Sophos Endpoint\SophosSetup.exe` |
| Output folder | `C:\Intune App Creator\output\Sophos Endpoint` |
| Catalog folder | `N` |

The tool will produce `SophosSetup.intunewin` in your output folder.

## Step 3 — Add the app in Intune

Sign in to the [Intune Admin Centre](https://intune.microsoft.com/) and navigate to **Apps > All apps > Add**.

Select **Windows app (Win32)** from the app type dropdown, then click **Select**.

Click **Select app package file**, browse to `SophosSetup.intunewin`, and click **OK**, then **Next**.

## Step 4 — Fill in app information

| Field | Value |
|---|---|
| Name | Sophos Central |
| Description | Advanced endpoint protection with centralised management via Sophos Central. |
| Publisher | Sophos Ltd |
| Privacy URL | `https://soph.so/oclS8c` |

Click **Next**.

## Step 5 — Set install and uninstall commands

| Field | Value |
|---|---|
| Install command | `SophosSetup.exe --quiet` |
| Uninstall command | `%ProgramFiles%\Sophos\Sophos Endpoint Agent\uninstallcli.exe` |

Leave all other settings as default and click **Next**.

## Step 6 — Requirements

Set the **Operating system architecture** and **Minimum operating system** to match your environment, then click **Next**.

## Step 7 — Detection rules

Select **Manually configure detection rules**, then click **Add** and fill in:

| Field | Value |
|---|---|
| Rule type | File |
| Path | `%ProgramFiles%\Sophos\Sophos UI` |
| File or folder | `Sophos UI.exe` |
| Detection method | File or folder exists |
| Associated with a 32-bit app on 64-bit clients | No |

Click **OK**, then **Next**. Skip the Dependencies and Supersedence pages.

## Step 8 — Assignments

Under **Required**, click **Add group** or **Add all devices** to target your deployment, then click **Next** and **Create**.

## Verifying the deployment

To confirm a device has received and installed Sophos, navigate to **Devices > All devices**, select the device, then go to **Managed apps**. The status should show as **Installed**.

You can also cross-reference in Sophos Central under **Devices** — the device should appear with a healthy status once the agent has checked in.
