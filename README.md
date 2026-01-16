# README

> Save X/Twitter posts and articles to your Obsidian vault with proper formatting and image links.

A [Claude Code](https://claude.ai/claude-code) skill that automates saving X/Twitter posts to your Obsidian vault. Extracts content, images, and metadata while applying consistent formatting.

## Features

- ✅ **Auto-extract** post content and metadata
- ✅ **Correct image URLs** using `pbs.twimg.com` format
- ✅ **Proper formatting** with Obsidian Callouts and structure
- ✅ **Clean frontmatter** with empty tags array
- ✅ **One-command usage** - just provide the URL

## Prerequisites

1. [Claude Code](https://claude.ai/claude-code) installed
2. [agent-browser](https://github.com/BUNotesAI/agent-browser-userdata) installed globally:
   ```bash
   npm install -g agent-browser
   agent-browser install
   ```

## Installation

### Quick Install

1. Copy `x-to-obsidian/` folder to `~/.claude/skills/`

2. Edit `SKILL.md` and configure your Obsidian vault path:
   ```bash
   nano ~/.claude/skills/x-to-obsidian/SKILL.md
   ```

   Find and replace:
   ```diff
   - **Obsidian vault**: `~/Documents/ObsidianVault`
   + **Obsidian vault**: `~/Documents/my-vault`
   ```

3. Restart Claude Code

## Usage

### Basic Usage

Simply tell Claude Code to save an X post:

```
Save this X post: https://x.com/user/status/123456
```

```
Archive this tweet to Obsidian
```

```
Extract the content from this thread
```

### What It Does

1. Opens the X post using agent-browser
2. Extracts post content, author info, and metadata
3. Gets all image URLs in correct `pbs.twimg.com` format
4. Creates a properly formatted markdown file in your Obsidian vault
5. Applies Obsidian formatting (headings, callouts, tables)

### Output Format

```markdown
---
tags: []
aliases: []
url: https://x.com/user/status/123456
author: John Doe @johndoe
date: 2026-01-16
source: X (Twitter)
created: 2026-01-16
modified: 2026-01-16
---

# Post Title

> [!INFO] Post Information
> - **Author**: John Doe @johndoe
> - **Date**: 2026-01-16

Post content goes here...

![Image](https://pbs.twimg.com/media/G-XXXX?format=jpg&name=medium)
```

## Image Format

**Critical**: X's images are hosted on `pbs.twimg.com`, not `x.com`.

| Format | Status |
|--------|--------|
| `https://pbs.twimg.com/media/G-XXXX?format=jpg&name=medium` | ✅ Correct |
| `https://x.com/user/article/123/media/456` | ❌ Wrong |

This skill automatically extracts the correct format.

## Formatting Standards

Saved posts follow these Obsidian formatting rules:

| Rule | Description |
|------|-------------|
| **Empty tags** | `tags: []` - no auto-tagging |
| **Multi-level headings** | Proper # ## ### structure |
| **No separators** | No `---` in content body |
| **Callouts** | Use `> [!TYPE]` for highlights |
| **Internal links** | `[[Note Name]]` for vault links |
| **External links** | `[Text](url)` for web links |

## File Naming

Auto-generated based on content type:

- Short posts: `{author}-{date}.md`
- Long posts: `{topic}-{author}.md`
- Threads: `{topic}-thread-{author}.md`

## Configuration

Edit `SKILL.md` to customize:

| Setting | Default | Description |
|---------|---------|-------------|
| Obsidian vault | `~/Documents/ObsidianVault` | Your vault path |
| Navigation delay | 2000ms | Delay between browser actions |

## Example Output

Input:
```
Save this X post: https://x.com/user/status/123
```

Output:
- File created: `~/Documents/ObsidianVault/topic-author.md`
- Content extracted with proper formatting
- All images using `pbs.twimg.com` URLs
- Frontmatter with metadata

## Troubleshooting

### Images not displaying

Ensure images use `pbs.twimg.com` format, not `x.com` URLs.

### Wrong save location

Edit `SKILL.md` and set your correct Obsidian vault path.

### Skill not triggering

Restart Claude Code after installing the skill.

## Contributing

Contributions are welcome! Feel free to open issues or submit PRs.

## License

MIT License - feel free to use and modify for your needs.

## Acknowledgments

Built with [skill-creator](https://github.com/anthropics/skill-creator) template.
Powered by [agent-browser](https://github.com/BUNotesAI/agent-browser-userdata).
