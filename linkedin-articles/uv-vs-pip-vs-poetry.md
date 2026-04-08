# uv vs pip vs Poetry: Speed, Stability, or Features?

## Introduction

"Just use pip." "No, Poetry is better." "Have you tried uv? It's 100x faster!"

Every Python project starts with this debate. After managing dependencies across dozens of production systems, I've learned that asking "which is best?" is the wrong question. The right question is: "Which problem am I solving?"

## The Three Tools, Decoded

### pip: The Universal Constant

**When it wins:**
- You're inheriting a legacy project with requirements.txt
- Docker builds where you need guaranteed reproducibility
- Your CI/CD runs on a locked-down environment
- You're deploying to platforms where exotic tools aren't allowed

**Real example:** Our production deployments use pip in Dockerfiles. Why? Because in 2 AM incidents, you want zero surprises. pip is boring. Boring is good in production.

**The gotcha:** No native lock file support means you're managing requirements.txt manually. Pin everything or suffer version drift.

### Poetry: The Packager's Choice

**When it wins:**
- You're building a library for PyPI
- Your team needs deterministic builds across dev/staging/prod
- You want dependency resolution that actually works
- You're tired of juggling setup.py, requirements.txt, and MANIFEST.in

**Real example:** Every internal Python library we publish uses Poetry. poetry build, poetry publish - done. No wrestling with setuptools configuration.

**The gotcha:** Slower than paint drying. A cold install with 50 dependencies? Grab coffee. Also, the resolver is picky - it'll reject valid dependency sets that pip would happily install.

### uv: The Speed Demon

**When it wins:**
- CI/CD pipelines where build time = money
- Monorepos with dozens of services
- Local development when you install dependencies 20 times a day
- You're tired of waiting for Poetry

**Real example:** We switched our CI to uv. Build time dropped from 4 minutes to 25 seconds. That's 150 engineering hours saved per month across the team.

**The gotcha:** It's new (launched 2023). Some edge cases aren't covered. If you hit a bug, you're filing a GitHub issue, not finding a Stack Overflow answer from 2015.

## The Decision Tree I Actually Use

**Starting a new service?**
• Production-bound → pip (boring wins)
• Internal tool → uv (speed matters)
• Will iterate frequently → uv (local dev speed)

**Building a library?**
• Publishing to PyPI → Poetry (no contest)
• Internal-only → Poetry or uv (either works)

**Stuck with legacy?**
• Already using pip → keep using pip (migration cost > benefit)
• Already using Poetry → keep using Poetry
• Want faster CI → add uv alongside existing tool

**CI/CD optimization?**
• Use uv for installs, keep your existing tool for management

## The Hybrid Pattern That Works

Here's what most experienced teams actually do:

**Dockerfile (use pip for stability)**
```dockerfile
FROM python:3.11-slim
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
```

**CI pipeline (use uv for speed)**
```yaml
- name: Install dependencies
  run: |
    pip install uv
    uv pip install -r requirements.txt
```

**Library development (use Poetry for publishing)**
```bash
poetry build
poetry publish
```

**The lesson:** Use the right tool for each context. You're not married to one.

## What About Switching Costs?

**pip → Poetry:** Medium effort. Generate pyproject.toml from requirements.txt, test thoroughly.

**pip → uv:** Low effort. uv is largely a drop-in replacement for pip commands.

**Poetry → uv:** Low-medium effort. uv can read pyproject.toml, but you lose Poetry's publish workflow.

**The trap:** Don't switch just because something new appeared on Hacker News. Switch when you have a specific pain point: slow CI, manual lock file management, or publishing friction.

## Conclusion

Speed matters when you're iterating. Stability matters when you're deploying. Features matter when you're publishing.

• **pip** = boring stability (production deployments, Docker)
• **Poetry** = complete lifecycle (library publishing, complex deps)
• **uv** = blazing speed (CI/CD, monorepos, local dev)

The 100x speed of uv is real. But so is pip's decade of battle testing. And so is Poetry's publishing workflow.

Pick your problem first. Then pick your tool.

What's your current setup? Are you using just one tool or mixing them like we do?

---

#python #packaging #pip #poetry #uv #developertools #devops #dependencies
