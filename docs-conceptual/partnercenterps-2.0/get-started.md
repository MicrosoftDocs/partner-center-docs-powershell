---
title: Get started with Partner Center PowerShell
description: Learn how to get started with Partner Center PowerShell.
ms.topic: get-started-article
ms.date: 09/09/2019
---

# Get started with Partner Center PowerShell

Azure PowerShell is designed for managing and administering Azure resources from the command line. Use Azure PowerShell when you want to build automated tools that use the Azure Resource Manager model. Try it out in your browser with [Azure Cloud Shell](/azure/cloud-shell/overview), or install on your local machine.

This article helps you get started with Azure PowerShell and teaches the core concepts behind it.

## Install or run in Azure Cloud Shell

The easiest way to get started with Azure PowerShell is by trying it out in an Azure Cloud Shell environment.
To get up and running with Cloud Shell, see [Quickstart for PowerShell in Azure Cloud Shell](/azure/cloud-shell/quickstart-powershell).
Cloud Shell runs PowerShell 6 on a Linux container, so Windows-specific functionality isn't available.

When you're ready to install Azure PowerShell on your local machine, follow the instructions in [Install the Azure PowerShell module](install.md).

## Sign in to Partner Center

Sign in interactively with the `Connect-PartnerCenter` cmdlet. Skip this step if you use Cloud Shell: Your Azure Cloud Shell session is already authenticated
for the environment, subscription, and tenant that launched the Cloud Shell session.

```azurepowershell-interactive
Connect-PartnerCenter
```

If you're in a non-US region, use the `-Environment` parameter to sign in. Get the name of the environment for your region by using
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
* [Get help from the community](https://stackoverflow.com/questions/tagged/partnercenter)
