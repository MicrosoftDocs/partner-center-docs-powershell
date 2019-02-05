---
title:  Partner Center PowerShell | Microsoft Docs
description: How to install the Partner Center PowerShell module.
services: partner-center
documentationcenter: ''
author: iswillia
manager: jegraves
editor: ''

ms.service: partner-center
ms.workload: partner-center
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.custom: posh-docs-conceptual
ms.topic: hero-article
ms.date: 10/25/2018
ms.author: iswillia
---

# Partner Center PowerShell

The Partner Center PowerShell module contains a set of PowerShell commands for administrators and developers to manage Cloud Solution Provider program resources. Using this module you can perform tasks such as customer and subscription life cycle management, confirm customer acceptance of the Microsoft Cloud Agreement, and purchase reserved instances.

## Installation

Run the following command in an elevated PowerShell session to install the Partner Center module:

```powershell
Install-Module -Name PartnerCenter
```

If you have an earlier version of the Partner Center PowerShell modules installed from the PowerShell Gallery and would like to update to the latest version, run the following commands from an elevated PowerShell session.

**Note:** `Update-Module` installs the new version, however, it does not remove the old version.

```powershell
# Install the latest version of the Partner Center PowerShell module
Update-Module -Name PartnerCenter
```