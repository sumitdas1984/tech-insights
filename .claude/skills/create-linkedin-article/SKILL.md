---
name: create-linkedin-article
description: Create a LinkedIn-publishable article directly from a topic idea, with proper LinkedIn formatting built in.
---

When the user invokes this skill with a topic idea:

1. **Generate structured outline** using the template from BACKLOG.md
2. **Create LinkedIn-ready article** directly in `linkedin-articles/[title].md` with:
   - Engaging introduction with hook
   - Clear sections for main points
   - Practical examples/comparisons
   - Strong conclusion with CTA
   - 500-800 words
   - LinkedIn-compatible formatting throughout
   - Hashtags at the end (#hashtag format)
3. **Confirm** the file path created

## Content Guidelines

- **Audience**: Tech leaders, developers, recruiters (10+ years experience level)
- **Style**: Concise, practical, engaging
- **Format**: Hook → Main points → Practical examples → Conclusion
- **Length**: 500-800 words
- **Personal brand**: Showcase expertise, thought leadership

## LinkedIn Formatting Requirements

**Use these elements:**
- ✅ Headers: ## Heading
- ✅ Bold: **bold text**
- ✅ Italic: *italic text*
- ✅ Bullet lists: - item
- ✅ Numbered lists: 1. item
- ✅ Links: [text](url)
- ✅ Hashtags: #hashtag (at the end of article)

**Do NOT use these elements:**
- ❌ Markdown tables (use formatted bullet lists instead)
- ❌ Inline code backticks: `like this` (use plain text)
- ❌ Code blocks: ```language```
- ❌ Blockquotes with special formatting
- ❌ Tag format with backticks: `tag` (use #hashtag)

## Formatting Examples

**Instead of tables, use formatted bullets:**
```
**Feature Comparison:**
- **Speed**: Tool A is fast, Tool B is moderate
- **Cost**: Tool A is $10/month, Tool B is free
- **Ease of use**: Tool A has a learning curve, Tool B is beginner-friendly
```

**Instead of inline code, use plain text with formatting:**
```
To install the package, run npm install in your terminal
```

**For technical terms, use bold or italics:**
```
The **dependency injection** pattern helps manage complex applications.
```

**For tags, use hashtags at the end:**
```
#python #datascience #machinelearning #ai
```

## Article Structure Template

```
[Engaging hook - personal story, provocative question, or surprising stat]

## The Challenge

[Describe the problem your audience faces]

## Main Point 1

[Your first key insight with practical example]

## Main Point 2

[Your second key insight with practical example]

## Main Point 3 (optional)

[Your third key insight with practical example]

## Conclusion

[Summarize key takeaways and call-to-action]

[Hashtags]
```

## Key Differences from Blog Posts

- No code examples with syntax highlighting (describe code instead)
- Use conversational formatting over technical markdown
- Optimize for LinkedIn's reader (shorter paragraphs, more whitespace)
- Focus on personal insights and experiences
- Include clear CTA for engagement (comments, shares, connections)
