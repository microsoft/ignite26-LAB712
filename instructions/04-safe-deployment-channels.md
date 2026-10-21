---
ms.custom: msecd-doc-authoring-106
---

# Assign device groups to safe deployment channels

**Estimated time:** 10 minutes.

Safe deployment plan (SDP) channels help you evaluate Defender changes on an intentionally selected device population before adopting those changes more broadly. The channels build on Microsoft's existing SDP approach and upgrade the [existing platform and engine channels on Windows](https://learn.microsoft.com/defender-endpoint/manage-gradual-rollout).

The new SDP channels are intended to replace existing Defender update-channel constructs. Use the following mappings in a similar way to current update rings.

| Channel | Purpose | Description |
|---|---|---|
| **Validation Channel** | Test updates before others | Devices in this channel are the first to receive new monthly binary platform and engine updates on Windows and platform updates on Linux. Because the likelihood of new issues is higher, add only devices with the highest risk tolerance. The recommended scope is 1% or less of devices in your environment. |
| **Release Channel - Early** | Get release channel updates earlier during gradual release | The release channel is appropriate for most of your production environment. Devices in this channel are offered updates earliest. Distribute devices across early, fast, and broad based on risk tolerance. Earlier channels can surface unexpected behavior sooner and help you gain confidence before broader deployment. |
| **Release Channel - Fast** | Get release channel updates later during gradual release | The release channel is appropriate for most of your production environment. Devices in this channel receive updates later during the gradual release cycle. |
| **Release Channel - Broad** | Get updates at the end of gradual release | The release channel is appropriate for most of your production environment. Devices in this channel receive updates at the end of the gradual release cycle. |
| **Delayed Channel** | Delay Defender updates | Windows devices in this channel are offered updates approximately 48 hours after devices in Release Channel - Broad. For Linux, updates might arrive 2-10 days after rollout to Release Channel - Broad. Use this channel for critical infrastructure and high-value assets. The recommended scope is 1% or less of devices. |
| **Not configured (default)** | Use default behavior | If you don't configure this policy, devices are added to the release channel. Microsoft determines whether devices receive updates earlier or later within the release channel. |

## Create and assign an SDP policy

1. In the Microsoft Intune admin center, go to **Endpoint security** > **Antivirus** > **Create policy**.
1. Select **Windows** for the platform and **Defender Safe Deployment** for the profile.

	![Create a profile pane with Windows selected as the platform and Defender Safe Deployment Plan available in the profile list.](../img/intune-lab/safe-deployment-profile.png)

1. Select the deployment channel for the policy.

	![Defender Safe Deployment Plan configuration page with the Deployment Channel setting.](../img/intune-lab/deployment-channel-setting.png)

1. Scope and assign the policy to the appropriate device groups.
1. Review the settings and select **Create**.

It can take up to eight hours for the Intune policy to apply to devices in scope. To force a sync during testing:

1. In the Microsoft Intune admin center, go to **All devices**.
1. Select the device.
1. On the action bar, select **Sync**.
1. Select **Yes** to confirm.

After the policy is applied, verify that the correct devices are in the intended channels by using either method:

- Run `Get-MpPreference -DeploymentChannel` in PowerShell.
- In the Microsoft Defender portal, go to **Configuration Management** > **Safe deployment dashboard** > **Deployment channels**.

[Previous: Enable configuration protection](03-configuration-protection.md) | [Lab agenda](README.md) | [Next: View effective settings](05-effective-settings.md)
