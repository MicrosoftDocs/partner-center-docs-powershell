---
title: Release notes for Partner Center PowerShell
description: Discover what has changed with Partner Center PowerShell with each release.
ms.topic: conceptual
ms.date: 09/09/2019
---

# Release notes

## 2.0.1909.1 - September 2019

* Agreements
  * Added the [Get-PartnerAgreementTemplate](/powershell/module/partnercenter/Get-PartnerAgreementTemplate) command to provide access to the links download or view the Microsoft Customer Agreement
  * Added the ability to request the Microsoft Customer Agreement template metadata
  * The *AgreementType* enumeration has been removed, and where it was used the type has changed to a *string*
* Authentication
  * Added the ability to invoke [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) without requiring the creation of an Azure Active Directory application
  * Enabled interactive login support for cross-platform by default
  * Device code flow login is now the backup option of interactive login fails, or the user provides the `-UseDeviceAuthentication` switch parameter
  * Token cache is now shared with other products, such as Azure CLI and Visual Studio 2019
* Module
  * The `PartnerCenter` module now supports PowerShell 5.1 and PowerShell, as a result the `PartnerCenter.NetCore` module will be retired
* Subscriptions
  * Added the [New-PartnerCustomerSubscriptionActivation](/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionActivation) command to make it where third-party subscriptions can be activated in the integration sandbox
