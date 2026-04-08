# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Technical blogging repository for creating short-form articles targeted at tech leaders, developers, and recruiters. Content is published on LinkedIn and Medium, focusing on software development, AI/ML, and related technologies.

## Architecture

### Dual-Format Workflow

This repository maintains two versions of each blog post:

1. **`posts/`**: Full markdown with tables, code blocks, all formatting
2. **`linkedin-posts/`**: LinkedIn-compatible version with restricted formatting

**Why dual format?** LinkedIn Articles don't support markdown tables, inline code backticks, or certain formatting. The linkedin-posts/ versions are pre-converted for direct copy-paste.

### Content Pipeline

```
BACKLOG.md (ideas) → posts/[title].md (full draft) → linkedin-posts/[title].md (platform-ready)
                                                    ↓
                                              INDEX.md (published tracking)
```

### Directory Structure

- `posts/` - Original blog drafts (full markdown capabilities)
- `linkedin-posts/` - LinkedIn-compatible versions (simplified formatting)
- `code/` - Python examples and code snippets referenced in posts
- `images/` - Visual assets and diagrams
- `BACKLOG.md` - Queue of blog ideas with structured template
- `INDEX.md` - Publication tracking (schedule: every Saturday, 4 blogs/month goal)

## Development Commands

### Python Environment

Uses `uv` for dependency management (Python 3.13+):

```bash
# Activate virtual environment
source .venv/bin/activate  # Unix
.venv\Scripts\activate     # Windows

# Install dependencies (if pyproject.toml updated)
uv sync
```

## Blog Creation Workflow

When user says **"new blog [idea]"** or **"create blog [idea]"**:

1. Generate structured outline using template from BACKLOG.md
2. Create full blog post in `posts/[title].md`:
   - 500-800 words
   - Hook → Main points → Practical examples → Conclusion
   - Include code examples from `code/` if relevant
   - Add tags in backtick format: `tag1` `tag2`
3. Generate LinkedIn version in `linkedin-posts/[title].md` with conversions:
   - Tables → Formatted bullet lists
   - Inline code `backticks` → Plain text
   - `` `tag` `` format → `#hashtag` format
   - Keep only: Headers (##), **bold**, *italic*, bullet lists, links
4. Confirm both file paths created

**Target audience:** Tech leaders and developers with 10+ years experience
**Writing style:** Concise, practical, thought leadership focused

## LinkedIn Format Restrictions

LinkedIn Articles support limited markdown:
- ✅ Headers (##), bold, italic, bullet lists, links
- ❌ Tables, inline code backticks, code blocks with syntax highlighting
- ❌ HTML tags, triple backtick blocks

When converting posts/ → linkedin-posts/, always apply these transformations.

## Publishing Workflow

1. Add idea to BACKLOG.md using structured template
2. Draft full post in posts/
3. Convert to linkedin-posts/
4. Update INDEX.md with publication date and status
5. Publish on Saturday (weekly schedule)
6. Update INDEX.md with link and mark as "Published"
