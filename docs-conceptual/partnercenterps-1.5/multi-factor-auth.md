---
title: Multi-factor Authentication | Microsoft Docs
description: Leveraging the Partner Center PowerShell module to obtain access tokens, used to connect to other PowerShell modules.
ms.date: 05/17/2019
---

# Multi-Factor Authentication

Multi-Factor Authentication (MFA) helps safeguard access to data and applications while maintaining simplicity for users. It provides additional security by requiring a second form of authentication and delivers strong authentication through a range of easy to use authentication methods. Users may or may not be challenged for Multi-Factor Authentication based on configuration decisions that an administrator makes. The requirement for Multi-Factor Authentication can complicate any automation that you have developed because a second form of authentication must be provided when authenticating.

Azure Active Directory has recently introduced a new feature known as baseline protection. Baseline protection is a set of predefined [conditional access policies](/azure/active-directory/conditional-access/overview). The goal of these policies is to ensure that you have at least the baseline level of security enabled in all editions of Azure Active Directory. Through the enforcement of these policies users who meet the criteria of the baseline policy will be required to authenticate using Multi-Factor Authentication.

With the requirement for Multi-Factor Authentication you will face a new challenge when automating tasks in a headless manner. This article covers how to utilize the [Secure Application Model](secure-app-model.md) to establish a connection to the following PowerShell modules without being prompted for credentials.

* Azure PowerShell
* Azure Active Directory
* MS Online
* Partner Center

## Azure

### Azure PowerShell

```powershell
$credential = Get-Credential
$refreshToken = 'Your-Refresh-Token-Value'

$azureToken = New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://management.azure.com/ -Credential $credential
$graphToken =  New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://graph.microsoft.com -Credential $credential

# Az Module
Connect-AzAccount -AccessToken $token.AccessToken -GraphAccessToken $graphToken.AccessToken -TenantId '<TenantId>'

# AzureRM Module
Connect-AzureRmAccount -AccessToken $token.AccessToken -GraphAccessToken $graphToken.AccessToken -TenantId '<TenantId>'
```

## Microsoft 365

### Azure Active Directory

```powershell
$credential = Get-Credential
$refreshToken = 'Your-Refresh-Token-Value'

$aadGraphToken = New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://graph.windows.net -Credential $credential
$graphToken =  New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://graph.microsoft.com -Credential $credential

Connect-AzureAD -AadAccessToken $aadGraphToken.AccessToken -AccountId '<UPN-OF-USER-USED-TO-GEN-REFRESH-TOKEN>' -MsAccessToken $graphToken.AccessToken
```

### Exchange Online PowerShell

When MFA is enabled partners will not be able to utilize their delegated administrative privileges with Exchange Online PowerShell to perform actions against their customers. See [Connect to Exchange Online PowerShell using multi-factor authentication](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/mfa-connect-to-exchange-online-powershell) for more information regarding this limitation.

### MS Online

```powershell
$credential = Get-Credential
$refreshToken = 'Your-Refresh-Token-Value'

$aadGraphToken = New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://graph.windows.net -Credential $credential
$graphToken =  New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://graph.microsoft.com -Credential $credential

Connect-MsolService -AdGraphAccessToken $aadGraphToken.AccessToken -MsGraphAccessToken $graphToken.AccessToken
```

## Partner Center

```powershell
$refreshToken = 'Enter the refresh token value here'

$credential = Get-Credential
$pcToken = New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://api.partnercenter.microsoft.com -Credential $credential -TenantId '<Your Tenant Id>'

Connect-PartnerCenter -AccessToken $pcToken.AccessToken -ApplicationId $appId -TenantId '<Your Tenant Id>'
```
