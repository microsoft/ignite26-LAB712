---
ms.custom: msecd-doc-authoring-106
---

# Strengthen endpoint protection from onboarding to offboarding

In this lab, you use Microsoft Intune and Microsoft Defender for Endpoint to manage endpoint security settings, onboard devices, enable configuration protection, assign safe deployment channels, review effective settings, and offboard devices.

## Prerequisites

- Access to the [Microsoft Intune admin center](https://intune.microsoft.com/) and [Microsoft Defender portal](https://security.microsoft.com/) with the lab-provided policy-management account.
- A Windows lab device. Local administrator access is needed for the optional antivirus exclusion activity.

Use only the lab-provided accounts and test devices, not personal or production environments. Don't put deployment keys or credentials in GitHub, screenshots, or notes.

### Enable public preview features

Allow **5 minutes** for this prerequisite setup before starting the activities. Turn on public preview features so that you can use the new features included in this lab.

1. In the Microsoft Defender portal, go to **Settings** > **Endpoints** > **Optional features**.
1. Turn on **Preview features**.

## Follow the lab activities

Select each activity to open its instructions and screenshots. Complete the six activities in order.

| Activity | Time | Primary experience |
|---|---|---|
| [Configure security settings management](01-security-settings-management.md) | 10 minutes | Intune connection and Defender enforcement scope |
| [Onboard devices](02-onboard-devices.md) | 15 minutes | Deployment package creation and device onboarding |
| [Enable configuration protection](03-configuration-protection.md) | 15 minutes | Intune policy creation and device synchronization |
| [Assign safe deployment channels](04-safe-deployment-channels.md) | 10 minutes | Deployment policy and channel verification |
| [View effective settings](05-effective-settings.md) | 10 minutes | Device configuration in the Defender portal |
| [Offboard devices](06-offboard-devices.md) | 10 minutes | Offboarding package creation and execution |

The times are planning estimates: **70 minutes of activities plus 5 minutes of prerequisite setup**, for a total of **75 minutes**. Allow additional time for the introductory presentation, optional exclusion exercises, and policy application delays.

1. Complete the prerequisites before starting activity 1.
1. If you choose the optional antivirus exclusion exercises, start the [baseline test](03-configuration-protection.md#optional-activity-add-a-local-antivirus-exclusion-before-configuration-protection) before enabling configuration protection in activity 3. Don't leave the baseline test until the end of the lab.
1. Confirm that policies have applied before comparing device behavior. If a policy hasn't applied, ask a proctor for help rather than assuming the activity failed.
1. Complete any [optional exclusion cleanup](03-configuration-protection.md#clean-up-the-optional-exclusion-activity) before offboarding the test device in activity 6.
