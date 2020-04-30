---
title: Get started with Partner Center PowerShell
description: Learn how to get started with Partner Center PowerShell.
ms.date: 12/05/2019
---

# Get started with Partner Center PowerShell

Partner Center PowerShell is designed for administering and managing Partner Center resources from the command line. This article helps you get started with Partner Center PowerShell and teaches the core concepts behind it.

## Install

When you are ready to install Partner Center PowerShell on your local machine, follow the instructions in [Install the Partner Center PowerShell module](install.md).

## Sign in to Partner Center

Sign in interactively with the `Connect-PartnerCenter` cmdlet.

```azurepowershell-interactive
Connect-PartnerCenter
```

If you are in a non-US region, use the `-Environment` parameter to sign in. Get the name of the environment for your region by using
the [Get-PartnerEnvironment](/powershell/module/partnercenter/Get-PartnerEnvironment) cmdlet. For example, to sign in to Azure China 21Vianet:

```azurepowershell-interactive
Connect-PartnerCenter -Environment AzureChinaCloud
```

When you run this cmdlet it will open a browser where you will be able to authenticate. If the system you are using to connect does not a browser, then you will be provided a code. To authenticate, copy this code and paste it into <https://microsoft.com/devicelogin> in a browser.

Once signed in, use the Partner Center PowerShell cmdlets to access and manage resources. To learn more about the sign-in process and authentication methods, see [Sign in with Partner Center PowerShell](authenticate.md).

## Find commands

Partner Center PowerShell cmdlets follow a standard naming convention for PowerShell, `VERB-NOUN`. The verb describes the action (examples include `New`, `Get`, `Set`, `Remove`) and the noun describes the resource type (examples include `PartnerAgreementTemplate`, `PartnerAzureRateCard`, `PartnerCustomer`). Nouns in Partner Center PowerShell always start with the prefix `Partner`. For the full list of standard verbs, see [Approved verbs for PowerShell Commands](/powershell/developer/cmdlet/approved-verbs-for-windows-powershell-commands).

You can use the [Get-Command](/powershell/module/microsoft.powershell.core/get-command) cmdlet to help find the nouns and verbs available. As an example, to find all Customer commands that use the `Get` verb you would use the following

```powershell-interactive
Get-Command -Verb Get -Noun PartnerCustomer*
```

## Next steps

* [Sign in with Partner Center PowerShell](authenticate.md)
* [Get help from the community](https://stackoverflow.com/questions/tagged/partner+center)
