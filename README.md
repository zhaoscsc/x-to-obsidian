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

---

# 中文说明

## 简介

> 将 X/Twitter 帖子和文章自动保存到你的 Obsidian 笔记库，格式完美。

这是一个 [Claude Code](https://claude.ai/claude-code) Skill，可以自动将 X 上的帖子和文章保存到 Obsidian，同时提取内容、图片和元数据，并应用统一的格式规范。

## 功能特点

- ✅ **自动提取**帖子的内容和元数据
- ✅ **正确图片链接**使用 `pbs.twimg.com` 格式
- ✅ **规范格式**包含 Obsidian Callout 和结构
- ✅ **清洁 Frontmatter** tags 为空数组
- ✅ **一行命令使用**只需提供 URL

## 前置要求

1. 已安装 [Claude Code](https://claude.ai/claude-code)
2. 全局安装 [agent-browser](https://github.com/BUNotesAI/agent-browser-userdata)：
   ```bash
   npm install -g agent-browser
   agent-browser install
   ```

## 安装

### 快速安装

1. 将 `x-to-obsidian/` 文件夹复制到 `~/.claude/skills/`

2. 编辑 `SKILL.md` 配置你的 Obsidian vault 路径：
   ```bash
   nano ~/.claude/skills/x-to-obsidian/SKILL.md
   ```

   找到并替换：
   ```diff
   - **Obsidian vault**: `~/Documents/ObsidianVault`
   + **Obsidian vault**: `~/Documents/my-vault`
   ```

3. 重启 Claude Code

## 使用方法

### 快捷触发（推荐）

当你说"保存 + x.com链接"时，Claude 会自动调用此 skill：

```
保存 https://x.com/user/status/123456
```

```
保存这个: https://x.com/user/status/123456
```

### 基本用法

直接告诉 Claude Code 保存 X 帖子：

```
保存这个 X 帖子: https://x.com/user/status/123456
```

```
把这个 tweet 保存到 Obsidian
```

```
提取这个 thread 的内容
```

### 它会做什么

1. 使用 agent-browser 打开 X 帖子
2. 提取帖子内容、作者信息和元数据
3. 获取所有图片链接（正确格式）
4. 在你的 Obsidian vault 中创建格式化的 markdown 文件
5. 应用 Obsidian 格式（标题、callout、表格）

### 输出格式

```markdown
---
tags: []
aliases: []
url: https://x.com/user/status/123456
author: 张三 @zhangsan
date: 2026-01-16
source: X (Twitter)
created: 2026-01-16
modified: 2026-01-16
---

# 帖子标题

> [!INFO] 帖子信息
> - **作者**: 张三 @zhangsan
> - **日期**: 2026-01-16

帖子内容...

![图片](https://pbs.twimg.com/media/G-XXXX?format=jpg&name=medium)
```

## 图片格式

**关键点**：X 的图片托管在 `pbs.twimg.com`，而不是 `x.com`。

| 格式 | 状态 |
|------|------|
| `https://pbs.twimg.com/media/G-XXXX?format=jpg&name=medium` | ✅ 正确 |
| `https://x.com/user/article/123/media/456` | ❌ 错误 |

这个 Skill 会自动提取正确的格式。

## 格式规范

保存的帖子遵循以下 Obsidian 格式规则：

| 规则 | 说明 |
|------|------|
| **空标签** | `tags: []` - 不自动添加标签 |
| **多级标题** | 正确的 # ## ### 结构 |
| **无分割线** | 内容主体不使用 `---` |
| **Callout** | 使用 `> [!TYPE]` 高亮重要信息 |
| **内部链接** | 使用 `[[笔记名]]` 引用 vault 中的笔记 |
| **外部链接** | 使用 `[文本](url)` 链接网页 |

## 文件命名

根据内容类型自动生成：

- 短帖子：`{作者}-{日期}.md`
- 长帖子/文章：`{主题}-{作者}.md`
- Thread：`{主题}-thread-{作者}.md`

## 配置

编辑 `SKILL.md` 自定义：

| 设置 | 默认值 | 说明 |
|------|--------|------|
| Obsidian vault | `~/Documents/ObsidianVault` | 你的 vault 路径 |
| 导航延迟 | 2000ms | 浏览器操作之间的延迟 |

## 输出示例

输入：
```
保存这个 X 帖子: https://x.com/user/status/123
```

输出：
- 文件创建：`~/Documents/ObsidianVault/主题-作者.md`
- 内容已格式化
- 所有图片使用 `pbs.twimg.com` URL
- 包含元数据的 Frontmatter

## 常见问题

### 图片无法显示

确保图片使用 `pbs.twimg.com` 格式，而不是 `x.com` URL。

### 保存位置不对

编辑 `SKILL.md` 设置正确的 Obsidian vault 路径。

### Skill 不触发

安装 Skill 后重启 Claude Code。

## 贡献

欢迎贡献！随时可以提 Issue 或提交 PR。

## 许可证

MIT License - 可以自由使用和修改。

## 致谢

基于 [skill-creator](https://github.com/anthropics/skill-creator) 模板构建。
由 [agent-browser](https://github.com/BUNotesAI/agent-browser-userdata) 提供支持。
