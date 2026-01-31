# Markdown Image Organizer

一个用于在 Markdown 文档中组织和管理图片的 Agent Skill。它可以智能地将图片移动到指定文件夹，根据上下文重命名图片，更新 Markdown 链接，并清理文本格式。适用于所有 Markdown 编辑器，包括 Obsidian、Typora、VS Code 等。

[English](docs/README_en.md)

## 功能特点

- **智能重命名**：根据文档上下文自动为图片生成有意义的名称
- **自动整理**：将图片移动到指定的文件夹（如"附录图"、"images"、"assets"）
- **链接更新**：自动更新 Markdown 文件中的图片链接
- **格式清理**：清理多余的空行、统一代码块格式等
- **批量处理**：支持一次性处理多个 Markdown 文件

## 适用场景

当你的 Markdown 文档（如 Obsidian 笔记、Typora 文档等）中包含大量粘贴的图片（通常名称如 `1.png`、`2.png`），并且希望：

- 将图片整理到专门的文件夹中
- 为图片添加有意义的文件名
- 保持图片链接的正确性
- 优化文档格式

## 使用方法

### 基本用法

当你在例如 OpenCode CLI 中加载此 skill 后，可以使用以下命令：

```bash
opencode skills load markdown-image-organizer
```

然后向 agent 提出请求，例如：

> 将 `一级目录/二级目录/数组.md` 文件中使用的图片全部移动至'附录图'文件夹中，并且保持文本图片的显示正常，同时修改图片的文件名称，使其符合文本链接意思

### 处理流程

1. **分析 Markdown 文件**：识别所有图片链接和上下文
2. **生成有意义的名称**：根据标题、前后文内容生成图片名称
3. **移动和重命名**：将图片移动到目标文件夹
4. **更新链接**：更新 Markdown 文件中的图片链接
5. **清理格式**：优化文档格式

### 命名规则

图片名称采用以下格式：`[文档名称]-[描述性文字].png`

例如：
- `1.png` → `数组-字符数组示例.png`
- `2.png` → `数组-删除元素移动.png`

## 安装

### 前置要求

- OpenCode CLI
- Node.js 18+ 或 Bun

### 安装步骤

```bash
git clone https://github.com/tuokun/markdown-image-organizer.git
cd markdown-image-organizer
```

将 `skills/markdown-image-organizer/SKILL.md` 文件复制到你的 skills 目录中。

#### opencode目录结构示例

```bash
git clone https://github.com/tuokun/markdown-image-organizer.git
cd markdown-image-organizer
```

项目已包含 `.opencode/skills/markdown-image-organizer/` 示例目录结构，你可以直接在当前目录运行 OpenCode CLI：

```bash
opencode skills load .opencode/skills/markdown-image-organizer
```

这种方式展示了 OpenCode skills 的标准目录结构，便于理解和维护。

## 文件结构

```
markdown-image-organizer/
├── skills/
│   └── markdown-image-organizer/
│       └── SKILL.md          # 核心技能定义文件
├── docs/
│   └── README_en.md          # 英文文档
├── README.md                 # 中文文档
└── LICENSE                   # Apache 2.0 许可证
```

## 支持的图片格式

- PNG (.png)
- JPEG (.jpg, .jpeg)
- GIF (.gif)
- SVG (.svg)
- WebP (.webp)

## 支持的链接类型

- Wikilinks: `![[image.png]]`
- Markdown 链接: `![alt text](image.png)`
- 带路径的链接: `![[folder/image.png]]` 或 `![alt text](folder/image.png)`

## 示例

### 输入文档

```markdown
# 数组

举一个字符数组的例子，如图所示：

![[1.png]]

删除元素时的移动过程：

![[2.png]]
```

### 输出结果

```markdown
# 数组

举一个字符数组的例子，如图所示：

![[附录图/数组-字符数组示例.png]]

删除元素时的移动过程：

![[附录图/数组-删除元素移动.png]]
```

图片文件结构：
```
一级目录/
├── 二级目录/
│   ├── 数组.md
│   └── 附录图/
│       ├── 数组-字符数组示例.png
│       └── 数组-删除元素移动.png
```

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

本项目采用 Apache 2.0 许可证 - 详见 [LICENSE](LICENSE) 文件
