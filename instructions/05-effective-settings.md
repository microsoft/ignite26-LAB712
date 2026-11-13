---
ms.custom: msecd-doc-authoring-106
---

# View effective settings

**Estimated time:** 5 minutes.

Verify the resulting state of the settings by viewing the device's effective settings in the Microsoft Defender portal. Effective settings show the configuration enforced on the device, which helps administrators validate protection and troubleshoot conflicting sources.

For this activity, review the Microsoft Defender Antivirus settings shown for the device. Verify safe deployment channels using the [channel verification steps](04-safe-deployment-channels.md#create-and-assign-an-sdp-policy), rather than relying on the SDP policy appearing in **Effective settings**.

For more information, see [Investigate devices in Microsoft Defender for Endpoint](https://learn.microsoft.com/defender-endpoint/investigate-machines).

1. Open the Microsoft Defender portal.
1. Go to **Assets** > **Devices**.
1. Search for and open the device that you want to review.
1. Select **Configuration management** > **Effective settings**.

	![Effective settings page for the fictitious example-device, showing Microsoft Defender Antivirus settings and effective values.](../img/intune-lab/effective-settings.png)

1. Find the behavior-monitoring setting configured in [Manage endpoint security in Microsoft Intune](03-manage-endpoint-security.md#create-a-microsoft-defender-antivirus-policy) and confirm that its effective value enables behavior monitoring. If it isn't shown or doesn't match the assigned policy, ask a proctor to help verify policy assignment and synchronization before drawing conclusions. Check the AI policy's deployment status in Intune; don't assume that profile appears in this view.

[Previous: Assign safe deployment channels](04-safe-deployment-channels.md) | [Lab agenda](README.md) | [Next: Offboard devices](06-offboard-devices.md)
