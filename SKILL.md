---
name: x-to-obsidian
description: Save X/Twitter posts and articles to Obsidian vault. Use when user asks to save, extract, or archive X/Twitter content (posts, threads, articles) to their Obsidian notes library. Handles content extraction, image URLs (pbs.twimg.com format), and proper frontmatter formatting with empty tags array.
---

# SKILL

Save X/Twitter posts and articles to Obsidian vault with proper formatting.

## Configuration

Before using this skill, set your Obsidian vault path in the skill below:

**Edit this file** and replace `YOUR_OBSIDIAN_VAULT` with your actual vault path:

```yaml
## Configuration

- **Obsidian vault**: `~/Documents/ObsidianVault`
  # Change to: `~/Documents/my-vault` or `/Users/yourname/Documents/vault`
```

## Workflow

### 1. Open the Post

```bash
AGENT_BROWSER_NAV_DELAY_MS=2000 agent-browser open "<url>"
```

### 2. Extract Content

```bash
# Get page structure
agent-browser snapshot

# Get all image URLs from pbs.twimg.com
agent-browser eval "Array.from(document.querySelectorAll('img[src*=\"pbs.twimg.com\"]')).map((img, i) => \`\${i+1}. \${img.src}\`).join('\\n')"
```

### 3. Parse Post Information

Extract from the snapshot:
- **Author**: Name and handle (@username)
- **Content**: Post text/thread content
- **Images**: All pbs.twimg.com URLs
- **Metadata**: Date, engagement metrics (replies, reposts, likes)

### 4. Save to Obsidian

**File path**: `~/Documents/ObsidianVault/{auto-generated-filename}.md`

**Frontmatter format**:

```yaml
---
tags: []
aliases: []
url: <post_url>
author: <name @handle>
date: YYYY-MM-DD
source: X (Twitter)
created: YYYY-MM-DD
modified: YYYY-MM-DD
---
```

> [!IMPORTANT] Frontmatter Rules
> - `tags` must be empty array: `tags: []`
> - Do not add any tags to the tags field
> - Include created and modified timestamps

### 5. Image Format

**Critical**: Use `pbs.twimg.com` URLs only.

```markdown
![description](https://pbs.twimg.com/media/G-XXXX?format=jpg&name=medium)
```

- ❌ Wrong: `https://x.com/user/article/123/media/456`
- ✅ Correct: `https://pbs.twimg.com/media/G-XXXX?format=jpg&name=medium`

### 6. Content Formatting

- Use **multi-level headings** (#, ##, ###)
- Use **Obsidian Callouts** for important info
- **No `---` separators** in content (only in frontmatter)
- Use **tables** for structured data
- **Internal links**: Use Obsidian wiki link syntax `[[filename]]` for vault notes
- **External links**: Use standard markdown `[text](url)` for external resources

**Link examples**:

```markdown
- [[Related Note]]
- [[Another Note]]
- [External Documentation](https://example.com)
```

**Callout examples**:

```markdown
> [!INFO] Post Information
> - **Author**: Name @handle
> - **Date**: YYYY-MM-DD

> [!TIP] Tip
> Tip details

> [!WARNING] Warning
> Warning details
```

## Example Usage

### Quick Trigger (快捷触发)

When user says "保存 + x.com链接", directly call this skill:

User says:
- "保存 https://x.com/user/status/123"
- "保存这个: https://x.com/..."

### Standard Usage

User says:
- "Save this X post: https://x.com/user/status/123"
- "Save this tweet to Obsidian"
- "Extract the content from this post"

## File Naming

Auto-generate based on content:
- Short posts: `{author}-{date}.md`
- Long posts/articles: `{topic_summary}-{author}.md`
- Threads: `{topic}-thread-{author}.md`

## Installation

1. Copy `x-to-obsidian/` folder to `~/.claude/skills/`
2. Edit `SKILL.md` and set your Obsidian vault path
3. Restart Claude Code
4. Use by saying: "Save this X post: [url]"
