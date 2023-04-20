---
title: Release notes for Partner Center PowerShell
description: Discover what has changed with Partner Center PowerShell with each release.
ms.date: 12/05/2019
---

# Release notes

## 3.0.6 - January 2020

* Authentication 
  * Addressed issue [#268](https://github.com/microsoft/Partner-Center-PowerShell/issues/268) that was impacting the [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) command when trying to get an access token for Exchange Online with a refresh token
* Agreements
  * Addressed issue [#262](https://github.com/microsoft/Partner-Center-PowerShell/issues/262) that was preventing [Get-PartnerAgreementDocument](/powershell/module/partnercenter/Get-PartnerAgreementDocument) from being invoked when the `Language` parameter was specified
* Qualifications
  * Addressed issue [#258](https://github.com/microsoft/Partner-Center-PowerShell/issues/258) with the [Set-PartnerCustomerQualification](/powershell/module/partnercenter/Set-PartnerCustomerQualification) command that was preventing API exception information from being parsed as excepted

## 3.0.5 - January 2020

* Authentication
  * Addressed issue [#254](https://github.com/microsoft/Partner-Center-PowerShell/issues/254) with the [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) where the Scope parameter was incorrectly being required
  * Addressed an issue where NullReferenceException exception was being encountered when invoking [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) using a certificate
  * Addressed an issue where NullReferenceException exception was being encountered when invoking [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) using a certificate
  * Defined the refresh token parameter set for the [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) command to make it easier to ensure all the appropriate parameters have been specified when exchanging a refresh token for an access token
* Module
  * All commands now perform operations asynchronously

## 3.0.4 - January 2020

* Authentication
  * Addressed an issue where NullReferenceException exception was being encountered when invoking [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) using a certificate
  * Addressed an issue where NullReferenceException exception was being encountered when invoking [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) using a certificate
  * Defined the refresh token parameter set for the [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) command to make it easier to ensure all the appropriate parameters have been specified when exchanging a refresh token for an access token
* Module
  * All commands now perform operations asynchronously

## 3.0.3 - December 2019

* Authentication
  * Added the [Register-PartnerTokenCache](/powershell/module/partnercenter/Register-PartnerTokenCache) to create, and delete, the control file that determines if a in-memory token cache should be used instead of the default persistent token cache
  * Addressed an issue where an InvalidOperationException exception was being encountering with the [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) and [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) commands when specifying an environment
  * Addressed an issue where an InvalidOperationException exception was being encountered under certain circumstances when invoking [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) and attempting to authenticate interactively
  * Addressed issue [#234](https://github.com/microsoft/Partner-Center-PowerShell/issues/234) that was preventing the [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) command from executing successfully when being invoked through an Azure Function app
* Invoice
  * Added the [Get-PartnerUnbilledInvoiceLineItem](/powershell/module/partnercenter/Get-PartnerUnbilledInvoiceLineItem) command to get unbilled invoice line items
  * Removed the `Period` parameter from the [Get-PartnerInvoiceLineItem](/powershell/module/partnercenter/Get-PartnerInvoiceLineItem) command because the functionality it enabled has been replaced with the [Get-PartnerUnbilledInvoiceLineItem](/powershell/module/partnercenter/Get-PartnerUnbilledInvoiceLineItem) command
* Network
  * Addressed an issue where the HTTP response from [Get-PartnerUser](/powershell/module/partnercenter/Get-PartnerUser) and [Get-PartnerUserSignInActivity](/powershell/module/partnercenter/Get-PartnerUserSignInActivity) was not being correctly written to the debug pipeline
* Product Upgrades
  * Addressed an issue with starting the upgrade process for an Azure Plan
* Subscription
  * Added the `PartnerId` parameter to the [Set-PartnerCustomerSubscription](/powershell/module/partnercenter/Set-PartnerCustomerSubscription) command
  * Addressed issue [#228](https://github.com/microsoft/Partner-Center-PowerShell/issues/228) that was causing issues with enabling and suspend an Azure subscription that is part of an Azure Plan

## 3.0.2 - December 2019

* Authentication
  * Addressed issue [#230](https://github.com/microsoft/Partner-Center-PowerShell/issues/230) that was caused by a deadlock

## 3.0.1 - December 2019

* Authentication
  * Updating the [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) command to make the `CertificateThumbprint` parameter required for the `ServicePrincipalCertificate` parameter set
* Security
  * Addressed issue [#194](https://github.com/microsoft/Partner-Center-PowerShell/issues/194) that was preventing the [Get-PartnerUserSignInActivity](/powershell/module/partnercenter/Get-PartnerUserSignInActivity) command from executing as expected in all scenarios
* Subscription
  * Added [Enable-PartnerAzureSubscription](/powershell/module/partnercenter/Enable-PartnerAzureSubscription) command to enable a suspend Azure subscription that is part of an Azure Plan
  * Added [Suspend-PartnerAzureSubscription](/powershell/module/partnercenter/Suspend-PartnerAzureSubscription) command to suspend an Azure subscription that is part of an Azure Plan
  * Removed the `CustomerName` parameter from the [New-PartnerAzureSubscription](/powershell/module/partnercenter/New-PartnerAzureSubscription)

## 3.0.0 - December 2019

* Agreement
  * Added the [Get-PartnerAgreementStatus](/powershell/module/partnercenter/Get-PartnerAgreementStatus) command to get the status of acceptance of the Microsoft Partner Agreement for the specified partner
* Authentication
  * Updated how [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) writes warnings during an authentication attempt
  * Updated how [New-PartnerAccessToken](/powershell/module/partnercenter/New-PartnerAccessToken) prompts for interaction
  * When using [Connect-PartnerCenter](/powershell/module/partnercenter/Connect-PartnerCenter) with an access token the account and tenant information are now extracted from the access token
* Azure
  * Added the [Get-PartnerAzureBillingPolicy](/powershell/module/partnercenter/Get-PartnerAzureBillingPolicy) to get the billing policy for the specified customer
  * Added the [Set-PartnerAzureBillingPolicy](/powershell/module/partnercenter/Set-PartnerAzureBillingPolicy) to update the billing policy for the specified customer
* Build
  * Updating the test project from .NET Core 2.2 to .NET 3.0
* Dependency
  * Updated to the latest version of the Partner Center SDK for .NET
* Invoice
  * Added the `Period` parameter to the [Get-PartnerInvoiceLineItem](/powershell/module/partnercenter/Get-PartnerInvoiceLineItem) command to provide a way for the user to specify if they want the current or previous unbilled line items
  * Addressed issue [#202](https://github.com/microsoft/Partner-Center-PowerShell/issues/202) that was returning request for invoice line items with no errors
* Module
  * Addressed issue [#217](https://github.com/microsoft/Partner-Center-PowerShell/issues/217) that was impacting executing commands through Azure Automation
  * Updated the transient error strategy for network operations
  * When running any command with with the `Debug` parameter the request and response from the API will be written to the console in addition to any operation specific debug information
* Security
  * Modified the [Get-PartnerUser](/powershell/module/partnercenter/Get-PartnerUser) command to leverage a task scheduler for requesting from Microsoft Graph
  * Modified the [Get-PartnerUserSignInActivity](/powershell/module/partnercenter/Get-PartnerUserSignInActivity) command to leverage a task scheduler for requesting from Microsoft Graph
  * Updated how [Test-PartnerSecurityRequirement](/powershell/module/partnercenter/Test-PartnerSecurityRequirement) prompts for interaction
* Subscription
  * Addressed an issue where the request for subscriptions by partner was causing an `InvalidCastException` to be thrown
  * Corrected the output for the [Get-PartnerCustomerAzurePlanEntitlement](/powershell/module/partnercenter/Get-PartnerCustomerAzurePlanEntitlement) command
* Validation
  * Addressed a scenario where a `NullReferenceException` could be thrown when running the [Test-PartnerAddress](/powershell/module/partnercenter/Test-PartnerAddress) command

## 2.0.1911.5 - November 2019

* Security
  * Optimized the Get-PartnerUser command
  * Optimized the Get-PartnerUserSignInActivity command

## 2.0.1911.4 - November 2019

* Azure
  * Added the [Get-PartnerAzureBillingAccount](/powershell/module/partnercenter/get-partnerazurebillingaccount) command to get billing accounts where the authenticated user has access
  * Added the [Get-PartnerAzureBillingProfile](/powershell/module/partnercenter/get-partnerazurebillingprofile) to get billing profiles for specified billing account
  * Added the [New-PartnerAzureSubscription](/powershell/module/partnercenter/new-partnerazuresubscription) to create a new Azure subscription for Microsoft Partner Agreement billing account.
* Security
  * Updated the [Get-PartnerUser](/powershell/module/partnercenter/Get-PartnerUser) command to ensure all user accounts are returned
  * Updated the [Get-PartnerUserSignInActivity](/powershell/module/partnercenter/Get-PartnerUserSignInActivity) command to ensure all user sign-in activities are returned

## 2.0.1911.3 - November 2019

* Authentication
  * Addressed issue [#186](https://github.com/microsoft/Partner-Center-PowerShell/issues/186) that was preventing access token from being generated when using the device code flow
* Security
  * Addressed issue preventing the [Test-PartnerSecurityRequirement](/powershell/module/partnercenter/test-partnersecurityrequirement) command from working as expected

## 2.0.1911.2 - November 2019

* Dependencies
  * Addressed issues [#183](https://github.com/microsoft/Partner-Center-PowerShell/issues/181) and [#183](https://github.com/microsoft/Partner-Center-PowerShell/issues/183) caused by an assembly binding issue

## 2.0.1911.1 - November 2019

* Authentication
  * Addressed issue preventing CTRL+C from interrupting the waiting for a response during the interactive authentication scenario
* Invoicing
  * [Daily Rated Usage Line Item](https://github.com/microsoft/Partner-Center-PowerShell/blob/master/src/PowerShell/Models/Invoices/PSDailyRatedUsageLineItem.cs)
    * Added the *EntitlementId*, *EntitlementDescription*, *PCToBCExchangeRate*, *PCToBCExchangeRateDate*, *EffectiveUnitPrice*, and *RateOfPartnerEarnedCredit* properties
    * Modified the type for the *AdditionalInfo* and *Tags* properties from string to *Dictionary<string, string>*
  * [One Time Invoice Line Item](https://github.com/microsoft/Partner-Center-PowerShell/blob/master/src/PowerShell/Models/Invoices/PSOneTimeInvoiceLineItem.cs)
    * Added the *BillableQuantity*, *MeterDescription*, *PCToBCExchangeRateDate*, *PCToBCExchangeRate*, *PriceAdjustmentDescription*, and *PricingCurrency* properties
* Product Upgrades
  * Added the Get-PartnerProductUpgrade command to get information on product upgrades for the specified customer
  * Added the [Get-PartnerProductUpgradeEligibility](/powershell/module/partnercenter/Get-PartnerProductUpgradeEligibility) command to determine if the specified customer has a product eligible for an upgrade
  * Added the [Get-PartnerProductUpgradeStatus](/powershell/module/partnercenter/Get-PartnerProductUpgradeStatus) command to get the status for product upgrades for the specified customer
  * Added the [New-PartnerProductUpgrade](/powershell/module/partnercenter/New-PartnerProductUpgrade) command to perform an upgrade for the specified customer
* Security
  * Added the [Get-PartnerUser](/powershell/module/partnercenter/Get-PartnerUser) command to get partner user accounts
    * Added the Get-PartnerUserSignInActivity command to get sign-in activities for the specified user account
* Subscriptions
  * Added the [Get-PartnerCustomerAzurePlanEntitlement](/powershell/module/partnercenter/Get-PartnerCustomerAzurePlanEntitlement) command to get entitlement information for an Azure Plan
* Usage
  * Added the [Get-PartnerCustomerUsageRecord](/powershell/module/partnercenter/Get-PartnerCustomerUsageRecord) command to get month usage records for all customers
  * Removed the `Get-PartnerCustomerSubscriptionUsage` command due to changes with the Partner Center SDK for .NET. This command will be replaced with the [Get-PartnerCustomerSubscriptionMeterUsage](/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionMeterUsage) and [Get-PartnerCustomerSubscriptionResourceUsage](/powershell/module/partnercenter/Get-PartnerCustomerSubscriptionResourceUsage) commands

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
  * Added the Get-PartnerAgreementTemplate command to provide access to the links download or view the Microsoft Customer Agreement
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
  * Added the New-PartnerCustomerSubscriptionActivation command to make it where third-party subscriptions can be activated in the integration sandbox
