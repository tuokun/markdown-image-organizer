# Markdown Image Organizer

An Agent Skill for organizing and managing images in Markdown documents. It intelligently moves images to specified folders, renames them based on context, updates Markdown links, and cleans up text formatting. Compatible with all Markdown editors including Obsidian, Typora, VS Code, and more.

[中文文档](../README.md)

## Features

- **Smart Renaming**: Automatically generates meaningful image names based on document context
- **Automatic Organization**: Moves images to specified folders (e.g., "appendix", "images", "assets")
- **Link Updates**: Automatically updates image links in Markdown files
- **Format Cleanup**: Removes extra blank lines, standardizes code blocks, and more
- **Batch Processing**: Process multiple Markdown files at once

## Use Cases

When your Markdown documents (such as Obsidian notes, Typora documents, etc.) contain many pasted images (usually named like `1.png`, `2.png`) and you want to:

- Organize images into dedicated folders
- Give images meaningful filenames
- Maintain correct image links
- Optimize document formatting

## Usage

### Basic Usage

After loading this skill in for example OpenCode CLI, use:

```bash
opencode skills load image-organizer
```

Then make requests to the agent, for example:

> Move all images in the `folder-one/folder-two/arrays.md` file to the 'appendix' folder, maintain proper image display, and rename image files to match their context in the text.

### Processing Flow

1. **Analyze Markdown File**: Identify all image links and their context
2. **Generate Meaningful Names**: Create image names based on headings, surrounding text
3. **Move and Rename**: Move images to target folders
4. **Update Links**: Update image links in Markdown files
5. **Clean Format**: Optimize document formatting

### Naming Convention

Image names follow this format: `[Document Name]-[Description].png`

For example:
- `1.png` → `arrays-char-array-example.png`
- `2.png` → `arrays-delete-element-movement.png`

## Installation

### Prerequisites

- OpenCode CLI
- Node.js 18+ or Bun

### Installation Steps

```bash
git clone https://github.com/tuokun/markdown-image-organizer.git
cd markdown-image-organizer
```

Copy the `skills/image-organizer/SKILL.md` file to your skills directory.

### OpenCode Directory Structure Example

```bash
git clone https://github.com/tuokun/markdown-image-organizer.git
cd markdown-image-organizer
```

The project already includes the `.opencode/image-organizer/` example directory structure. You can run OpenCode CLI directly in the current directory:

```bash
opencode skills load .opencode/image-organizer
```

This approach demonstrates the standard OpenCode skills directory structure for better understanding and maintenance.

## Project Structure

```
markdown-image-organizer/
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

- Wikilinks: `![[image.png]]`
- Markdown links: `![alt text](image.png)`
- Links with paths: `![[folder/image.png]]` or `![alt text](folder/image.png)`

## Example

### Input Document

```markdown
# Arrays

Here's an example of a character array:

![[1.png]]

The movement process when deleting elements:

![[2.png]]
```

### Output Result

```markdown
# Arrays

Here's an example of a character array:

![[appendix/arrays-char-array-example.png]]

The movement process when deleting elements:

![[appendix/arrays-delete-element-movement.png]]
```

Image file structure:
```
folder-one/
├── folder-two/
│   ├── arrays.md
│   └── appendix/
│       ├── arrays-char-array-example.png
│       └── arrays-delete-element-movement.png
```

## Contributing

Issues and Pull Requests are welcome!

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](../LICENSE) file for details
