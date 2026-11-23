---
ms.custom: msecd-doc-authoring-106
---

# Strengthen endpoint protection from onboarding to offboarding

Use Microsoft Intune and Microsoft Defender for Endpoint together to manage endpoint protection from onboarding to offboarding, including devices that aren't enrolled in Intune. Defender for Endpoint security settings management lets you use Intune endpoint security policies to manage those devices.

In this lab, you create endpoint security policies, connect Microsoft Intune and Microsoft Defender for Endpoint ervices, onboard a Windows test device, assign a safe deployment channel, and review the applied configuration before offboarding.

For a guided session, allow **5 minutes** for introductory context before setup. If you're completing the lab independently, use the scenario above and follow the written activities below; you don't need the presentation slides.

## Prerequisites

- For self-guided use, bring an authorized non-production Microsoft 365 test tenant with the required Intune and Defender for Endpoint licenses. Use an account assigned with the Security Administrator or Global Adminstrator role to configure the connector and enforcement scope ), manage and report on endpoint security policies, and generate deployment packages. In a guided session, use the environment provided by your instructor.
- Use a supported Windows test device, physical or virtual, that you can administer locally. To practice managing a device without Intune enrollment, use one that isn't enrolled in Intune or onboarded to another organization's Defender environment.
- Prepare a dedicated Microsoft Entra device group for policy assignments. Add the test device once its device record is available. Don't assign the exercise policies to **All Devices**.

For lab purposes, do not use a production tenant or device. 

If you don't have a suitable tenant or Windows test device, use the Microsoft Learn links for a read-through. You won't be able to complete or verify the hands-on steps without these resources.

### Open the lab portals

1. Sign in to your test tenant in the [Microsoft Defender portal](https://security.microsoft.com/) and go to **Setup & configuration** > **Settings**. If you see **Hang on!** or **Endpoints** isn't available yet, start Activity 1 while Defender provisions.

    ![Microsoft Defender portal loading message while it prepares the tenant's data spaces.](../img/intune-lab/defender-portal-initial-setup.png)

1. In a new tab, sign in to the same test tenant in the [Microsoft Intune admin center](https://intune.microsoft.com/).

First-time Defender provisioning varies by tenant. The [Microsoft Learn deployment guide](https://learn.microsoft.com/en-us/defender-endpoint/production-deployment) doesn't specify a fixed wait. Return to Defender before Activity 2 and continue once **Endpoints** appears under **Settings**.

## Follow the lab activities

Select each activity to open its instructions and screenshots. Complete the six activities in order.

| Activity | Time | Primary experience |
|---|---|---|
| [Manage endpoint security in Microsoft Intune](03-manage-endpoint-security.md) | 15 minutes | Create and assign antivirus and AI agent runtime protection policies |
| [Configure security settings management](01-security-settings-management.md) | 10 minutes | Intune connection and Defender enforcement scope |
| [Onboard devices](02-onboard-devices.md) | 15 minutes | Deployment package creation and device onboarding |
| [Assign safe deployment channels](04-safe-deployment-channels.md) | 10 minutes | Deployment policy and channel verification |
| [View effective settings](05-effective-settings.md) | 5 minutes | Review Microsoft Defender Antivirus settings in the Defender portal |
| [Offboard devices](06-offboard-devices.md) | 10 minutes | Offboarding package creation and execution |

Allow **about 75 minutes** for the introduction, portal setup, and six core activities. This estimate excludes preparing your test environment, first-time Defender provisioning, and waits for device check-in or policy results.

1. Create and assign the policies first. Use audit-only modes for the AI policy and leave **Prompt Evidence Collection** unconfigured. Skip the AI exercise if the profile or audit-only modes aren't available.
1. After configuring security settings management and onboarding, you can [check policy deployment](03-manage-endpoint-security.md#verify-deployment-after-onboarding-optional). If results are pending, keep going and return to the check before offboarding.
1. Check [deployment-channel placement](04-safe-deployment-channels.md#verify-the-deployment-channel) separately from [effective settings](05-effective-settings.md). Finish the checks you want to perform before [offboarding the test device](06-offboard-devices.md).

## Lab completion

Onboarding, policy assignment, and effective settings are separate checks. A device appearing in Defender doesn't mean its assigned policies have applied.

- [Manage devices that aren't enrolled in Intune with Defender for Endpoint security settings management](https://learn.microsoft.com/en-us/intune/device-security/microsoft-defender/security-settings-management).
- [Plan a pilot and deploy Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-xdr/pilot-deploy-defender-endpoint).
- [Offboard devices from Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/offboard-machines) and learn why an offboarded device can still appear in inventory.
