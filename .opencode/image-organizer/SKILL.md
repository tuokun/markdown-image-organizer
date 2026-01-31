---
name: obsidian-image-organizer
description: Organize and manage images in Obsidian notes by moving them to specified folders, renaming them meaningfully based on context, and updating links. Also cleans up text formatting in Markdown files.
---

# Obsidian Image Organizer Skill

This skill enables agents to organize images in Obsidian notes by moving them to dedicated folders, renaming them with meaningful names based on their context in the document, updating the image links, and cleaning up text formatting.

## Overview

When working with Obsidian, images are often pasted with generic names like "Pasted image 20260130230732.png". This skill helps:
- Move images to organized folders (e.g., "附录图", "images", "assets")
- Rename images with meaningful names based on their context in the document
- Update image links in Markdown files to reflect new locations and names
- Clean up text formatting (remove extra blank lines, standardize code blocks, etc.)

## Prerequisites

Before using this skill, verify:
1. The target Markdown file exists
2. The destination folder exists or can be created
3. Images referenced in the document exist in the expected locations

## Usage Scenarios

Use this skill when:
- User asks to organize images in a note
- User wants to move images to a specific folder
- User wants to rename images with meaningful names
- User wants to clean up formatting in a Markdown file

## Step-by-Step Process

### Step 1: Analyze the Markdown File

Read the Markdown file to:
1. Identify all image links (Obsidian wikilinks format `![[image.png]]`)
2. Understand the context around each image
3. Note the current location of each image file

**Example:**
```markdown
举一个字符数组的例子，如图所示：

![[Pasted image 20260130230732.png]]
```

### Step 2: Generate Meaningful Names

For each image, analyze the surrounding text to generate a meaningful name:
- Look at the heading under which the image appears
- Look at the text immediately before the image
- Look at any descriptions or labels near the image

**Naming Convention:**
- Use the note name as prefix (e.g., "数组-")
- Use a descriptive suffix based on context (e.g., "字符数组示例.png")
- Keep names concise but descriptive
- Use Chinese for Chinese content

**Examples:**
- `Pasted image 20260130230732.png` → `数组-字符数组示例.png`
- `Pasted image 20260130230810.png` → `数组-删除元素移动.png`
- `Pasted image 20260130231442.png` → `数组-二维数组示例.png`

### Step 3: Move and Rename Images

For each image:
1. Verify the image exists in the current location
2. Move it to the destination folder with the new name
3. Verify the move was successful

**Example:**
```bash
mv "Pasted image 20260130230732.png" "附录图/数组-字符数组示例.png"
```

### Step 4: Update Image Links

Update all image links in the Markdown file to reference the new paths:
- Replace old wikilinks with new ones
- Use relative paths from the note's location
- Ensure the link syntax is correct

**Example:**
```markdown
# Before:
![[Pasted image 20260130230732.png]]

# After:
![[附录图/数组-字符数组示例.png]]
```

### Step 5: Clean Up Text Formatting

After updating links, clean up the Markdown file:
1. Remove excessive blank lines (more than 2 consecutive blank lines)
2. Standardize code blocks (use proper language identifiers)
3. Remove duplicate content
4. Ensure consistent heading levels
5. Fix inconsistent spacing

**Common Formatting Issues to Fix:**
- Extra blank lines between sections
- Inconsistent code block language identifiers (` ```text` instead of ` ```txt`)
- Duplicate paragraphs or sections
- Inconsistent heading hierarchy

## Implementation Example

### Complete Workflow

```python
# 1. Read the Markdown file
file_path = "蓝图/算法/数组.md"
content = read_file(file_path)

# 2. Extract all image links
images = extract_image_links(content)
# Returns: [
#   {"original": "Pasted image 20260130230732.png", "context": "字符数组的例子"},
#   {"original": "Pasted image 20260130230810.png", "context": "删除元素移动"},
#   ...
# ]

# 3. Generate new names
for image in images:
    new_name = generate_name(image["context"], "数组")
    image["new_name"] = new_name

# 4. Move images
for image in images:
    old_path = f"蓝图/算法/{image['original']}"
    new_path = f"蓝图/算法/附录图/{image['new_name']}"
    move_file(old_path, new_path)

# 5. Update links
for image in images:
    content = content.replace(
        f"![[{image['original']}]]",
        f"![[附录图/{image['new_name']}]]"
    )

# 6. Clean up formatting
content = clean_formatting(content)

# 7. Write updated content
write_file(file_path, content)
```

## Best Practices

### Naming Guidelines

1. **Keep it concise**: Avoid overly long names
2. **Be descriptive**: The name should clearly indicate what the image shows
3. **Use consistent prefixes**: Group related images with the same prefix
4. **Use appropriate language**: Match the language of the document content
5. **Avoid special characters**: Stick to alphanumeric, hyphens, and underscores

### Folder Structure Recommendations

```
笔记/
├── 文章.md
└── 附录图/
    ├── 文章-概念图.png
    ├── 文章-示例.png
    └── 文章-流程图.png
```

### Error Handling

Always verify:
1. The original image file exists before attempting to move
2. The destination folder exists before moving files
3. The move operation completed successfully
4. The links were updated correctly

## Supported Image Formats

- PNG (.png)
- JPEG (.jpg, .jpeg)
- GIF (.gif)
- SVG (.svg)
- WebP (.webp)

## Link Types Supported

### Obsidian Wikilinks
```markdown
![[image.png]]
![[folder/image.png]]
![[folder/image.png|alt text]]
```

### Markdown Links
```markdown
![alt text](image.png)
![alt text](folder/image.png)
```

## Advanced Features

### Batch Processing

You can process multiple files at once:
```python
for file_path in glob("**/*.md"):
    organize_images(file_path, "附录图")
```

### Custom Naming Functions

Define custom naming logic based on specific needs:
```python
def custom_naming_function(context, prefix):
    # Custom logic for generating names
    return f"{prefix}-{context}-{timestamp}.png"
```

### Link Validation

After updating links, verify they point to valid files:
```python
for link in extract_image_links(updated_content):
    if not file_exists(link):
        log_error(f"Broken link: {link}")
```

## Troubleshooting

### Issue: Image not found

**Cause**: Original image file doesn't exist in expected location
**Solution**: Use Glob to find the actual location of the image

### Issue: Links broken after update

**Cause**: Relative path calculation error
**Solution**: Verify the path is correct relative to the note's location

### Issue: Duplicate names

**Cause**: Generated names collide with existing files
**Solution**: Add a unique suffix or number to avoid conflicts

## Example Session

**User Request:**
"将 `蓝图/算法/数组.md` 文件中使用的图片全部移动至'附录图'文件夹中，并且保持文本图片的显示正常，同时修改图片的文件名称，使其符合文本链接意思"

**Agent Actions:**
1. Read `蓝图/算法/数组.md`
2. Extract image links and contexts
3. Generate meaningful names for each image
4. Move images to `蓝图/算法/附录图/` with new names
5. Update image links in the Markdown file
6. Clean up text formatting
7. Verify all images display correctly

## Related Skills

- **obsidian-markdown**: For general Obsidian Markdown syntax
- **obsidian-bases**: For managing Obsidian Bases
- **json-canvas**: For working with Canvas files

## References

- [Obsidian Image Embeds](https://help.obsidian.md/Embeds)
- [Obsidian Internal Links](https://help.obsidian.md/Links)
- [Wikilink Syntax](https://help.obsidian.md/How+to/Link+notes+and+files)
