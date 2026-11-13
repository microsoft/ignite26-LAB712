---
ms.custom: msecd-doc-authoring-106
---

# Manage devices with Defender for Endpoint that aren't enrolled in Intune

**Estimated time:** 10 minutes.

Enable Microsoft Defender for Endpoint security settings management. This capability lets you use Intune endpoint security policies to manage Defender settings on devices that aren't enrolled in Intune.

For more information, see [Use Intune to manage Microsoft Defender settings on devices that aren't enrolled with Intune](https://learn.microsoft.com/intune/device-security/microsoft-defender/security-settings-management).

## Connect Intune and Defender for Endpoint

1. Sign in to the [Microsoft Intune admin center](https://intune.microsoft.com/).
1. Go to **Endpoint security** > **Microsoft Defender for Endpoint**.
1. If the Defender connection isn't configured, select **Connect Microsoft Defender for Endpoint**.
1. Set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.
1. Select **Save**.

This setting allows eligible devices that are onboarded to Defender for Endpoint, but not enrolled in Intune, to receive endpoint security policies through the Defender for Endpoint management channel.

## Configure the enforcement scope

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
1. Go to **Setup & configuration** > **Settings** > **Endpoints**.
1. Under **Configuration management**, select **Enforcement scope**.
1. Enalbe **Use MDE to enforce security configuration settings from Intune**.
1. Enable the platforms that you want Defender for Endpoint to manage, such as:
	 - Windows client devices
	 - Windows Server devices
	 - Windows Server domain controller devices
	 - Linux devices
	 - macOS devices
1. For each applicable platform, select the scope option for your deployment, such as all eligible devices or a limited device scope.
1. Review options for devices managed by Configuration Manager or onboarded through Defender for Cloud.
1. Select **Save**.

Devices must be included in this enforcement scope before they can complete enrollment into Defender for Endpoint security settings management. If **Manage security settings using Configuration Manager** is enabled, devices with a Configuration Manager client are excluded from Defender for Endpoint security settings management. If it's disabled, eligible devices with the Configuration Manager client can receive policy through the Defender for Endpoint management channel.

[Previous: Manage endpoint security in Microsoft Intune](03-manage-endpoint-security.md) | [Lab agenda](README.md) | [Next: Onboard devices](02-onboard-devices.md)
