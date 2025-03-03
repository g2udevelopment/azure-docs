---
title: Best practices for Web Application Firewall on Azure Application Gateway
description: In this tutorial, you learn about the best practices for using the web application firewall with Application Gateway.
services: web-application-firewall
author: vhorne
ms.service: web-application-firewall
ms.topic: tutorial
ms.date: 07/18/2022
ms.author: jodowns
---

# Best practices for Web Application Firewall on Application Gateway

This article summarizes best practices for using the web application firewall (WAF) on Azure Application Gateway.

## General best practices

### Enable the WAF

For internet-facing applications, we recommend you enable a web application firewall (WAF) and configure it to use managed rules. When you use a WAF and Microsoft-managed rules, your application is protected from a range of attacks.

### Use WAF policies

WAF policies are the new resource type for managing your Application Gateway WAF. If you have older WAFs that use WAF Configuration resources, you should migrate to WAF policies to take advantage of the latest features.

For more information, see the following resources:
- [Migrate Web Application Firewall policies using Azure PowerShell](./migrate-policy.md)
- [Upgrade Application Gateway WAF configuration to WAF policy using Azure Firewall Manager](../shared/manage-policies.md#upgrade-application-gateway-waf-configuration-to-waf-policy)

### Tune your WAF

The rules in your WAF should be tuned for your workload. If you don't tune your WAF, it might accidentally block requests that should be allowed. Tuning might involve creating [rule exclusions](application-gateway-waf-configuration.md) to reduce false positive detections.

While you tune your WAF, consider using [detection mode](create-waf-policy-ag.md#configure-waf-rules-optional), which logs requests and the actions the WAF would normally take, but doesn't actually block any traffic.

For more information, see [Troubleshoot Web Application Firewall (WAF) for Azure Application Gateway](web-application-firewall-troubleshoot.md).

### Use prevention mode

After you've tuned your WAF, you should configure it to [run in prevention mode](create-waf-policy-ag.md#configure-waf-rules-optional). By running in prevention mode, you ensure the WAF actually blocks requests that it detects are malicious. Running in detection mode is useful while you tune and configure your WAF, but provides no protection.

## Managed ruleset best practices

### Enable core rule sets

Microsoft's core rule sets are designed to protect your application by detecting and blocking common attacks. The rules are based on a various sources including the OWASP top 10 attack types and information from Microsoft Threat Intelligence.

For more information, see [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

### Enable bot management rules

Bots are responsible for a significant proportion of traffic to web applications. The WAF's bot protection rule set categorizes bots based on whether they're good, bad, or unknown. Bad bots can then be blocked, while good bots like search engine crawlers are allowed through to your application.

For more information, see [Azure Web Application Firewall on Azure Application Gateway bot protection overview](bot-protection-overview.md).

### Use the latest ruleset versions

Microsoft regularly updates the managed rules to take account of the current threat landscape. Ensure that you regularly check for updates to Azure-managed rule sets.

For more information, see [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

## Geo-filtering best practices

### Geo-filter traffic

Many web applications are designed for users within a specific geographic region. If this situation applies to your application, consider implementing geo-filtering to block requests that come from outside of the countries you expect to receive traffic from.

For more information, see [Geomatch custom rules](geomatch-custom-rules.md).

## Logging

### Add diagnostic settings to save your WAF's logs

Application Gateway's WAF integrates with Azure Monitor. It's important to save the WAF logs to a destination like Log Analytics. You should review the WAF logs regularly. Reviewing logs helps you to [tune your WAF policies to reduce false-positive detections](#tune-your-waf), and to understand whether your application has been the subject of attacks.

For more information, see [Azure Web Application Firewall Monitoring and Logging](application-gateway-waf-metrics.md).

### Send logs to Microsoft Sentinel

Microsoft Sentinel is a security information and event management (SIEM) system, which imports logs and data from multiple sources to understand the threat landscape for your web application and overall Azure environment. Application Gateway's WAF logs should be imported into Microsoft Sentinel or another SIEM so that your internet-facing properties are included in its analysis. For Microsoft Sentinel, use the Azure WAF connector to easily import your WAF logs.

For more information, see [Using Microsoft Sentinel with Azure Web Application Firewall](../waf-sentinel.md).

## Next steps

Learn how to [enable the WAF on an Application Gateway](application-gateway-web-application-firewall-portal.md).
