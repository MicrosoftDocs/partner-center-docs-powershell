---
title: Release notes for Partner Center PowerShell
description: Discover what has changed with Partner Center PowerShell with each release.
ms.topic: conceptual
ms.date: 09/14/2019
---

# Release notes

## 2.0.1909.3 - September 2019

* Authentication
  * Address issue [#156](https://github.com/microsoft/Partner-Center-PowerShell/issues/156) where the refresh token was not being returned if it had not been previously used by the module during an interactive authentication attempt
  * After successfully authenticating the module will attempt to get country and locale based on the partner organization profile

## 2.0.1909.2 - September 2019

* Authentication
  * Addressed issue [#153](https://github.com/microsoft/Partner-Center-PowerShell/issues/153) that was preventing the [New-PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/New-PartnerAccessToken) command from working as expected.
* Dependencies
  * Updated the version of Microsoft.Rest.ClientRuntime to the latest.

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
