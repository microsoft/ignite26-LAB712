---
ms.custom: msecd-doc-authoring-106
---

# Strengthen endpoint protection from onboarding to offboarding

Use Microsoft Intune and Microsoft Defender for Endpoint together to manage endpoint protection from onboarding to offboarding, including devices that aren't enrolled in Intune. Defender for Endpoint security settings management lets you use Intune endpoint security policies to manage those devices.

In this lab, you connect the two services, onboard a Windows lab device, enable configuration protection, assign safe deployment channels, and verify the applied configuration before offboarding. The goal is to see both how to configure protection and how to confirm that the device received it.

For a guided session, allow **5 minutes** for introductory context before setup. If you're completing the lab independently, use the scenario above and follow the written activities below; you don't need the presentation slides.

## Prerequisites

- Access to the [Microsoft Intune admin center](https://intune.microsoft.com/) and [Microsoft Defender portal](https://security.microsoft.com/) with the lab-provided policy-management account.
- A Windows lab device with the lab-provided local administrator account for device-side steps.

Use only the lab-provided accounts and test devices, not personal or production environments. Don't put deployment keys or credentials in GitHub, screenshots, or notes.

Some lab features require preview settings and might not be available in every tenant. If a required feature or policy profile is missing, ask a proctor to confirm the lab environment before proceeding.

### Verify public preview features

Allow **5 minutes** for setup and this prerequisite check before starting the activities. The lab tenant might already have public preview features enabled.

1. In the Microsoft Defender portal, go to **Settings** > **Endpoints** > **Optional features**.
1. Check **Preview features**. If it's already **On**, leave it unchanged. Otherwise, turn it **On**.

## Follow the lab activities

Select each activity to open its instructions and screenshots. Complete the six activities in order.

| Activity | Time | Primary experience |
|---|---|---|
| [Configure security settings management](01-security-settings-management.md) | 10 minutes | Intune connection and Defender enforcement scope |
| [Onboard devices](02-onboard-devices.md) | 15 minutes | Deployment package creation and device onboarding |
| [Enable configuration protection](03-configuration-protection.md) | 15 minutes | Intune policy creation and device synchronization |
| [Assign safe deployment channels](04-safe-deployment-channels.md) | 10 minutes | Deployment policy and channel verification |
| [View effective settings](05-effective-settings.md) | 5 minutes | Verify configuration protection in the Defender portal |
| [Offboard devices](06-offboard-devices.md) | 10 minutes | Offboarding package creation and execution |

Plan for **75 minutes total**: **5 minutes of introduction, 5 minutes of setup, and 65 minutes across the six core activities**. These are planning estimates, not guaranteed policy-application times. Each activity page also shows its estimated duration.

The optional exclusion exercises aren't included in the core estimates. Attempt them only if there is enough time within the session for the before-and-after checks and cleanup.

1. Complete the prerequisites before starting activity 1.
1. In a guided session, follow the activities with the speakers and ask a proctor for help when needed.
1. If time allows for the optional antivirus exclusion exercises, start the [baseline test](03-configuration-protection.md#optional-activity-add-a-local-antivirus-exclusion-before-configuration-protection) before enabling configuration protection in activity 3. Don't leave the baseline test until the end of the lab.
1. Complete [configuration-protection synchronization and verification](03-configuration-protection.md#sync-and-verify-configuration-protection) whether or not you do the optional exclusion test. If a policy hasn't applied, ask a proctor for help rather than assuming the activity failed.
1. Complete any [optional exclusion cleanup](03-configuration-protection.md#clean-up-the-optional-exclusion-activity) before offboarding the test device in activity 6.
