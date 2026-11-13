---
ms.custom: msecd-doc-authoring-106
---

# Strengthen endpoint protection from onboarding to offboarding

Use Microsoft Intune and Microsoft Defender for Endpoint together to manage endpoint protection from onboarding to offboarding, including devices that aren't enrolled in Intune. Defender for Endpoint security settings management lets you use Intune endpoint security policies to manage those devices.

In this lab, you connect the two services, onboard a Windows lab device, create antivirus and AI agent runtime protection policies, assign safe deployment channels, and verify the applied configuration before offboarding. The goal is to see both how to configure protection and how to confirm that the device received it.

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
| [Manage endpoint security in Microsoft Intune](03-manage-endpoint-security.md) | 15 minutes | Create and assign antivirus and AI agent runtime protection policies |
| [Assign safe deployment channels](04-safe-deployment-channels.md) | 10 minutes | Deployment policy and channel verification |
| [View effective settings](05-effective-settings.md) | 5 minutes | Review Microsoft Defender Antivirus settings in the Defender portal |
| [Offboard devices](06-offboard-devices.md) | 10 minutes | Offboarding package creation and execution |

Plan for **75 minutes total**: **5 minutes of introduction, 5 minutes of setup, and 65 minutes across the six core activities**. These are planning estimates, not guaranteed policy-application times. Each activity page also shows its estimated duration.

1. Complete the prerequisites before starting activity 1.
1. In a guided session, follow the activities with the speakers and ask a proctor for help when needed.
1. Use only confirmed audit-only modes for the AI policy example and leave **Prompt Evidence Collection** unconfigured. If the profile or its audit-only modes aren't available, ask a proctor before proceeding.
1. Verify [deployment-channel placement](04-safe-deployment-channels.md#create-and-assign-an-sdp-policy) and review [effective settings](05-effective-settings.md) before [offboarding the test device](06-offboard-devices.md). If a policy hasn't applied, ask a proctor for help rather than assuming the activity failed.
1. After verification, follow the instructor's direction to [clean up the two exercise policies](03-manage-endpoint-security.md#clean-up-resources) before offboarding.
