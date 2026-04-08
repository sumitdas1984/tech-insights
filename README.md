# Technical Blogging

## Purpose

This repository serves as a centralized workspace for managing technical blog content focused on software development, AI/ML, and related technologies. With over 10 years of software development experience, I'm leveraging this platform to:

- **Build Personal Brand**: Create thought leadership content that resonates with tech leaders, recruiters, and industry stakeholders
- **Share Technical Insights**: Write and publish short-form technical articles on platforms like Medium and LinkedIn
- **Organize Content Pipeline**: Maintain a structured backlog of blog ideas, drafts, and published articles
- **Streamline Publishing**: Manage all aspects of blog creation from ideation to publication in one place

This repository helps me establish visibility in the tech community and showcase expertise to key decision-makers while contributing valuable insights to the developer ecosystem.

## Structure

```
.
├── linkedin-articles/  # LinkedIn-ready articles (optimized formatting)
├── code/               # Python code examples and snippets
├── images/             # Images, diagrams, and visual assets
├── INDEX.md            # Catalog of published articles with status
├── BACKLOG.md          # Queue of blog ideas and topics to write about
├── CLAUDE.md           # Project instructions and available skills
├── pyproject.toml      # Python project configuration
└── README.md           # This file
```

## Usage

**Create LinkedIn Article:**
```bash
/create-linkedin-article [topic idea]
```

This will:
- Generate a structured outline from BACKLOG.md template
- Create a LinkedIn-ready article in `linkedin-articles/`
- Use proper LinkedIn formatting (no code blocks, no tables, hashtags)
- Ready to copy/paste directly to LinkedIn

**Additional workflows:**
1. Add code examples in `code/`
2. Store images and diagrams in `images/`
3. Track published articles in `INDEX.md`
