---
title: Breaking changes for Partner Center PowerShell
description: Learn about the breaking changes for Partner Center PowerShell.
ms.topic: conceptual
ms.date: 09/12/2019
---

# Breaking changes

## Release 2.0 - September 2019

* Authentication
  * Environments have been renamed to match the Azure PowerShell module. The new values are: *AzureChinaCloud*, *AzureCloud*, *AzureGermanCloud*, *AzurePPE*, and *AzureUSGovernment*
  * Replaced the `Consent` parameter with the `UseAuthorizationCode` parameter for the `New-PartnerAccessToken` cmdlet
  * Replaced the `Resource` parameter with the `Scopes` parameter for the `Connect-PartnerCenter` and `New-PartnerAccessToken` cmdlets
  * ServicePrincipal parameter is now required when using a confidential client with the `Connect-PartnerCenter` and `New-PartnerAccessToken` cmdlets
* Module
  * The `PartnerCenter` module now supports PowerShell 5.1 and PowerShell, as a result the `PartnerCenter.NetCore` module will be retired
