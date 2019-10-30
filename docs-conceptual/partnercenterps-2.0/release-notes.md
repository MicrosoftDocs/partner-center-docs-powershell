---
title: Release notes for Partner Center PowerShell
description: Discover what has changed with Partner Center PowerShell with each release.
ms.topic: conceptual
ms.date: 10/15/2019
---

# Release notes

## 2.0.1911.1 - November 2019

* Authentication
  * Addressed issue preventing CTRL+C from interrupting the waiting for a response during the interactive authentication scenario
* Invoicing
  * [Daily Rated Usage Line Item](https://github.com/microsoft/Partner-Center-PowerShell/blob/master/src/PowerShell/Models/Invoices/PSDailyRatedUsageLineItem.cs)
    * Added the *EntitlementId*, *EntitlementDescription*, *PCToBCExchangeRate*, *PCToBCExchangeRateDate*, *EffectiveUnitPrice*, and *RateOfPartnerEarnedCredit* properties
    * Modified the type for the *AdditionalInfo* and *Tags* properties from string to *Dictionary<string, string>*
  * [One Time Invoice Line Item](https://github.com/microsoft/Partner-Center-PowerShell/blob/master/src/PowerShell/Models/Invoices/PSOneTimeInvoiceLineItem.cs)
    * Added the *BillableQuantity*, *MeterDescription*, *PCToBCExchangeRateDate*, *PCToBCExchangeRate*, *PriceAdjustmentDescription*, and *PricingCurrency* properties
* Partner
  * Added the [Get-PartnerUser](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerProductUpgrade) command to get partner user accounts
    * Added the [Get-PartnerUserSignActivity](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerUserSignActivity) command to get sign-in activities for the specified user account
* Product Upgrades
  * Added the [Get-PartnerProductUpgrade](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerProductUpgrade) command to get information on product upgrades for the specified customer
  * Added the [Get-PartnerProductUpgradeEligibility](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerProductUpgrade) command to determine if the specified customer has a product eligible for an upgrade
  * Added the [Get-PartnerProductUpgradeStatus](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerProductUpgradeStatus) command to get the status for product upgrades for the specified customer
  * Added the [New-PartnerProductUpgrade](https://docs.microsoft.com/powershell/module/partnercenter/New-PartnerProductUpgrade) command to perform an upgrade for the specified customer
* Subscriptions
  * Added the [Get-PartnerCustomerAzurePlanEntitlement](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerCustomerAzurePlanEntitlement) command to get entitlement information for an Azure Plan
* Usage
  * Added the [Get-PartnerCustomerUsageRecord](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerCustomerUsageRecord) command to get month usage records for all customers
  * Removed the `Get-PartnerCustomerSubscriptionUsage` command due to changes with the Partner Center SDK for .NET. This command will be replaced with the [Get-PartnerCustomerSubscriptionMeterUsage](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionMeterUsage) and [Get-PartnerCustomerSubscriptionResourceUsage](https://docs.microsoft.com/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionResourceUsage) commands

## 2.0.1909.5 - September 2019

* Dependency
  * Corrected an issue that was preventing a dependency from being updated after a successful build

## 2.0.1909.4 - September 2019

* Authentication
  * Log events from the Microsoft Authentication Library (MSAL) will now be written to the console when the debug flag is set

## 2.0.1909.3 - September 2019

* Authentication
  * Address issue [#156](https://github.com/microsoft/Partner-Center-PowerShell/issues/156) where the refresh token was not being returned if it had not been previously used by the module during an interactive authentication attempt
  * After successfully authenticating the module will attempt to get country and locale based on the partner organization profile
* Security
  * Adding the [Test-PartnerSecurityRequirement](/powershell/module/partnercenter/Test-PartnerSecurityRequirement) command to help validate that the authenticating account was challenged for multi-factor authentication

## 2.0.1909.2 - September 2019

* Authentication
  * Addressed issue [#153](https://github.com/microsoft/Partner-Center-PowerShell/issues/153) that was preventing the [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) command from working as expected.
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
