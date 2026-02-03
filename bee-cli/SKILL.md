---
name: bee-cli
description: "Interact with Bee wearable AI data using the bee CLI tool. Use this skill when the user wants to: (1) Learn about the owner through their personal facts and captured conversations, (2) Access facts that Bee has learned about the user, (3) Read recent conversations and transcripts, (4) Search for relevant conversations on specific topics, (5) Sync Bee data to local markdown files, (6) Manage personal facts or todos, (7) Work with data from the Bee wearable device."
---

# Bee CLI

CLI client for Bee - the wearable AI that captures conversations and learns about you.

## About Bee

Bee is a wearable AI device that continuously captures and transcribes ambient audio from the owner's daily life. The device listens to conversations, meetings, phone calls, and any spoken interactions throughout the day, creating a comprehensive record of the owner's verbal communications and experiences.

### How Bee Works

Bee uses advanced speech recognition to transcribe all ambient audio in real-time. This includes:

- Face-to-face conversations with friends, family, and colleagues
- Business meetings and professional discussions
- Phone calls and video conferences
- Personal reflections and voice notes
- Overheard conversations in the owner's environment

From these transcriptions, Bee automatically extracts and learns facts about the owner - their preferences, relationships, work projects, commitments, and personal details mentioned in conversations.

### Privacy and Security

**Bee data is extremely sensitive.** The transcriptions contain intimate details of the owner's personal and professional life, including private conversations that were never intended to be recorded or shared.

**All Bee data is end-to-end encrypted and accessible only to the owner.** The encryption ensures that:

- Only the authenticated owner can access their conversation transcripts
- No third parties, including Bee's servers, can read the decrypted content
- The data remains private even if storage systems are compromised
- Access requires explicit authentication through the owner's credentials

**When working with Bee data, treat all information as highly confidential.** The owner has entrusted access to their most private conversations and personal details.

## When to Use This Skill

Use the Bee CLI skill when:

- **Learning about the owner**: Access facts that Bee has extracted from conversations to understand the owner's preferences, relationships, work, and personal details
- **Reading recent conversations**: Review transcripts of recent discussions to recall what was said or find specific information
- **Searching for relevant conversations**: Find past conversations on specific topics, with certain people, or about particular projects
- **Managing personal knowledge**: View, update, or organize the facts Bee has learned
- **Tracking commitments**: Access todos and action items extracted from conversations
- **Reviewing daily activity**: See summaries of each day's conversations and interactions

## Installation

Check if `bee` CLI is installed:
```bash
bee --version
```

If not installed, download from https://github.com/bluush-co/bee-cli/releases/latest

Select the binary for the current platform:
- macOS ARM: `bee-darwin-arm64`
- macOS Intel: `bee-darwin-amd64`
- Linux: `bee-linux-amd64`
- Windows: `bee-windows-amd64.exe`

Download and make executable:
```bash
# Example for macOS ARM
curl -L -o bee https://github.com/bluush-co/bee-cli/releases/latest/download/bee-darwin-arm64
chmod +x bee
sudo mv bee /usr/local/bin/
```

The binary can be used directly without additional installation steps.

## Authentication

Check authentication status:
```bash
bee status
```

If not authenticated, initiate login:
```bash
bee login --agent
```

This returns a URL. Provide the URL to the user and instruct them to open it in their browser to complete authentication. Wait for confirmation before proceeding with other commands.

## Commands

### Facts - Learn About the Owner

Facts are pieces of information Bee has learned about the owner from their conversations. This is the primary way to understand who the owner is, what they care about, and what's happening in their life.

List all facts:
```bash
bee facts list
```

**Confirmed vs Non-Confirmed Facts:**

Facts are categorized as either confirmed or non-confirmed:

- **Confirmed facts**: Explicitly verified by the owner or clearly stated in conversations. These are reliable and should be trusted.
- **Non-confirmed facts**: Inferred or extracted from context but not explicitly verified. These may be accurate but could also be misinterpretations.

When using facts, always prefer confirmed facts first. Non-confirmed facts can be used for speculation or additional context, but treat them as potentially inaccurate. If making decisions or providing information based on non-confirmed facts, acknowledge the uncertainty.

Facts include information like:
- Personal preferences ("prefers morning meetings", "allergic to peanuts")
- Relationships ("married to Sarah", "manager is John")
- Work details ("working on Project Atlas", "deadline is March 15")
- Interests and hobbies ("learning Spanish", "training for marathon")
- Contact information and personal details

Create a fact:
```bash
bee facts create --text "I prefer morning meetings"
```

Update a fact:
```bash
bee facts update <id> --text "Updated fact text"
```

Delete a fact:
```bash
bee facts delete <id>
```

### Conversations - Access Transcripts

Conversations are the raw transcripts of everything Bee has captured. Use these to find specific details, recall what was discussed, or search for information mentioned in past interactions.

List recent conversations:
```bash
bee conversations list
```

View a specific conversation transcript:
```bash
bee conversations show <id>
```

Conversation transcripts include:
- Full text of what was said
- Speaker identification when possible
- Timestamps and duration
- Location or context when available

### Search for Relevant Conversations

To find conversations about specific topics:

1. List conversations to see available transcripts
2. Review conversation summaries to identify relevant ones
3. View full transcripts of matching conversations

```bash
bee conversations list
bee conversations show <conversation-id>
```

### Todos - Track Commitments

Todos are action items and commitments extracted from conversations.

List todos:
```bash
bee todos list
```

Create a todo:
```bash
bee todos create --text "Buy groceries"
```

Update a todo:
```bash
bee todos update <id> --text "Updated todo" --completed
```

Delete a todo:
```bash
bee todos delete <id>
```

### Daily Summaries

View summaries of daily conversations and activities:
```bash
bee daily
```

View a specific date:
```bash
bee daily --date <YYYY-MM-DD>
```

### Sync Data to Markdown

Export all Bee data to local markdown files for offline access or integration with other tools:
```bash
bee sync
```

Options:
- `--output <dir>` - Output directory (default: ./bee-data)
- `--depth <n>` - How far back to sync

## Common Workflows

### Understanding the Owner

To learn about the owner and their context:
```bash
bee facts list
bee daily
bee conversations list
```

Review facts first to understand who they are, then check recent daily summaries and conversations for current context.

### Finding Information from Past Conversations

To find something mentioned in a past conversation:
```bash
bee conversations list
bee conversations show <relevant-conversation-id>
```

List conversations to find the relevant timeframe or topic, then view the full transcript.

### Export All Data for AI Context

Sync everything to markdown for comprehensive access:
```bash
bee sync --output ./my-bee-data
```

This creates markdown files for facts, todos, daily summaries, and conversation transcripts.
