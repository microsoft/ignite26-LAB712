# Prepare to present LAB712

Use this guide to prepare the speakers and proctors for **Manage endpoint protection with Microsoft Intune and Defender**. Attendees should start with the [lab instructions](../instructions/README.md).

## Review the preparation status

The supplied excerpt from the **Ignite LAB712 Weekly Working Session** confirms the responsibilities and follow-ups below. It skips from 1:02 to 21:59, so it isn't a complete record of the meeting. It doesn't confirm that the Skillable environment is available, tested, or ready for delivery.

| Follow-up | Responsibility | Status in the supplied excerpt |
|---|---|---|
| Confirm Skillable provisioning status with Jen and Tim, and obtain the current environment link | Jodi Dyer offered to reply to the existing email thread and close the loop | Pending confirmation |
| Arrange a technical walkthrough if needed | Coordinate with Jen; Jamie noted that a Skillable technical resource can be made available | Available on request, not confirmed as scheduled |
| Walk through the environment after its availability is confirmed | Lorena Mora requested an initial walkthrough | Pending environment confirmation |
| Review the talk track and rehearse the attendee experience | Lorena Mora proposed a separate speaker check-in with Swapna after her return | Proposed, not confirmed as scheduled |

Don't treat an earlier temporary environment link as the final attendee entry point. Confirm the current link and handoff with the lab owner and Skillable contacts before delivery. Don't publish temporary access links, lab credentials, deployment keys, or tenant identifiers in this repository.

## Confirm team responsibilities

These roles reflect the supplied meeting excerpt. Confirm any later changes before delivery.

| Responsibility | Team members |
|---|---|
| Lab owner | Jodi Dyer |
| Intune narrative and messaging coverage | Chris Sorensen, partnering with Claire |
| Microsoft Defender for Endpoint narrative and messaging | Claire |
| Lab development | Jody Cedola and Sinclaire Hamilton |
| Speakers | Lorena Mora and Swapna |
| Proctors | Jamie Detwiler and Al |

Only first names were provided for Claire, Swapna, and Al in the excerpt. Don't infer their full names or assume Claire and Sinclaire are the same person.

## Prepare the introductory slides

Use the [LAB712 introductory PowerPoint](slides/LAB712-context-Ignite-2026.pptx). It uses the master, theme, and built-in layouts from the Microsoft Ignite PowerPoint supplied from the meeting chat, rather than the previous custom layout.

- Use the seven visible slides for the attendee introduction. The core talk track is **5:30**; optional prompts on slides 2, 3, and 5 extend it to **7 minutes**.
- Review the talk track and source references in the speaker notes. The final, hidden slide is for presenter preparation, not attendee delivery.
- Confirm the speakers and proctors before introductions. The lab owner, messaging reviewers, and lab developers aren't automatically session speakers.
- Keep the introduction short so attendees have time for the six activities. The [lab agenda](../instructions/README.md#follow-the-lab-activities) uses a five-minute introduction estimate; rehearse the actual deck and adjust pacing within the 75-minute session.
- Remove internal preparation notes, internal source links, and the hidden slide before distributing the deck externally. Hiding a slide doesn't remove its contents.

Applying the supplied template doesn't establish final content, accessibility, or event-design approval.

## Rehearse in the confirmed environment

After the lab owner confirms environment availability:

1. Open the confirmed attendee environment and verify access to both the Microsoft Intune admin center and the Microsoft Defender portal with the lab-provided accounts.
1. Complete the [prerequisite checks and six activities](../instructions/README.md) in order, using only lab-provided test devices.
1. Verify feature availability, onboarding, policy assignment, synchronization, and the results on the test device. Don't assume an assigned policy has applied.
1. Check configuration protection in **Effective settings** and deployment-channel placement separately in the safe deployment dashboard.
1. Complete any optional exclusion cleanup before offboarding. Verify the offboarding steps as part of the walkthrough.
1. Rehearse the talk track with the speakers. Agree on the key messages, portal handoffs, pacing, and how to support attendees who follow closely or work independently.
1. Confirm how the proctors will help attendees who need assistance or join late.
1. Record the walkthrough results and unresolved issues in the team's coordination thread. Confirm readiness with the lab owner before reporting the lab as ready.

The meeting excerpt doesn't change the technical steps in the six exercise pages. Those steps still need to be verified in the confirmed Skillable environment.
