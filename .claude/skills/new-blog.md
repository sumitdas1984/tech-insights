# New Blog Skill

Create a new blog post from a raw idea, following the established workflow.

## Usage

```
/new-blog "Your blog idea here"
```

## Instructions

When this skill is invoked:

1. **Extract the blog idea** from the arguments. If no argument provided, ask the user for their blog idea.

2. **Read the template** from `BACKLOG.md` to understand the structure for blog ideas.

3. **Generate a structured outline** based on the idea and template:
   - Create a compelling title
   - Identify target audience (tech leaders, developers, recruiters)
   - Define the core message/takeaway
   - Develop an outline with:
     - Opening hook/problem statement
     - 3-4 main points with supporting details
     - Practical examples or comparisons
     - Clear verdict/conclusion
   - Craft an attention-grabbing opening line
   - Suggest relevant tags

4. **Create the full blog post** in `posts/` directory:
   - Use the outline to write a complete, well-structured blog post
   - Include:
     - Engaging introduction with the hook
     - Clear sections for each main point
     - Code examples if relevant (reference from `code/` directory)
     - Comparison tables or lists where appropriate
     - Strong conclusion with call-to-action
   - Filename: Use kebab-case based on the title (e.g., `my-blog-title.md`)
   - Keep it concise (500-800 words for LinkedIn/Medium)

5. **Generate LinkedIn-compatible version** in `linkedin-posts/` directory:
   - Same filename as the original post
   - Convert unsupported elements:
     - Tables → Formatted bullet lists
     - Inline code backticks → Plain text
     - Code blocks → Keep simple, or convert to text if complex
     - Tags: Convert from \`tag\` format to #hashtag format
   - Keep only LinkedIn-supported markdown:
     - Headers (##, ###)
     - Bold/italic
     - Bullet lists
     - Links

6. **Show the user** both file paths and ask if they want to:
   - Add this idea to BACKLOG.md for future reference/tracking
   - Update INDEX.md with the new blog entry

## Key Principles

- **Concise**: Write short, punchy technical content suitable for LinkedIn/Medium
- **Practical**: Include real-world examples and actionable insights
- **Engaging**: Start with a hook, end with a question or call-to-action
- **Professional**: Leverage the user's 10+ years of software development experience
- **Personal brand**: Content should appeal to tech leaders, recruiters, and stakeholders

## Output

The skill should create:
1. `posts/[title].md` - Full blog post with all markdown features
2. `linkedin-posts/[title].md` - LinkedIn-compatible version

Then confirm completion and show the file paths.
