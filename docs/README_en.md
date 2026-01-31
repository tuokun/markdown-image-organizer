# Obsidian Image Organizer Skill

An OpenCode Agent Skill for organizing and managing images in Obsidian notes. It intelligently moves images to specified folders, renames them based on context, updates Markdown links, and cleans up text formatting.

[中文文档](../README.md)

## Features

- **Smart Renaming**: Automatically generates meaningful image names based on document context
- **Automatic Organization**: Moves images to specified folders (e.g., "附录图", "images", "assets")
- **Link Updates**: Automatically updates image links in Markdown files
- **Format Cleanup**: Removes extra blank lines, standardizes code blocks, and more
- **Batch Processing**: Process multiple Markdown files at once

## Use Cases

When your Obsidian notes contain many pasted images (usually named like `Pasted image 20260130230732.png`) and you want to:

- Organize images into dedicated folders
- Give images meaningful filenames
- Maintain correct image links
- Optimize document formatting

## Usage

### Basic Usage

After loading this skill in OpenCode CLI, use:

```bash
opencode skills load image-organizer
```

Then make requests to the agent, for example:

> Move all images in the `蓝图/算法/数组.md` file to the '附录图' folder, maintain proper image display, and rename image files to match their context in the text.

### Processing Flow

1. **Analyze Markdown File**: Identify all image links and their context
2. **Generate Meaningful Names**: Create image names based on headings, surrounding text
3. **Move and Rename**: Move images to target folders
4. **Update Links**: Update image links in Markdown files
5. **Clean Format**: Optimize document formatting

### Naming Convention

Image names follow this format: `[Note Name]-[Description].png`

For example:
- `Pasted image 20260130230732.png` → `数组-字符数组示例.png`
- `Pasted image 20260130230810.png` → `数组-删除元素移动.png`

## Installation

### Prerequisites

- OpenCode CLI
- Node.js 18+ or Bun

### Installation Steps

```bash
git clone https://github.com/your-username/image-organizer.git
cd image-organizer
```

Copy the `skills/image-organizer/SKILL.md` file to your OpenCode skills directory.

## Project Structure

```
image-organizer/
├── skills/
│   └── image-organizer/
│       └── SKILL.md          # Core skill definition file
├── docs/
│   └── README_en.md          # English documentation
├── README.md                 # Chinese documentation
└── LICENSE                   # Apache 2.0 license
```

## Supported Image Formats

- PNG (.png)
- JPEG (.jpg, .jpeg)
- GIF (.gif)
- SVG (.svg)
- WebP (.webp)

## Supported Link Types

- Obsidian Wikilinks: `![[image.png]]`
- Markdown links: `![alt text](image.png)`
- Links with paths: `![[folder/image.png]]`

## Example

### Input Document

```markdown
# 数组

举一个字符数组的例子，如图所示：

![[Pasted image 20260130230732.png]]

删除元素时的移动过程：

![[Pasted image 20260130230810.png]]
```

### Output Result

```markdown
# 数组

举一个字符数组的例子，如图所示：

![[附录图/数组-字符数组示例.png]]

删除元素时的移动过程：

![[附录图/数组-删除元素移动.png]]
```

Image file structure:
```
数组/
├── 数组.md
└── 附录图/
    ├── 数组-字符数组示例.png
    └── 数组-删除元素移动.png
```

## Contributing

Issues and Pull Requests are welcome!

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](../LICENSE) file for details
