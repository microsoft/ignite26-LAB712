---
ms.custom: msecd-doc-authoring-106
---

# Strengthen endpoint protection from onboarding to offboarding

In this lab, you use Microsoft Intune and Microsoft Defender for Endpoint to manage endpoint security settings, onboard devices, enable configuration protection, assign safe deployment channels, review effective settings, and offboard devices.

## 1. Manage devices with Defender for Endpoint that aren't enrolled in Intune

Enable Microsoft Defender for Endpoint security settings management. This capability lets you use Intune endpoint security policies to manage Defender settings on devices that aren't enrolled in Intune.

For more information, see [Use Intune to manage Microsoft Defender settings on devices that aren't enrolled with Intune](https://learn.microsoft.com/intune/device-security/microsoft-defender/security-settings-management).

### Connect Intune and Defender for Endpoint

1. Sign in to the [Microsoft Intune admin center](https://intune.microsoft.com/).
1. Go to **Endpoint security** > **Microsoft Defender for Endpoint**.
1. If the Defender connection isn't configured, select **Connect Microsoft Defender for Endpoint**.
1. Set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.
1. Select **Save**.

This setting allows eligible devices that are onboarded to Defender for Endpoint, but not enrolled in Intune, to receive endpoint security policies through the Defender for Endpoint management channel.

### Configure the enforcement scope

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
1. Go to **System** > **Settings** > **Endpoints**.
1. Under **General**, select **Configuration management**.
1. Open the **Enforcement scope** section.
1. Enable the platforms that you want Defender for Endpoint to manage, such as:
	 - Windows client devices
	 - Windows Server devices
	 - Windows Server domain controllers
	 - Linux devices
	 - macOS devices
1. For each applicable platform, select the scope option for your deployment, such as all eligible devices or a limited device scope.
1. Review options for devices managed by Configuration Manager or onboarded through Defender for Cloud.
1. Select **Save**.

Devices must be included in this enforcement scope before they can complete enrollment into Defender for Endpoint security settings management. If **Manage security settings using Configuration Manager** is enabled, devices with a Configuration Manager client are excluded from Defender for Endpoint security settings management. If it's disabled, eligible devices with the Configuration Manager client can receive policy through the Defender for Endpoint management channel.

## 2. Enable public preview features

Turn on public preview features so that you can use the new features included in this lab.

1. In the Microsoft Defender portal, go to **Settings** > **Endpoints** > **Optional features**.
1. Turn on **Preview features**.

## 3. Onboard devices

Onboard devices to Defender for Endpoint by using Intune or the Microsoft Defender portal.

For more information, see:

- [Use the Microsoft Defender deployment tool for Windows](https://learn.microsoft.com/defender-endpoint/defender-deployment-tool-windows)
- [Onboard Windows devices to Microsoft Defender for Endpoint by using Microsoft Intune](https://learn.microsoft.com/defender-endpoint/configure-endpoints-mdm)

### Create the onboarding package

1. In the Microsoft Defender portal, go to **Assets** > **Devices** > **Onboard**.
1. Under **Defender deployment tool (preview)**, select **Onboard**.
1. On the **Generate Defender deployment tool with an access key** page, enter a unique, descriptive package name, and then select **Generate**.
1. Copy and securely save the key. You can't access the key again after you leave the page.
1. Select **Download deployment tool**.
1. Copy the deployment tool executable to the device that you want to onboard.

### Run the onboarding package

Use either of the following methods:

- To use the executable, double-click it, select **Continue**, and paste the key when prompted.

	![Microsoft Defender deployment tool welcome screen with Continue and Cancel buttons.](../img/intune-lab/deployment-tool-welcome.png)

	![Defender deployment tool screen with an empty field for the deployment key.](../img/intune-lab/enter-deployment-key.png)

- To use the command line, open Command Prompt as an administrator and run:

	```console
	<package-name>.exe -key:"<onboarding-key>"
	```

	For a silent installation, append the `-quiet` parameter.

### Verify onboarding

Verify that the device appears in the Microsoft Defender portal, or review the deployment tool log:

```text
C:\ProgramData\Microsoft\DefenderDeploymentTool\DefenderDeploymentTool-<COMPUTERNAME>.log
```

The tool also records events in **Windows Logs** > **Application** with source **WDATPOnboarding**.

To view deployment packages, go to **Settings** > **Endpoints** > **Deployment packages** in the Microsoft Defender portal.

## 4. Enable configuration protection and sync policy

Configuration protection makes cloud-managed policy from Intune and Defender for Endpoint the authoritative source for Microsoft Defender Antivirus. Intune and Defender for Endpoint policies are enforced while conflicting settings from Group Policy, Configuration Manager, scripts, and local administrators are ignored.

Configuration protection differs from tamper protection. Tamper protection safeguards a limited set of critical settings by enforcing Microsoft-defined secure defaults. Configuration protection extends enforcement across a broader configuration surface, sets recommended security values, and enforces the settings defined by your organization.

For more information, see [Configuration protection in Microsoft Defender for Endpoint](https://learn.microsoft.com/defender-endpoint/secure-controlled-configuration).

Before you begin, confirm that the Windows device:

- Is onboarded to Defender for Endpoint.
- Is managed through Intune or Defender for Endpoint security settings management.

### Optional activity: Add a local antivirus exclusion before configuration protection

Use this activity to compare local administrator control before and after configuration protection is enabled, if time allows. If you skip it, continue to [Enable configuration protection](#enable-configuration-protection).

For this activity, use a Windows client lab device with the Windows Security app and the lab-provided local administrator account. Confirm that the device meets the [configuration protection prerequisites](https://learn.microsoft.com/defender-endpoint/secure-controlled-configuration#prerequisites), that configuration protection isn't already enabled, and that an existing policy doesn't disable local administrator merge.

> [!CAUTION]
> Antivirus exclusions reduce protection. Use only the provided lab device and the empty test folder specified here. Don't exclude a drive, a user profile, or folders containing applications or data. Don't turn off tamper protection or real-time protection to make this activity work.

1. Sign in to the Windows lab device with the lab-provided local administrator account.
1. In File Explorer, confirm that `C:\LAB712-AVExclusionTest` doesn't already exist, then create it as an empty folder. If it already exists, ask a proctor for help instead of reusing it.
1. Open **Windows PowerShell** as an administrator. Locate the latest installed Defender command-line tool and check the test folder:

    ```powershell
    $platform = Get-ChildItem -LiteralPath "$env:ProgramData\Microsoft\Windows Defender\Platform" -Directory -ErrorAction Stop |
        Sort-Object Name -Descending |
        Select-Object -First 1
    $mpCmdRun = Join-Path -Path $platform.FullName -ChildPath 'MpCmdRun.exe'
    & $mpCmdRun -CheckExclusion -Path 'C:\LAB712-AVExclusionTest'
    ```

    Confirm that the output says **is not excluded** and reports exit code **1** before you add the exclusion. If the tool isn't available, the command fails, or the folder is already excluded, ask a proctor to check the device. Don't treat a tool error as evidence that an exclusion is blocked.
1. Open **Windows Security** > **Virus & threat protection** > **Manage settings**. Under **Exclusions**, select **Add or remove exclusions**.
1. Select **Add an exclusion** > **Folder**, and select `C:\LAB712-AVExclusionTest`. Approve the administrator prompt if one appears.
1. In the same elevated PowerShell window, run the check again:

    ```powershell
    & $mpCmdRun -CheckExclusion -Path 'C:\LAB712-AVExclusionTest'
    ```

    **Expected result:** The output says **is excluded** and reports exit code **0**. You have demonstrated that the local administrator can add an effective antivirus exclusion before configuration protection is enabled.
1. In **Add or remove exclusions**, select only `C:\LAB712-AVExclusionTest` and select **Remove**. Run the check again and confirm **is not excluded**, with exit code **1**, so the next test starts without the exclusion.

Keep the empty folder and the PowerShell window open for the checks after policy application. If you can't add or remove the baseline exclusion, ask a proctor to check the existing policies; don't weaken device protection to force the expected result.

### Enable configuration protection

1. In the Microsoft Intune admin center, go to **Endpoint security** > **Antivirus** > **Create policy**.
1. Select **Windows** for the platform and **Windows Security Experience** for the profile.

	![Create a new policy pane with Windows selected as the platform and Windows Security Experience selected as the template.](../img/intune-lab/windows-security-experience-policy.png)

1. Enter a descriptive name for the policy, and then select **Next**.
1. Under **Configuration settings**, locate **Controlled Configuration (Device)** and select **Controlled Configuration (On)**.

	![Configuration settings page with Configuration Protection set to On.](../img/intune-lab/enable-configuration-protection.png)

1. Under **Assignments**, select the device groups that should receive the policy.
1. Review the settings and select **Create**.
1. Sync the test device or wait for its next policy check-in.

> [!IMPORTANT]
> Excluding a device or removing its policy assignment removes the value delivered by that policy.

### Optional activity: Verify that protection prevents a local exclusion

Complete this part only if you completed the baseline activity before enabling configuration protection.

1. Allow the configuration-protection policy to apply. In the Intune admin center, go to **All devices**, select the test device, and select **Sync** > **Yes**. On the device, run:

    ```powershell
    Get-MpComputerStatus | Select-Object AMProductVersion, ControlledConfigurationState, IsTamperProtected
    ```

    Confirm that **ControlledConfigurationState** reports configuration protection as enabled. You can also check the device's effective settings in the Defender portal, as described in [View effective settings](#6-view-effective-settings). Don't rely only on the policy being assigned, and don't continue until the device has applied it.
1. While still signed in as the local administrator, return to **Windows Security** > **Virus & threat protection** > **Manage settings** > **Add or remove exclusions**. Try to add the same folder, `C:\LAB712-AVExclusionTest`.
1. In the same elevated PowerShell window, check the result:

    ```powershell
    & $mpCmdRun -CheckExclusion -Path 'C:\LAB712-AVExclusionTest'
    ```

    **Expected result:** The local administrator can't create an effective exclusion. The UI might prevent the change, or a locally recorded change might be ignored. The check reports **is not excluded**, with exit code **1**. A UI entry alone isn't proof that an exclusion is honored.

    If the folder is still excluded, ask a proctor to verify the applied configuration-protection state, whether a cloud policy explicitly enables local administrator merge, and whether a centrally managed exclusion covers the folder. Don't disable protection to troubleshoot the activity.

With configuration protection enabled, local antivirus exclusions aren't honored by default. An organization can explicitly allow them through a cloud-managed local administrator merge policy while keeping configuration protection enabled.

### Optional extension: Allow local antivirus exclusions through policy

Use this extension only with the instructor's approval and only for the test-device group. Allowing local exclusions is an exception to the protected default, not a recommendation for all devices.

The lab-provided policy-management account needs Intune **Security baselines** permissions to read, create, update, and assign antivirus policies, scoped to the lab test devices. See [Role-based access control for endpoint security](https://learn.microsoft.com/intune/device-configuration/endpoint-security/manage-policies#role-based-access-control-for-endpoint-security). If your account can't sync devices or remove the temporary policy, ask a proctor to perform those actions.

1. Using the lab-provided policy-management account, open the [Microsoft Intune admin center](https://intune.microsoft.com/). Go to **Endpoint security** > **Antivirus** > **Create policy**.
1. Select **Windows** for the platform and **Microsoft Defender Antivirus** for the profile. Name the policy `LAB712 - Allow local antivirus exclusions`.
1. Under **Configuration settings**, find **Disable Local Admin Merge** and select **Enable local admin merge**. If the portal shows Boolean values, set **Disable Local Admin Merge** to **False**.

    The setting name is inverted: **False** enables local administrator merge; **True** disables it. With configuration protection enabled, leaving the setting **Not configured** doesn't explicitly allow local antivirus exclusions.
1. Leave unrelated settings unconfigured. Assign the policy only to the dedicated lab test-device group, then review and create it. If another assigned policy explicitly disables local administrator merge, ask a proctor to resolve the conflicting lab assignments before proceeding.
1. Sync the test device and wait for policy application. Confirm the merge setting and that configuration protection remains enabled:

    ```powershell
    Get-MpPreference | Select-Object DisableLocalAdminMerge
    Get-MpComputerStatus | Select-Object ControlledConfigurationState
    ```

    **Expected result:** **DisableLocalAdminMerge** is **False**, and configuration protection is still enabled.
1. On the device, repeat the Windows Security steps to add `C:\LAB712-AVExclusionTest` as a folder exclusion. Run the check again:

    ```powershell
    & $mpCmdRun -CheckExclusion -Path 'C:\LAB712-AVExclusionTest'
    ```

    **Expected result:** The output says **is excluded**, with exit code **0**. The cloud policy now allows the local antivirus exclusion without turning off configuration protection.

This exception applies to local antivirus exclusions. Locally defined attack surface reduction exclusions aren't honored under configuration protection, even when local administrator merge is enabled. For more information, see [Configuration protection enforcement](https://learn.microsoft.com/defender-endpoint/secure-controlled-configuration#how-configuration-protection-enforcement-works) and [Disable Local Admin Merge policy values](https://learn.microsoft.com/defender-endpoint/use-intune-config-manager-microsoft-defender-antivirus#disable-local-admin-merge).

### Clean up the optional exclusion activity

1. If you completed the merge-policy extension, remove the test exclusion while local administrator merge is still allowed. In **Windows Security** > **Add or remove exclusions**, select only `C:\LAB712-AVExclusionTest` and select **Remove**. Alternatively, in elevated PowerShell, run:

    ```powershell
    Remove-MpPreference -ExclusionPath 'C:\LAB712-AVExclusionTest'
    ```

1. Run the exclusion check and confirm **is not excluded**, with exit code **1**. If you skipped the merge-policy extension, remove any test entry that the UI recorded and verify the same result. If removal is blocked or you can't confirm cleanup, ask a proctor to reset the disposable lab device before continuing; don't turn off protection.
1. If you created the temporary merge policy, change **Disable Local Admin Merge** to **Disable local admin merge** (**True** in a Boolean UI), sync the device, and verify **DisableLocalAdminMerge** is **True**. Confirm that configuration protection remains enabled and the test folder isn't excluded. Work with the instructor to remove the temporary policy and its assignment when the lab is reset; leave the original configuration-protection policy unchanged.
1. Delete only the empty `C:\LAB712-AVExclusionTest` folder you created. If it contains files, stop and ask a proctor for help instead of deleting its contents.

| Checkpoint | Expected effective result |
|---|---|
| Before configuration protection, after adding the test exclusion | The folder is excluded. |
| After configuration protection, without a cloud policy allowing local administrator merge | The local attempt doesn't create an effective exclusion. |
| After explicitly allowing local administrator merge through policy | The local antivirus exclusion is honored while configuration protection stays enabled. |
| After cleanup | The test folder isn't excluded, and configuration protection remains enabled. |

For details about the verification tool, see [Verify whether a file or folder is excluded by using MpCmdRun](https://learn.microsoft.com/defender-endpoint/microsoft-defender-antivirus-exclusions-configure#verify-whether-a-file-or-folder-is-excluded-by-using-mpcmdrun).

## 5. Assign device groups to safe deployment channels

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

### Create and assign an SDP policy

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

## 6. View effective settings

Verify the resulting state of the settings by viewing the device's effective settings in the Microsoft Defender portal. Effective settings show the configuration enforced on the device, which helps administrators validate protection and troubleshoot conflicting sources.

For more information, see [Investigate devices in Microsoft Defender for Endpoint](https://learn.microsoft.com/defender-endpoint/investigate-machines).

1. Open the Microsoft Defender portal.
1. Go to **Assets** > **Devices**.
1. Search for and open the device that you want to review.
1. Select **Configuration management** > **Effective settings**.

	![Effective settings page for the fictitious example-device, showing Microsoft Defender Antivirus settings and effective values.](../img/intune-lab/effective-settings.png)

## 7. Offboard devices

The new SDP private preview experience allows you to enable or disable individual public preview features, giving administrators more deliberate control over feature adoption.

### Enable embedded offboarding

1. In the Microsoft Defender portal, go to **Settings** > **Endpoints** > **Preview features**.
1. Enable **Embedded offboarding experience**.
1. In the **Endpoints** area, go to **Offboarding** and select **Offboard**.

	![Endpoints offboarding page showing available offboarding methods.](../img/intune-lab/offboarding-options.png)

1. Under **Defender deployment tool**, select **Offboard**.

	![Defender deployment tool option on the Endpoints offboarding page.](../img/intune-lab/defender-deployment-tool-offboard.png)

### Create the offboarding package

1. On the **Generate Defender deployment tool with an offboarding key** page, enter a unique, descriptive package name.

	![Generate the Defender deployment tool page with fields for the package name, organization, and expiration.](../img/intune-lab/generate-offboarding-package.png)

1. Select **Generate**.
1. Copy and securely save the key. You can't access the key again after you leave the page.

	![Defender deployment package ready page with the offboarding key replaced by asterisks.](../img/intune-lab/offboarding-key-ready.png)

1. Select **Download deployment tool**. Select the executable or ZIP format based on your organization's needs.
1. Copy the deployment tool executable to the device that you want to offboard.

### Run the offboarding package

Use either of the following methods:

- To use the executable, double-click it, select **Continue**, and paste the key when prompted.
- To use the command line, open Command Prompt as an administrator and run:

	```console
	<package-name>.exe -offboard -key:"<offboarding-key>"
	```

	For a silent offboarding experience, append the `-quiet` parameter.

To view offboarding packages, go to **Settings** > **Endpoints** > **Deployment packages** in the Microsoft Defender portal.

![Deployment packages page with fictitious package, creator, and organization values.](../img/intune-lab/deployment-packages.png)

The deployment tool log is located at:

```text
C:\ProgramData\Microsoft\DefenderDeploymentTool\DefenderDeploymentTool-<COMPUTERNAME>.log
```

The tool also records events in **Windows Logs** > **Application** with source **WDATPOffboarding**.
