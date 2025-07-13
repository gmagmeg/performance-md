# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---
description: 
globs: 
alwaysApply: true
---

## Project Overview

This is a Marp presentation project for creating technical slides. The workflow involves:
1. Creating raw content in `input/` directory as `.txt` files
2. Converting content to Marp-formatted `.md` files in `output/` directory
3. Using custom CSS themes from `themes/` directory
4. Placing images in `.images/` directory

## Content Creation Rules

### File Naming Convention
- Input files: `input/XXXYYY.txt` (where XXX is sequence, YYY is topic code)
- Output files: `output/YYYYMMDD_topic_description.md` (date-based naming)
- Template reference: `@YYYYMMDD_template.md` (though template file doesn't exist yet)

### Content Constraints
- **Title**: Maximum 40 characters
- **Body text**: Maximum 50 characters per line
- **Total slide content**: Maximum 500 characters per slide
- **Maximum lines per slide**: 15 lines
- **Code blocks**: Maximum 20 lines per block
- **Images**: Maximum 2 per slide, maximum 800px width
- **Heading levels**: h1 to h3 only
- **Lists**: Maximum 3 levels of nesting
- **Tables**: Maximum 1 per slide

### Required Marp Front Matter
```yaml
---
marp: true
theme: custom
---
```

## Architecture

### Directory Structure
```
input/          # Raw content files (.txt)
output/         # Generated Marp presentations (.md)
themes/         # Custom CSS themes
.images/        # Image assets
resources/      # Additional resources
```

### Theme System
- Primary theme: `themes/custom.css`
- Brand colors: booost company colors (blue #00338D, green #27DB84)
- Custom classes available: `.lead`, `.inverse`, `.center`
- Table styling with branded headers and hover effects

### Content Processing Workflow
1. Write content in `input/` as structured text
2. Convert to Marp format with proper slide breaks (`---`)
3. Apply content constraints and formatting rules
4. Use custom theme for consistent branding
5. Place images in `.images/` directory and reference appropriately

## Development Guidelines

### When Creating New Presentations
1. Always start with content in `input/` directory
2. Use date-based naming for output files
3. Respect all content constraints (character limits, line limits, etc.)
4. Center-align images by default
5. Specify language for code blocks
6. Maintain existing slide layout patterns

### Theme Customization
- Modify `themes/custom.css` for styling changes
- Brand colors are defined in CSS variables
- Table styling follows specific pattern with branded headers
- Custom section classes available for different slide types

### Image Management
- Store all images in `.images/` directory
- Maximum 2 images per slide
- Maximum width 800px
- Default to center alignment

## Content Format Examples

### Basic slide structure:
```markdown
---
marp: true
theme: custom
---

## Slide Title

Content goes here

---

## Next Slide

More content
```

### Table format:
```markdown
| Item | Column 1 | Column 2 |
| --- | --- | --- |
| Row 1 | Data | Data |
```

Tables automatically get booost brand styling with blue headers.

## Commands and Build Process

### Current Workflow (Manual)
This project currently uses a manual workflow with no automated build system:

1. **Content Creation**: Write raw content in `input/` directory
2. **Manual Conversion**: Convert to Marp format in `output/` directory
3. **Presentation Generation**: Use Marp CLI or compatible viewer to generate slides

### Presentation Viewing
- Use Marp CLI: `marp output/main-presen.md` (if installed)
- Use Marp for VS Code extension for live preview
- Export to PDF/HTML: `marp output/main-presen.md --pdf` or `--html`

## Performance Testing Data Structure

The `keisoku-kekka/` directory contains structured performance testing results:
- `no-cache/`: Results without OPcache enabled
- `on-cache/`: Results with OPcache enabled, subdivided by server type
- `spike/`: Spike load testing results
- Each subdirectory contains JSON performance data and CSV memory usage data

### Performance Testing Architecture
- **Testing Tool**: k6 for load testing
- **Monitoring**: OpenTelemetry for profiling
- **Environments Tested**: Apache+PHP, Nginx+PHP-FPM, Swoole, FrankenPHP
- **Key Metrics**: Response times (P90, P95), memory usage, CPU utilization, error rates

## Key Architectural Decisions

### Theme System Architecture
- Single custom theme with CSS variables for brand consistency
- Responsive layout with logo positioning classes
- Special layouts: `.columns` for 2-column content, `.tech-stack` for technology grids
- Color scheme based on booost brand colors (blue #00338D, green #27DB84)

### Content Organization Strategy
- Input files use sequence-based naming (`XXXYYY.txt`) 
- Output files use date-based naming for chronological organization
- Performance data is categorized by testing scenario and server configuration
- Images organized by type (logos vs. content images)