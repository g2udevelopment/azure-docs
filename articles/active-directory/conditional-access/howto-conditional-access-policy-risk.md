---
title: Sign-in risk-based Conditional Access - Azure Active Directory
description: Create Conditional Access policies using Identity Protection sign-in risk

services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: how-to
ms.date: 03/21/2022

ms.author: joflore
author: MicrosoftGuyJFlo
manager: amycolannino
ms.reviewer: calebb, davidspo

ms.collection: M365-identity-device-management
---
# Conditional Access: Sign-in risk-based Conditional Access

Most users have a normal behavior that can be tracked, when they fall outside of this norm it could be risky to allow them to just sign in. You may want to block that user or maybe just ask them to perform multi-factor authentication to prove that they are really who they say they are. 

A sign-in risk represents the probability that a given authentication request isn't authorized by the identity owner. Organizations with Azure AD Premium P2 licenses can create Conditional Access policies incorporating [Azure AD Identity Protection sign-in risk detections](../identity-protection/concept-identity-protection-risks.md#sign-in-risk). 

There are two locations where this policy may be configured, Conditional Access and Identity Protection. Configuration using a Conditional Access policy is the preferred method providing more context including enhanced diagnostic data, report-only mode integration, Graph API support, and the ability to utilize other Conditional Access attributes in the policy.

The Sign-in risk-based policy protects users from registering MFA in risky sessions. For example. If the users are not registered for MFA, their risky sign-ins will get blocked and presented with the AADSTS53004 error.

## Template deployment

Organizations can choose to deploy this policy using the steps outlined below or using the [Conditional Access templates (Preview)](concept-conditional-access-policy-common.md#conditional-access-templates-preview). 

## Enable with Conditional Access policy

1. Sign in to the **Azure portal** as a global administrator, security administrator, or Conditional Access administrator.
1. Browse to **Azure Active Directory** > **Security** > **Conditional Access**.
1. Select **New policy**.
1. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
1. Under **Assignments**, select **Users and groups**.
   1. Under **Include**, select **All users**.
   1. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts. 
   1. Select **Done**.
1. Under **Cloud apps or actions** > **Include**, select **All cloud apps**.
1. Under **Conditions** > **Sign-in risk**, set **Configure** to **Yes**. Under **Select the sign-in risk level this policy will apply to**. 
   1. Select **High** and **Medium**.
   1. Select **Done**.
1. Under **Access controls** > **Grant**.
   1. Select **Grant access**, **Require multi-factor authentication**.
   1. Select **Select**.
1. Confirm your settings and set **Enable policy** to **Report-only**.
1. Select **Create** to create to enable your policy.

After confirming your settings using [report-only mode](howto-conditional-access-insights-reporting.md), an administrator can move the **Enable policy** toggle from **Report-only** to **On**.

## Next steps

[Conditional Access common policies](concept-conditional-access-policy-common.md)

[User risk-based Conditional Access](howto-conditional-access-policy-risk-user.md)

[Determine impact using Conditional Access report-only mode](howto-conditional-access-insights-reporting.md)

[Simulate sign in behavior using the Conditional Access What If tool](troubleshoot-conditional-access-what-if.md)

[What is Azure Active Directory Identity Protection?](../identity-protection/overview-identity-protection.md)
