---
ms.custom: msecd-doc-authoring-106
---

# Manage devices with Defender for Endpoint that aren't enrolled in Intune

**Estimated time:** 10 minutes.

Enable Microsoft Defender for Endpoint security settings management. This capability lets you use Intune endpoint security policies to manage Defender settings on devices that aren't enrolled in Intune.

For more information, see [Use Intune to manage Microsoft Defender settings on devices that aren't enrolled with Intune](https://learn.microsoft.com/intune/device-security/microsoft-defender/security-settings-management).

## Enable the Microsoft Intune connection in Defender

1. In the [Microsoft Defender portal](https://security.microsoft.com/), go to **Setup & configuration** > **Settings**. If **Endpoints** isn't available yet, wait for provisioning and refresh before continuing.

    ![Microsoft Defender Settings page with the Endpoints entry in the list.](../img/intune-lab/defender-settings-endpoints-navigation.png)

1. Under **Endpoints** > **General** > **Advanced features**, turn on **Microsoft Intune connection** and select **Save preferences**. Scroll down or zoom out slightly if the toggle isn't visible. Use this path directly if the link from Intune doesn't take you to the toggle.

## Verify public preview features

1. To try embedded offboarding in Activity 6, open **Endpoints** > **Optional features**. If **Preview features** is available and off, turn it **On**, select **Save preferences**, and refresh. Leave unrelated options unchanged.

    ![Optional features page showing the Preview features toggle turned on.](../img/intune-lab/defender-optional-preview-features.png)

1. Open **Preview features**. If available, enable **Embedded offboarding experience in Defender deployment tool for Windows**. If either preview control is unavailable, continue and use the [standard offboarding fallback in Activity 6](06-offboard-devices.md#enable-embedded-offboarding).

    ![Manage preview features page showing embedded offboarding enabled in a tenant where it's available.](../img/intune-lab/defender-manage-preview-features.png)

## Configure the enforcement scope

1. Stay in the Microsoft Defender portal and go to **Setup & configuration** > **Settings** > **Endpoints**.
1. Under **Configuration management**, select **Enforcement scope**.
1. Enable **Use MDE to enforce security configuration settings from Intune**.
1. Enable **Windows client devices** for this exercise. Use the limited, tagged-device scope where available. In Activity 3, apply the `MDE-Management` tag to your test device after it appears in Defender. Use the all-devices enforcement scope only in a dedicated test tenant where every eligible Windows client is intended to be in scope. Don't enable additional platforms for the exercise.
1. Review options for devices managed by Configuration Manager or onboarded through Defender for Cloud.
1. Select **Save**.

Devices must be included in this enforcement scope before they can complete enrollment into Defender for Endpoint security settings management. If **Manage security settings using Configuration Manager** is enabled, devices with a Configuration Manager client are excluded from Defender for Endpoint security settings management. If it's disabled, eligible devices with the Configuration Manager client can receive policy through the Defender for Endpoint management channel.

## Connect Intune and Defender for Endpoint

1. After saving the Defender settings, sign in to the [Microsoft Intune admin center](https://intune.microsoft.com/) with an account authorized to configure the connector in your test tenant.
1. Go to **Endpoint security** > **Microsoft Defender for Endpoint** and confirm **Connection status** shows **Enabled**. If it doesn't, verify that **Microsoft Intune connection** is on in Defender, then wait and select **Refresh** in Intune. The status can take up to 15 minutes to update.

    ![Intune connector page showing an example of Connection status as Unavailable before setup.](../img/intune-lab/intune-defender-connector-unavailable.png)

1. Under **Endpoint Security Profile Settings**, set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.

    ![Endpoint Security Profile Settings with the Defender enforcement control set to On.](../img/intune-lab/intune-endpoint-security-enforcement-toggle.png)

1. Under **Compliance policy evaluation**, set **Connect Windows devices version 10.0.15063 and above to Microsoft Defender for Endpoint** to **On**.
1. Select **Save** and confirm the **Connector settings saved** notification.

    ![Intune connector toolbar with the Save button highlighted.](../img/intune-lab/intune-defender-connector-save.png)

    ![Intune notification confirming the connector settings were saved.](../img/intune-lab/intune-defender-connector-saved.png)

The enforcement setting allows eligible devices that are onboarded to Defender for Endpoint, but not enrolled in Intune, to receive endpoint security policies through the Defender for Endpoint management channel.

[Previous: Manage endpoint security in Microsoft Intune](01-manage-endpoint-security.md) | [Lab agenda](README.md) | [Next: Onboard devices](03-onboard-devices.md)
