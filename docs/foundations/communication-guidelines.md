# Communication Guidelines

This document defines rules and best practices for managing work-related communication in messenger apps.

---

## Table of Contents

- [1. General Principles](#1-general-principles)
- [2. Telegram Guidelines](#2-telegram-guidelines)
  - [2.1 Chat Structure](#21-chat-structure)
  - [2.2 Naming Conventions & Profile Rules](#22-naming-conventions--profile-rules)
  - [2.3 Message Etiquette](#23-message-etiquette)
  - [2.4 Tags & Message Formatting](#24-tags--message-formatting)
  - [2.5 Chat Types](#25-chat-types)
  - [2.6 Chat Naming Format](#26-chat-naming-format)
  - [2.7 Pinned Message Template](#27-pinned-message-template)
  - [2.8 Emergency Contact Table](#28-emergency-contact-table)
  - [2.9 Notification Rules](#29-notification-rules)
  - [2.10 Message Retention & Chat Lifecycle Policies](#210-message-retention--chat-lifecycle-policies)
    - [2.10.1 Message Editing & Deletion Policy](#2101-message-editing--deletion-policy)
    - [2.10.2 Archiving Inactive Chats](#2102-archiving-inactive-chats)
  - [2.11 Roles & Responsibilities](#211-roles--responsibilities)
- [3. FAQ / Tips](#3-faq--tips)
  - [3.1 What to do if no one replies in chat?](#31-what-to-do-if-no-one-replies-in-chat)
  - [3.2 Should I write directly to someone or in a group chat?](#32-should-i-write-directly-to-someone-or-in-a-group-chat)
  - [3.3 Is it okay to ping @all/@channel?](#33-is-it-okay-to-ping-allchannel)
  - [3.4 How to Start a New Project Chat](#33-is-it-okay-to-ping-allchannel)

---

## 1. General Principles

- Use appropriate channels for each topic.
- Be concise, clear, and respectful in communication.
- Mention people directly when expecting a response.
- Acknowledge messages (emoji, short reply) to show you've seen it.
- Link to related tasks, documents, or decisions for clarity.
- Use threads or reply functions to preserve conversation context.
- Avoid flooding channels — use designated FLOOD or social chats.
- Be responsive during working hours or inform if unavailable.
- Be mindful of time zones in distributed teams.
- Prefer async communication where possible; sync only when necessary.
- Default to group chats for transparency, unless the topic is private.
- Escalate through other channels only when absolutely necessary.

---

## 2. Telegram Guidelines

### 2.1 Chat Structure

1. **One chat — one topic**  
   Each project or team should have a **dedicated chat**.

2. **Noise reduction**
- Use  **announcement channels** for read-only important updates (e.g. infrastructure, releases).
- Use FLOOD chats for informal talks.
- Use sync groups for temporary focused discussions.
- Use additional topic-based groups for specific domains or sub-teams (e.g. QA, DevOps).

---

### 2.2 Naming Conventions & Profile Rules

- All participants in work-related chats must:
  - Use their **real first and last name**.
  - Set a **real, clear profile photo**.
  - Use a **clear @username** (e.g., @john_smith instead of @dragonking1987).

---

### 2.3 Message Etiquette

- Start messages with an appropriate **tag** (see below).
- Always **mention specific people** when requesting a response or review.
- Be respectful and avoid excessive sarcasm or jokes in work chats.
- Use threads (if supported) or reply function to maintain conversation context.

---

### 2.4 Tags & Message Formatting
Use standardized **message tags**:

| Tag         | Usage                                      |
|-------------|--------------------------------------------|
| `#bug`      | Bug reports or issue discussions           |
| `#review`   | Review requests or feedback discussions    |
| `#release`  | Release-related updates                    |
| `#test`     | QA-ready tasks                             |
| `#issue`    | Urgent blockers or risks                   |
| `#announcement` | Major updates or news                  |
| `#idea`     | Proposals or improvement suggestions       |

**Example**  
`#bug Preview not loading on Safari @john Please check browser compatibility.`

---

### 2.5 Chat Types

| Type                    | Purpose                                                       |
|-------------------------|---------------------------------------------------------------|
| **Feature/Project Chats** | Discussion and coordination for specific functionality         |
| **Functional Chats**      | Focused on a discipline: frontend, backend, devops, etc.       |
| **Role-Based**            | Based on responsibility: `pm`, `leads`, `owners`              |
| **Sync Groups**           | Temporary real-time decision-making spaces                    |
| **Announcement Channels** | Read-only channels for official announcements                |
| **FLOOD Chats**           | Informal chats for memes, social discussions, or side topics  |
| **Topic-Based Group Chats** | Group chats with topic threads enabled (for large teams)     |
| **Team-Based Chats**      | Dedicated to specific team units (e.g., `blockchain-team`)     |


---

### 2.6 Chat Naming Format

```
[Team|Project] - [Scope|Role] - [Topic]
```

**Examples:**
- `core - frontend - bugs`
- `hr - general - announcements`
- `mobile - design - review`

---

### 2.7 Pinned Message Template

```md
This chat is dedicated to coordination and collaboration for the [Project Name] team.  
Please follow the guidelines below to ensure productive communication.

**Purpose:**  
Discussion of tasks, bugs, releases, and team coordination related to the project/module.

**Chat Moderator:**  
[@username] — responsible for maintaining order, answering chat-related questions, and resolving disputes.

**Use tags to categorize messages:**
#bug – bug reports or investigations  
#review – code review requests or discussions  
#release – release planning or updates  
#test – when a task is ready for testing  
#issue – any blockers or general concerns  
#announcement – important notices (e.g., team/process changes)  
#idea – suggestions and improvement proposals

**Message Format:**
- Always **tag the topic** at the beginning of your message.
- **Mention (@username)** people directly when action or feedback is expected.

**Example:**  
`#bug Login fails after timeout @alex Please check error logs`

**Daily syncs:** [Optional – add if used, e.g., 10:00 UTC]  
For non-work topics, please use the dedicated FLOOD chat.

Let’s keep this space clean and professional.
```

---

### 2.8 Emergency Contact Table

It is recommended to maintain a shared contact sheet (e.g., Google Sheet) with the following columns:

| First Name | Last Name | Telegram Nick | Phone        | Backup Phone | Email              | Location     | Timezone | Emergency Contact       | Department       | Position      | Employment Type | First Work Day | Supervisor         |
|------------|-----------|----------------|--------------|---------------|--------------------|--------------|----------|--------------------------|------------------|---------------|------------------|----------------|---------------------|
| John       | Doe       | @john_doe      | +9876543210  | +1234567890  | john@company.com   | Berlin, Germany  | UTC+2    | +1122334455 (Brother) | Blockchain Team | Developer | Full-time        | 2007-04-01     | Alice Smith |

This table helps identify alternative ways to reach a team member if they’re unavailable for an extended period.

---

### 2.9 Notification Rules

- **Mute by default**: If you're not actively participating in a chat, mute notifications to reduce noise.
- **@channel and @all** – only for critical updates or releases. Avoid overusing these mentions.
- **@mention** – always mention specific people when a message requires their response.
- Consider creating channels with limited notification scope for less urgent messages.

---

### 2.10 Message Retention & Chat Lifecycle Policies

#### 2.10.1 Message Editing & Deletion Policy

To maintain a transparent and accountable communication environment:

- **Editing messages** is allowed within the first 15 minutes for quick corrections (e.g., typos, broken links).
- **Deleting messages** should be avoided unless absolutely necessary (e.g., sensitive info shared by mistake).
- Edited or deleted messages should be acknowledged in a follow-up message if relevant for team context.
- **Pinned messages** (e.g., project rules or meeting links) should only be edited by the chat owner or moderator.

> Messages used in task discussions, release planning, or escalations should not be deleted.

---

### 2.10.2 Archiving Inactive Chats

To reduce noise and clutter, teams are encouraged to regularly review and archive unused chats.

#### When to archive:
- No messages in the last 2–3 sprints.
- The project/initiative has been completed or cancelled.
- The chat has been replaced by another (e.g., new project structure).

#### Archiving process:
1. Notify participants: "This chat will be archived due to inactivity."
2. Pin a summary message with relevant handover links.
3. Rename the group to `[archived] project-name`.
4. Remove the chat from pinned/favorites (optional).
5. Archive the chat.

> You can still access archived chats in Telegram if needed.

---


### 2.11 Roles & Responsibilities

| Role              | Responsibilities                                                       | Can Create Chats |
|-------------------|------------------------------------------------------------------------|------------------|
| **Team Lead**     | Organize team-specific and project chats, maintain clarity             | +                |
| **Project Manager** | Create and manage chats for cross-functional work and coordination  | +                |
| **Moderators**    | Help with pinning rules, managing discussions                          | +                |
| **Engineers/Designers** | Participate, follow guidelines, report issues                    | - (by request)   |
| **HR/Operations** | Manage company-wide channels, onboarding chats                         | +                |

> For critical channels (e.g., `announcements`), only designated roles may post or modify content.


---

## 3. FAQ / Tips

### 3.1 “What to do if no one replies in chat?”
- Wait a reasonable time before following up (typically 1–2 hours during working hours, depending on your team’s or company’s agreed responsiveness norms). Each team may define its own expected response window.
- Tag a specific person responsible for the topic (e.g., `@nickname`).
- If it's urgent, escalate through an alternative channel (e.g., call, team lead ping, emergency contacts).
- Check if the question is already answered in documentation, Notion, or pinned messages.

### 3.2 “Should I write directly to someone or in a group chat?”
- Prefer group chats for transparency and knowledge sharing.
- Use direct messages only for private or personal matters.

### 3.3 “Is it okay to ping @all/@channel?”
- Use **@channel** only for critical or time-sensitive messages (e.g., release blocker, broken production).
- Prefer tagging specific people to reduce noise.

### 3.4 How to Start a New Project Chat
Follow these steps to create a structured and well-managed chat (Step-by-step):
1. Define the purpose and audience of the chat.
2. Use a clear and consistent **naming format**.
3. Set a pinned message using the provided template.
4. Add relevant members (team leads, developers, QA, PM, etc).
5. Enable Topics in Telegram if you expect parallel threads.
6. Add chat to the shared team directory or communication board.