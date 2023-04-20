---
title: Breaking changes for Partner Center PowerShell
description: Learn about the breaking changes for Partner Center PowerShell.
ms.topic: conceptual
ms.date: 09/24/2019
---

# Breaking changes

## Release 2.0.19101 - October 2019

* Usage
  * Removed the `Get-PartnerCustomerSubscriptionUsage` command due to changes with the Partner Center SDK for .NET. This command will be replaced with the [Get-PartnerCustomerSubscriptionMeterUsage](/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionMeterUsage) and [Get-PartnerCustomerSubscriptionResourceUsage](/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionResourceUsage) commands

## Release 2.0.1909.1 - September 2019

* Authentication
  * Environments have been renamed to match the Azure PowerShell module. The new values are: *AzureChinaCloud*, *AzureCloud*, *AzureGermanCloud*, *AzurePPE*, and *AzureUSGovernment*
  * Replaced the `Consent` parameter with the `UseAuthorizationCode` parameter for the `New-PartnerAccessToken` cmdlet
  * Replaced the `Resource` parameter with the `Scopes` parameter for the `Connect-PartnerCenter` and `New-PartnerAccessToken` cmdlets
  * ServicePrincipal parameter is now required when using a confidential client with the `Connect-PartnerCenter` and `New-PartnerAccessToken` cmdlets
  * When using the [New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken) command and the `UseAuthorizationCode` parameter you will be prompted to authentication interactively using the authorization code flow. The redirect URI value will generated dynamically. This generation process will attempt to find a port between 8400 and 8999 that is not in use. Once an available port has been found, the redirect URL value will be constructed (e.g. `http`://localhost:8400`). So, it is important that you have configured the redirect URI value for your Azure Active Directory application accordingly.
* Module
  * The `PartnerCenter` module now supports PowerShell 5.1 and PowerShell, as a result the `PartnerCenter.NetCore` module will be retired
