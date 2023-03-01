---
title: Use the Exchange Online PowerShell v3 module with GDAP and App consent
description: Learn how to use the Exchange Online PowerShell v3 module with GDAP and App consent.
ms.date: 01/24/2023
---

# Use the Exchange Online PowerShell v3 Module with GDAP and App Consent

If you are not already familiar with how GDAP changes the Secure App Model, read the [GDAP to DAP Secure Application Model document](https://aka.ms/gdap-sam).

## Prerequisites

- A multi-tenant app created in your partner tenant
  - Since the sample script is using the Partner Center Consent API, ensure the app has `user_impersonation` permissions for the Partner Center API (fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd). For more information about Secure App Model permissions, see [Create a secure partner application](/partner-center/developer/secure-sample-application#apply-permissions)
- [ExchangeOnlineManagement 3.1.0 Powershell module](https://www.powershellgallery.com/packages/ExchangeOnlineManagement/3.1.0)
- [Partner Center Powershell module](install.md)
- A GDAP relationship approved by the customer that has one of the following roles:
  - Global admin
  - Privileged role admin
  - Cloud application admin
- User account that is a member of the AdminAgents group as well as a member of the group with the aforementioned GDAP relationship.

## Sample script

Below is a simplified sample PowerShell script that sets up a consented application in the customer’s tenant.

> [!WARNING]
> This script is for illustrative purposes. Secrets should be stored in a key vault as outlined in the [Secure Application Model framework](/partner-center/developer/enable-secure-app-model#get-refresh-token).

```powershell
#variables
$AppId = '<AppID in Partner tenant>'
$AppSecret = '<App secret from AppID in partner tenant>'
$CustomerTenantId = '<Customer tenant ID>'
$consentscope = 'https://api.partnercenter.microsoft.com/user_impersonation'
$AppCredential = (New-Object System.Management.Automation.PSCredential ($AppId, (ConvertTo-SecureString $AppSecret -AsPlainText -Force)))
$PartnerTenantid = '<Partner tenant ID>'
$AppDisplayName = '<App name for AppID in Partner tenant>'
# Get PartnerAccessToken token
$PartnerAccessToken = New-PartnerAccessToken -serviceprincipal -ApplicationId $AppId -Credential $AppCredential -Scopes $consentscope -tenant $PartnerTenantid -UseAuthorizationCode
# Connect using PartnerAccessToken token
$PartnerCenter = Connect-PartnerCenter -AccessToken $PartnerAccessToken.AccessToken
#Grants needed
$MSGraphgrant = New-Object -TypeName Microsoft.Store.PartnerCenter.Models.ApplicationConsents.ApplicationGrant
$MSgraphgrant.EnterpriseApplicationId = "00000003-0000-0000-c000-000000000000"
$MSGraphgrant.Scope = "Directory.Read.All,Directory.AccessAsUser.All"
$ExOgrant = New-Object -TypeName Microsoft.Store.PartnerCenter.Models.ApplicationConsents.ApplicationGrant
$ExOgrant.EnterpriseApplicationID = "00000002-0000-0ff1-ce00-000000000000"
$ExOgrant.Scope = "Exchange.Manage"
New-PartnerCustomerApplicationConsent -ApplicationGrants @($MSGraphgrant, $ExOgrant) -CustomerId $CustomerTenantId -ApplicationId $AppId -DisplayName $appdisplayname
#Connect to customer Exchange via App+User
$token = New-PartnerAccessToken -ApplicationId $AppId -Scopes 'https://outlook.office365.com/.default' -ServicePrincipal -Credential $appcredential -Tenant $CustomerTenantId -RefreshToken $PartnerAccesstoken.refreshToken
Connect-ExchangeOnline -DelegatedOrganization $CustomerTenantId -AccessToken $token.AccessToken
```
