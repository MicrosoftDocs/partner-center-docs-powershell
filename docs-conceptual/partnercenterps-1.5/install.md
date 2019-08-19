---
title: Install Partner Center PowerShell with PowerShellGet
description: How to install Partner Center PowerShell with PowerShellGet
ms.topic: conceptual
ms.date: 08/18/2019
---

# Partner Center PowerShell

The Partner Center PowerShell module contains a set of PowerShell commands for administrators and developers to manage Cloud Solution Provider program resources. Using this module you can perform tasks such as customer and subscription life cycle management, confirm customer acceptance of the Microsoft Cloud Agreement, and purchase reserved instances.

## Requirements

Partner Center PowerShell works with PowerShell 5.1 or higher on Windows, or PowerShell Core 6.x and later on
all platforms. If you aren't sure if you have PowerShell, or are on macOS or Linux,
[install the latest version of PowerShell Core](/powershell/scripting/install/installing-powershell#powershell-core).

To check your PowerShell version, run the command:

```powershell-interactive
$PSVersionTable.PSVersion
```

To run Partner Center PowerShell in PowerShell 5.1 on Windows:

1. Update to [Windows PowerShell 5.1](/powershell/scripting/install/installing-windows-powershell#upgrading-existing-windows-powershell) if needed. If you're on Windows 10, you already
  have PowerShell 5.1 installed.
2. Install [.NET Framework 4.6.1 or later](/dotnet/framework/install).

There are no additional requirements for Partner Center PowerShell when using PowerShell Core.

## Install the Partner Center PowerShell module

The recommended install method is to only install for the active user:

```powershell-interactive
# PowerShell 5.1
Install-Module -Name PartnerCenter -AllowClobber -Scope CurrentUser

# PowerShell Core
Install-Module -Name PartnerCenter.NetCore -AllowClobber -Scope CurrentUser
```

If you want to install for all users on a system, this requires administrator privileges. From an elevated PowerShell session either
run as administrator or with the `sudo` command on macOS or Linux:

```powershell-interactive
# PowerShell 5.1
Install-Module -Name PartnerCenter -AllowClobber -Scope AllUsers

# PowerShell Core
Install-Module -Name PartnerCenter.NetCore -AllowClobber -Scope AllUsers
```

By default, the PowerShell gallery isn't configured as a trusted repository for PowerShellGet. The first time you use the PSGallery you see the following prompt:

```output
Untrusted repository

You are installing the modules from an untrusted repository. If you trust this repository, change
its InstallationPolicy value by running the Set-PSRepository cmdlet.

Are you sure you want to install the modules from 'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

Answer `Yes` or `Yes to All` to continue with the installation.

## Troubleshooting

Here are some common problems seen when installing the Partner Center PowerShell module. If you experience a problem not listed here,
please [file an issue on GitHub](https://github.com/microsoft/partner-center-powershell/issues).

## Provide feedback

If you find a bug in Partner Center Powershell or have feedback, [file an issue on GitHub](https://github.com/microsoft/partner-center-powersehll/issues).
