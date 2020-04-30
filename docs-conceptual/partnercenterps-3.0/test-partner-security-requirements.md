---
title: Testing the Partner Security Requirements
description: Learn more about testing the partner security requirements.
ms.date: 12/05/2019
---

# Testing the Partner Security Requirements

See [Partner Security Requirements](https://docs.microsoft.com/partner-center/partner-security-requirements) to learn more about the requirements. These requirements will be enforced by Azure Active Directory and Partner Center. To validate the account accessing resources was challenged for multi-factor authentication both platforms will be checking the [authentication method reference](https://tools.ietf.org/html/rfc8176) claim to see if MFA is listed.

> [!NOTE]
> If you are using Azure Active Directory with Azure Multi-Factor Authentication, then the authentication method reference (AMR) claim will be present. However, if you have implemented a third-party solution there is a chance additional actions will need to be taken to ensure the claim is issued. You will need to work with the vendor of your third-party solution to determine what actions are will be required.

## Checking your account

You can use the [Test-PartnerSecurityRequirement](https://docs.microsoft.com/powershell/module/partnercenter/Test-PartnerSecurityRequirement) command to check if the authentication method reference claim is present and that it contains the MFA value. When you run this command, it will prompt you to authenticate, and the test will be performed using the authenticating account.

If the claim is missing, the you will see a response similar to the following

```powershell
Test-PartnerSecurityRequirement
```

```output
WARNING: Attempting to launch a browser for authorization code login.
WARNING: We have launched a browser for you to login. For the old experience with device code flow, please run 'Test-PartnerSecurityRequirement -UseDeviceAuthentication'.
WARNING: Unable to find the AMR claim, which means the ability to verify the MFA challenge happened will not be possible. See https://aka.ms/partnercenterps-testing-psr for more information.
fail
```

If the claim is present and it is missing the MFA value, then you will see a response similar to the following

```powershell
Test-PartnerSecurityRequirement
```

```output
WARNING: Attempting to launch a browser for authorization code login.
WARNING: We have launched a browser for you to login. For the old experience with device code flow, please run 'Test-PartnerSecurityRequirement -UseDeviceAuthentication'.
WARNING: Unable to determine if the account authenticated using MFA. See https://aka.ms/partnercenterps-testing-psr for more information.
fail
```

If the claim is present and the MFA value is present, then you will see a response similar to the following

```powershell
Test-PartnerSecurityRequirement
```

```output
pass
```

## Reacting to a failed test

If the output from the [Test-PartnerSecurityRequirement](https://docs.microsoft.com/powershell/module/partnercenter/Test-PartnerSecurityRequirement) command states the test failed, then you have additional actions that need to performed. Either the authentication method reference claim is missing or the MFA value was not listed. Both of these scenarios can happen even if the account was challenged for multi-factor authentication.

> [!IMPORTANT]
> When using a third-party solution, you will need to work with the vendor who developed the solution to determine what actions should be taken.

If you are using Active Directory Federation Service (ADFS), then you will need to ensure that the `http://schemas.microsoft.com/claims/multipleauthn` claim is being issued by the relying party trust.

## Additional Information

The [Test-PartnerSecurityRequirement](https://docs.microsoft.com/powershell/module/partnercenter/Test-PartnerSecurityRequirement) command decodes the access token generated as a result of a successful authentication attempt. Next it will check if the authentication method reference (AMR) claim is present. If the claim is present, then it will confirm that the MFA value is listed. You can reproduce this test by decoding an access token using the [JWT Decoder](https://adfshelp.microsoft.com/JwtDecoder/GetToken) and checking the values listed in the AMR element.

The following is an example of a decoded access token that correctly reflects the account was challenged for multi-factor authentication.

```json
{
  "aud": "https://api.partnercenter.microsoft.com",
  "iss": "https://sts.windows.net/df845f1a-7b35-40a2-ba78-6481de91f8ae/",
  "iat": 1549088552,
  "nbf": 1549088552,
  "exp": 1549092452,
  "acr": "1",
  "amr": [
    "pwd",
    "mfa"
  ],
  "appid": "23ec45a3-5127-4185-9eff-c8887839e6ab",
  "appidacr": "0",
  "family_name": "Williams",
  "given_name": "Isaiah",
  "ipaddr": "127.0.0.1",
  "name": "Isaiah Williams",
  "oid": "4988e250-5aee-482a-9136-6d269cb755c0",
  "scp": "user_impersonation",
  "tenant_region_scope": "NA",
  "tid": "df845f1a-7b35-40a2-ba78-6481de91f8ae",
  "unique_name": "Isaiah.Williams@testtestpartner.onmicrosoft.com",
  "upn": "Isaiah.Williams@testtestpartner.onmicrosoft.com",
  "ver": "1.0"
}
```
