## Before you're done

This repo has been created for your Microsoft Ignite 2026 session. Here's how to get it ready.

**Easiest path — use the agent (recommended):**

- Open GitHub Copilot Chat and say `help me initialize repo`. The agent will walk you through getting the README populated.
- When you're ready to publish, say `help me finalize repo`. The agent will clean up unused folders, validate everything, and remove this "Before you're done" section and other extra stuff that attendees don't need to see.
- Curious how it works? Read the [agent workflow](.github/AGENT-WORKFLOW.md).

**Doing it manually?**

Fill in the sections below yourself, then:

- Delete any placeholder folders you don't need (`data/`, `infra/`, etc.)
- Delete this "Before you're done" section
- Delete `.github/agents/`, `.github/tests/`, `.github/copilot-instructions.md`, and `.github/AGENT-WORKFLOW.md` — these are template tooling, not part of your published repo

**Folder conventions:**

- Attendee step-by-step guidance goes in `instructions/`. If you use MkDocs or a docs site instead, put it in `docs/` and link to it from this README.
- Reference material and background reading go in `docs/`.
- You can add a `.devcontainer/` folder if needed.

---

<a name="start-building"></a>

<p align="center">
<img src="img/banner-ignite-26.png" alt="Microsoft Ignite 2026" width="100%"/>
</p>

# [Microsoft Ignite 2026](https://ignite.microsoft.com)

## 🔥LAB712: Manage Endpoint Protection with Microsoft Intune and Defender
### Session description

Add your session description here. Keep it concise — 2-3 sentences about what attendees will learn and why it matters.

### 🚀 Getting started

#### In a guided session

If you're following along during a live session:

1. Step 1
2. Step 2
3. Open [`instructions/`](instructions/README.md) when this session includes
   attendee step-by-step guidance

Section 1  – Manage devices with MDE that are not onboarded to Intune
Enable Microsoft Defender for Endpoint security settings management. This capability lets us use Intune endpoint security policies to manage Defender settings on devices that are not enrolled in Intune.
Reference: Learn about using Intune to manage Microsoft Defender settings on devices that aren't enrolled with Intune - Microsoft Intune | Microsoft Learn
First, we’ll connect Intune and Defender and configure the management scope. .
1.	Sign in to the Microsoft Intune admin center. 
2.	Go to Endpoint security > Microsoft Defender for Endpoint. 
3.	If the Defender connection has not already been configured, select Connect Microsoft Defender for Endpoint. 
4.	Set Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations to On. 
5.	Select Save.
This setting allows eligible devices that are onboarded to Defender for Endpoint, but not enrolled in Intune, to receive endpoint security policies through the MDE management channel.
Next, we’ll identify which devices should use security settings management.
1.	Sign in to the Microsoft Defender portal.
2.	Go to System > Settings > Endpoints.
3.	Under General, select Configuration management.
4.	Open the Enforcement scope section.
5.	Enable the platforms you want MDE to manage, such as: 
o	Windows client devices
o	Windows Server devices
o	Windows Server domain controllers
o	Linux devices
o	macOS devices
6.	For each applicable platform, select the available scope option appropriate for your deployment, such as all eligible devices or a limited device scope.
7.	Review any options related to devices managed by Configuration Manager or onboarded through Defender for Cloud.
8.	Select Save.

Devices must be included in this enforcement scope before they can complete enrollment into MDE security settings management. If Manage security settings using Configuration Manager is enabled, devices with a Configuration Manager client are excluded from MDE security settings management. If it’s disabled, eligible devices with the Configuration Manager client can receive policy through the MDE management channel.


#### On your own

If you're learning at your own pace:

1. Clone this repository
2. Set up your environment
3. Follow the session guidance in [`instructions/`](instructions/README.md), or
   use the linked docs-site entry point when this repository uses that pattern

### 🎯 Learning outcomes

By the end of this session, you will be able to:

- Outcome 1
- Outcome 2
- Outcome 3

### 💻 Technologies used

- Technology 1
- Technology 2
- Technology 3

### 📚 Continue your learning

Pick your next step based on your learning style:

| Resource | What you'll get |
|----------|-----------------|
| **[Ignite 2026 Next Steps](https://aka.ms/ignite26-next-steps)** | Additional session repos and materials from Microsoft Ignite 2026 |
| **[Microsoft AI Skills Navigator](https://aka.ms/ignite26-asn)** | Discover AI skills, learning paths, and resources for your next step |
| **[Microsoft Learn](https://aka.ms/ignite26-learn)** | Official documentation and guided learning paths on these topics |
| **[Microsoft Foundry Community](https://aka.ms/MicrosoftFoundryDiscord-Ignite26)** | Connect with other learners and experts in our Discord community |

### 🌟 Microsoft Learn MCP Server

<!-- Remove this section if the Microsoft Learn MCP Server is not relevant to the session. -->

The Microsoft Learn MCP Server gives your AI agent direct access to Microsoft's official documentation — grounded, up-to-date answers about the topics in this session.

**GitHub Copilot CLI** — Install with:

```shell
copilot plugin install microsoftdocs/mcp
```

**VS Code** — One-click install:  
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Microsoft_Learn_MCP-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=microsoft-learn&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Flearn.microsoft.com%2Fapi%2Fmcp%22%7D)

For more information, visit the [Learn MCP Server repo](https://aka.ms/learnmcp).

### 👥 Content owners

<!-- TODO: Add yourself as a content owner
1. Change the src in the image tag to {your github url}.png
2. Change INSERT NAME HERE to your name
3. Change the github url in the final href to your url. -->

<table>
<tr>
    <td align="center"><a href="http://github.com/yourGitHubHandle">
        <img src="https://github.com/yourGitHubHandle.png" width="100px;" alt="INSERT NAME HERE"/><br />
        <sub><b>INSERT NAME HERE</b></sub></a><br />
            <a href="https://github.com/yourGitHubHandle" title="talk">📢</a>
    </td>
</tr></table>

### ⚖️ Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow [Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general). Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.

Any use of third-party trademarks or logos are subject to those third-party's policies.
