# Prompt Caching: The One-Line Fix for Expensive RAG Systems

## The Hidden Cost of Repetition

You've built a RAG chatbot. It works great. Users love it. Then the Claude API bill arrives: $450.

Wait, what?

For a documentation bot that gets maybe 100 queries a day? Something's off.

Here's what's probably happening: you're sending the same context to the API repeatedly and paying full price each time. It's one of those things nobody mentions in the tutorials, but it's costing real money.

## The Pattern That Burns Money

Most RAG systems follow this flow:

1. User asks a question
2. System retrieves relevant docs (vector search, keyword matching, whatever)
3. Send those docs + the question to the LLM
4. Return the answer

Seems reasonable. Except here's the problem: **those docs don't change between requests.**

You're sending the same employee handbook, the same API documentation, the same knowledge base content with every single query. The LLM doesn't remember it from last time. You pay to reprocess it every time.

Think about it:
- Question 1: "How do I reset my password?" → Send 40KB of docs + question
- Question 2: "What's the support email?" → Send the same 40KB of docs + question
- 1,000 questions → Send the same docs 1,000 times

It's like hiring a consultant and making them re-read all the background materials before answering each question. Wasteful, but that's exactly what's happening.

## The Fix: Prompt Caching

Both Claude and OpenAI support prompt caching. The idea is simple: mark certain content as cacheable, and the API remembers it for a few minutes. Next request with the same content? Pull from cache instead of reprocessing.

Cache hits cost about 90% less than regular processing.

Here's what that looks like in code:

**Standard approach (expensive):**
```python
response = client.messages.create(
    model="claude-sonnet-4",
    messages=[{
        "role": "user",
        "content": f"{knowledge_base_docs}\n\nQuestion: {user_question}"
    }]
)
```

**With caching (much cheaper):**
```python
response = client.messages.create(
    model="claude-sonnet-4",
    messages=[{
        "role": "user",
        "content": [
            {
                "type": "text",
                "text": knowledge_base_docs,
                "cache_control": {"type": "ephemeral"}  # ← Cache this part
            },
            {"type": "text", "text": f"Question: {user_question}"}
        ]
    }]
)
```

That cache_control parameter tells Claude to remember the knowledge base content. For the next 5 minutes, any request with the same content reuses the cached version.

## The Math on Actual Savings

Let's run some simple numbers:

**Assumptions:**
• 100 queries per day (small-to-medium RAG system)
• 50,000 tokens of context per query (typical documentation)
• Claude pricing: $3 per million input tokens

**Without caching:**
• Daily tokens: 100 × 50,000 = 5 million tokens
• Daily cost: 5M × $3/M = **$15/day** = **$450/month**

**With caching:**
• Cache expires every 5 minutes
• First query in each 5-minute window: full price (cache write)
• Subsequent queries in the same window: 90% discount (cache hit)
• **Typical savings: 70-90%** depending on traffic patterns

For this example, if queries cluster during work hours, you'd likely see **$125-200/month** instead of $450.

**Real-world range: $300-400/month savings** for adding one parameter.

## When This Actually Matters

Prompt caching makes sense when you're:

**✅ Good use cases:**
• RAG systems with static knowledge bases
• Chatbots with long system prompts
• Code assistants (cache the repo, not the query)
• Multi-turn conversations (cache conversation history)

**❌ Not useful when:**
• Every prompt is unique
• Query volume is low (cache expires before reuse)
• Context changes constantly

If you're sending the same stuff repeatedly, you should be caching.

## Common Mistakes (And How to Avoid Them)

**Mistake 1: Caching the wrong content**

Don't cache what changes. Cache the stable stuff. Your knowledge base? Cache it. The user's question? Don't cache it.

**Mistake 2: Order matters**

Put cacheable content first. Cache boundaries are prefix-based - everything before the cache marker gets cached. If you put it at the end, it won't work.

**Mistake 3: Not monitoring cache hits**

The API returns cache statistics:
```python
response.usage.cache_creation_input_tokens  # How many tokens you cached
response.usage.cache_read_input_tokens      # How many came from cache
```

Log these. They tell you if caching is actually helping or if you're just adding complexity.

## The Bottom Line

Most LLM applications send the same context over and over. Without caching, you're paying full price every time. With caching, you pay once and reuse at 90% off.

It's not complicated. It's not new. But a lot of production systems aren't doing it.

Check your RAG system. Check your chatbot. If you're sending repeated content without caching, you're probably burning 70-90% more than you need to.

One parameter. Massive savings. No downside.

Worth five minutes to check.

---

#llm #costoptimization #claude #openai #rag #api #promptcaching #engineering
