---
author: ckanyika
ms.author: ckanyika
ms.service: azure-devops
ms.date: 2/24/2025
ms.topic: include
---

### Microsoft Entra profile information (preview)

Last fall, we introduced [Microsoft Entra profile information](/azure/devops/organizations/settings/set-your-preferences?view=azure-devops&tabs=preview-page&preserve-view=true) integration in Azure DevOps, so you no longer need to update your profile separately. Over the next few weeks, this will become the default experience. 

> [!div class="mx-imgBorder"]
> [![Screenshot of Entra profile information toggle.](../../media/252-general-01c.png "Screenshot of Entra profile information toggle")](../../media/252-general-01c.png#lightbox)

The preview will run for a month or two, and after that this will be the way profile information works for Entra users in Azure DevOps. If you need to opt out during the preview, please share feedback so we can address any issues during the preview.

> [!div class="mx-imgBorder"]
> [![Screenshot of feedback box.](../../media/252-general-02.png "Screenshot of feedback box")](../../media/252-general-01.png#lightbox)

### Basic access included with GitHub Enterprise

Starting this week, we're including Azure DevOps Basic usage rights with GitHub Enterprise licenses and automating the experience for Azure DevOps users.

If you're using GitHub Enterprise Cloud with Microsoft Entra, you'll be automatically recognized in Azure DevOps. Your access level will be set to 'GitHub Enterprise,' and you won't accrue additional charges in Azure DevOps [Learn more about access for GitHub Enterprise users](/azure/devops/organizations/accounts/faq-user-and-permissions-management#github-enterprise).

Initially this capability is limited to GitHub Enterprise Cloud users, but we’ll be adding GitHub Enterprise Cloud with Data Residency users soon.

### Azure DevOps Allowed IP addresses

We're thrilled to announce significant upgrades to our networking infrastructure, aimed at enhancing the performance and reliability of our service. Add the new IP addresses below, to your firewall allowlist as soon as possible to ensure continuous service during our infrastructure upgrade.

**IP V4 Ranges:**
* 150.171.22.0/24
* 150.171.23.0/24
* 150.171.73.0/24
* 150.171.74.0/24
* 150.171.75.0/24
* 150.171.76.0/24

**IP V6 Ranges:**
* 2620:1ec:50::/48
* 2620:1ec:51::/48
* 2603:1061:10::/48

**ExpressRoute IP V4 Ranges:**
* 150.171.73.14/32
* 150.171.73.15/32
* 150.171.73.16/32
* 150.171.74.14/32
* 150.171.74.15/32
* 150.171.74.16/32
* 150.171.75.14/32
* 150.171.75.15/32
* 150.171.75.16/32
* 150.171.76.14/32
* 150.171.76.15/32
* 150.171.76.16/32
* 150.171.22.17/32
* 150.171.22.18/32
* 150.171.22.19/32
* 150.171.23.17/32
* 150.171.23.18/32
* 150.171.23.19/32

**ExpressRoute IP V6 Ranges:**
* 2603:1061:10::14/128
* 2603:1061:10::15/128
* 2603:1061:10::16/128
* 2603:1061:10:1::14/128
* 2603:1061:10:1::15/128
* 2603:1061:10:1::16/128
* 2603:1061:10:2::14/128
* 2603:1061:10:2::15/128
* 2603:1061:10:2::16/128
* 2603:1061:10:3::14/128
* 2603:1061:10:3::15/128
* 2603:1061:10:3::16/128
* 2620:1ec:50::17/128
* 2620:1ec:50::18/128
* 2620:1ec:50::19/128
* 2620:1ec:51::17/128
* 2620:1ec:51::18/128
* 2620:1ec:51::19/128

Be advised that these new ExpressRoute IP ranges will be added to ExpressRoute’s 'Azure Global Services' BGP community in March.
For more details please visit our blog, [Update to Azure DevOps Allowed IP addresses](https://devblogs.microsoft.com/devops/update-to-ado-allowed-ip-addresses/).

 