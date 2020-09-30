---
title: Slow logon with a blank screen
description: Describes an issue that makes Windows logon slow, with a blank screen displayed during the delay. Occurs in Windows 7 and Windows 8.1 environments. A workaround is provided.
ms.date: 09/08/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-client
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Slow logon
ms.technology: UserProfilesAndLogon
---
# Slow logon with a blank screen in Windows 7 or Windows 8.1

This article provides a workaround for an issue that makes Windows logon slow, with a blank screen displayed during the delay.

_Original product version:_ &nbsp; Windows 10 - all editions  
_Original KB number:_ &nbsp; 3161390

## Summary

In Windows 7 or Windows 8.1, Remote Desktop and console users experience a slow logon with a blank screen before the desktop is rendered. Longer logon times directly correspond to the number of desktop shortcuts that are defined in the user's profile.

## Symptoms

In this situation, you might notice that the logon times increase continually. A blank screen may be displayed during this delay period. You may also notice that Explorer.exe consumes excessive CPU resources.

Additionally, Procmon shows that affected computers are busy accessing the following registry key:

`HKEY_USERS\S-1-5-21-xxxxxxx\Software\Microsoft\Windows\CurrentVersion\UFH\SHC`
(or `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\UFH\SHC`)

You may also notice frequent changes or additions to shortcuts on the desktop. This might occur if you use a logon script to update the desktop or in a Remote Desktop situation in which the cached profile is deleted. This makes all entries new on the next logon.

## Workaround

To work around this issue, configure a logon script to delete the following registry key during logon:

`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\UFH\SHC`

You can also use Group Policy preferences to work around this issue.

> [!NOTE]
> There's a known issue when you use this workaround. As soon as the script is in place, users will see entries on the Start menu marked as "new" even though there aren't any newly installed applications or items. It might be a good idea to share this information with users to prevent them from logging a call with the Service Desk about this.