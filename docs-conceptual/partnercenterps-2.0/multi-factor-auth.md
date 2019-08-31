---
title: Automating tasks with PowerShell
description: How to automate tasks in PowerShell when Multi-Factor Authentication is enforced.
ms.topic: conceptual
ms.date: 09/09/2019
---

# Multi-Factor Authentication

Multi-Factor Authentication (MFA) helps safeguard access to data and applications while maintaining simplicity for users. It provides additional security by requiring a second form of authentication and delivers strong authentication through a range of easy to use authentication methods. Users may or may not be challenged for Multi-Factor Authentication based on configuration decisions that an administrator makes. Starting on August 1, 2019 all partners involved with the Cloud Solution Provider are contractually required to have Multi-Factor Authentication enforced for all accounts in their partner tenant. See the [partner security requirements](/partner-center/partner-security-requirements) for more information.

## Secure Application Model

The requirement for Multi-Factor Authentication can complicate any automation that you have developed because a second form of authentication must be provided when authenticating. To content with this requirement, the Secure Application Model was developed to provide guidance on how the appropriate authentication can be performed in non-interactive scenarios. This model is comprised of two distinct steps

| Step | Description |
| ---- | ----------- |
| Consent  | This where you will authenticate interactively using the [authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow) or [device code flow](/azure/active-directory/develop/v2-oauth2-device-code). The response from Azure Active Directory will contain an access token and a refresh token. The refresh token value should be stored somewhere secure, such as [Azure Key Vault](/azure/key-vault/key-vault-whatis). This value will be used by your application, or script, instead of user credential when authenticating.  |
| Exchange | Using the securely stored refresh token, generated through the consent step, you will request a new access token from Azure Active Directory. See [refresh the access token](/azure/active-directory/develop/v2-oauth2-auth-code-flow#refresh-the-access-token) for more information regarding the refresh token value. |

> [!IMPORTANT]
> By default, the lifetime of a refresh token is 90 days. So, it is important that you have a process for updating the refresh token prior to the expiration. If it does expire, you will receive an error similar to the following when attempting to exchange it for an access token *The refresh token has expired due to inactivity. The token was issued on 2019-01-02T09:19:53.5422744Z and was inactive for 90.00:00:00*.

### Consent

The consent step can be performed through several different methods. When using PowerShell it is recommended to use the [New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken) cmdlet. The following is an example of how you can request a new access token for use with the Partner Center API, SDK, or PowerShell module.

```powershell-interactive
$credential = Get-Credential
New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'xxxx-xxxx-xxxx-xxxx' -UseAuthorizationCode
```

The first command gets the service principal credentials (application identifier and service principal secret), and then stores them in the `$credential` variable. The second command will generate a new access token using the service principal credentials stored in the `$credential` variable and the authorization code flow. The output from this command will contain several values, including a refresh token. That value should be stored somewhere secure such as [Azure Key Vault](/azure/key-vault/key-vault-whatis) because it will be used instead of user credentials in future operations.

### Exchange

The exchange step can be performed through a number of different methods. When using PowerShell it is recommended to use the [New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken) cmdlet. The following is an example of how to exchange a refresh token for an access token that can be used with the Partner Center API, SDK, or PowerShell module.

```powershell-interactive
credential = Get-Credential
$refreshToken = '<refreshToken>'

New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'
```

The first command gets the service principal credentials (application identifier and service principal secret), and then stores them in the `$credential` variable. The third command will generate a new access token using the service principal credentials stored in the `$credential` variable and the refresh token stored in the `$refreshToken` variable for authentication.

## Samples

The following sections demonstrate how to use the [New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken) cmdlet to request access tokens and connect to other commonly used PowerShell modules.

### Azure

#### Azure PowerShell

```powershell-interactive
$credential = Get-Credential
$refreshToken = '<RefreshToken>'

$azureToken = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://management.azure.com//user_impersonation' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'
$graphToken = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://graph.microsoft.com/.default' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'

# Az Module
Connect-AzAccount -AccessToken $token.AccessToken -AccountId 'azureuser@contoso.com' -GraphAccessToken $graphToken.AccessToken -TenantId 'xxxx-xxxx-xxxx-xxxx'
```

### Microsoft 365

#### Azure Active Directory

```powershell-interactive
$credential = Get-Credential
$refreshToken = '<RefreshToken>'

$aadGraphToken = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://graph.windows.net/.default' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'
$graphToken = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://graph.microsoft.com/.default' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'

Connect-AzureAD -AadAccessToken $aadGraphToken.AccessToken -AccountId 'azureuser@contoso.com' -MsAccessToken $graphToken.AccessToken
```

#### Exchange Online PowerShell

> [!WARNING]
> When MFA is enforced partners will not be able to utilize their delegated administrative privileges with Exchange Online PowerShell to perform actions against their customers. See [Connect to Exchange Online PowerShell using multi-factor authentication](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/mfa-connect-to-exchange-online-powershell) for more information regarding this limitation.

You can work around this limitation by creating a new account and never using it to perform an interactive authentication. It is recommended that you leverage [Azure AD PowerShell](/powershell/module/azuread/) to create the new account and perform the initial configuration. The following PowerShell can be used to create and configure the account

```powershell-interactive
Import-Module AzureAD
Connect-AzureAD

$PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile

$PasswordProfile.Password = "Password"
$PasswordProfile.ForceChangePasswordNextLogin = $false

$user = New-AzureADUser -DisplayName "New User" -PasswordProfile $PasswordProfile -UserPrincipalName "NewUser@contoso.com" -AccountEnabled $true

# Uncomment the following two lines if you want the account to have Admin Agent privileges
# $adminAgentsGroup = Get-AzureADGroup -Filter "DisplayName eq 'AdminAgents'"
# Add-AzureADGroupMember -ObjectId $adminAgentsGroup.ObjectId -RefObjectId $user.ObjectId
```

Next time you connect to Exchange Online through PowerShell use this account and it will work as expected.

> [!IMPORTANT]
> The ability for partners to utilize their delegated administrative privileges with Exchange Online PowerShell to perform actions against their customers, when MFA is enforced, will be available in the future. Until then you should leverage this work around.

#### MS Online

```powershell-interactive
$credential = Get-Credential
$refreshToken = '<RefreshToken>'

$aadGraphToken = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://graph.windows.net/.default' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'
$graphToken = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://graph.microsoft.com/.default' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'

Connect-MsolService -AdGraphAccessToken $aadGraphToken.AccessToken -MsGraphAccessToken $graphToken.AccessToken
```

### Partner Center

```powershell-interactive
$credential = Get-Credential
$refreshToken = '<refreshToken>'
$token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Credential $credential -RefreshToken $refreshToken -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Tenant 'xxxx-xxxx-xxxx-xxxx'

Connect-PartnerCenter -AccessToken $token.AccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Tenant 'xxxx-xxxx-xxxx-xxxx'
```
