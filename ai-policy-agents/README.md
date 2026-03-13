# AI Policy Briefing Agent — Setup Guide

Build your own AI-powered news briefing agent using Claude Code. This tool scans Canadian news sources for AI policy developments and generates a concise briefing note.

## What's in this kit

| File | Description |
|------|-------------|
| `example-brief.md` | Sample briefing note output (March 6, 2026) |
| `SKILL.md` | The skill file that powers the `/brief` command |
| `README.md` | This setup guide |

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) installed and authenticated
- A terminal (macOS Terminal, iTerm2, Windows Terminal, etc.)

## Setup (5 minutes)

### Step 1: Create the skill directory

Open your terminal and run:

```bash
mkdir -p ~/.claude/skills/brief
```

### Step 2: Copy the skill file

Copy `SKILL.md` into the directory you just created:

```bash
cp SKILL.md ~/.claude/skills/brief/SKILL.md
```

Or if you downloaded this kit to your Downloads folder:

```bash
cp ~/Downloads/ai-policy-agents/SKILL.md ~/.claude/skills/brief/SKILL.md
```

### Step 3: Verify it's in place

```bash
cat ~/.claude/skills/brief/SKILL.md
```

You should see the skill file contents with the `---` frontmatter at the top.

### Step 4: Launch Claude Code

```bash
claude
```

Type `/brief` and it should appear in the autocomplete. If it doesn't, try starting a new session.

## Usage

**General AI policy scan:**
```
/brief
```

**Topic-focused scan:**
```
/brief AI sovereignty
/brief compute infrastructure
/brief AI regulation copyright
/brief AI workforce and talent
```

The agent will:
1. Search CBC, Globe and Mail, BetaKit, and The Logic for recent AI news
2. Read the most relevant articles
3. Synthesize a briefing note with 3-5 key takeaways
4. Save the output as a markdown file on your Desktop

## Customizing the skill

The `SKILL.md` file is just a text file — you can edit it to change the behaviour.

### Change the news sources

Edit the source list in the Instructions section. For example, to add Reuters:

```
- Reuters (reuters.com)
```

### Change the topic focus

Swap "Canadian AI policy" for any policy area. For example, change the guidelines to focus on climate policy, health policy, or defence.

### Change the output format

Edit the Output Format section to match whatever structure works for you. Want a shorter brief? Cut it to 3 takeaways. Want more detail? Add an "Analysis" section.

### Change where it saves

Edit the save path in Step 4 of the Instructions. Replace `~/Desktop/` with any folder you prefer.

## Troubleshooting

**"/brief" returns "Unknown skill"**
- Make sure the file is at exactly `~/.claude/skills/brief/SKILL.md`
- Check that the filename is `SKILL.md` (case-sensitive)
- Try starting a fresh Claude Code session

**Some news sources return errors**
- Paywalled sites (The Logic) may not return full content — that's normal
- National Post blocks the web crawler — it's excluded by default
- The agent will note which sources it couldn't access

**Output is too long or too short**
- Edit `SKILL.md` and change the guidelines (e.g., "MAX 3 takeaways" or "MAX 7 takeaways")

## How it works

The skill file is a prompt template that Claude Code reads when you type `/brief`. It tells Claude to:

1. Use `WebSearch` to find recent articles on each news site
2. Use `WebFetch` to read the full content of key articles
3. Synthesize everything into the briefing format
4. Save the result as a markdown file

The `$ARGUMENTS` placeholder gets replaced with whatever you type after `/brief`. So `/brief AI sovereignty` passes "AI sovereignty" as the topic focus.

## Going further

Some ideas for extending this:

- **Add more sources** — Financial Post, Policy Options, IRPP, Brookfield Institute
- **Schedule it** — Run Claude Code with a script to generate a brief every morning
- **Change the policy area** — Swap AI for climate, health, defence, or trade
- **Add email delivery** — Use a Gmail MCP integration to email the brief to yourself
- **Compare across countries** — Add international sources and track how Canada's approach differs
