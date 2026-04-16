---
layout: post
title: "Learning with Agents"
---
![agent learning](/assets/b400-9670-e7e6-cdfe.png)

## Project Idea and Testing Ground

Agents don’t just generate code — they adapt to how you work. If you capture that learning, future outputs get better.

I ran a simple session with Copilot to generate a small Python script to rename blog images into hashed filenames. The goal was both to create the hashing script and to test whether agent learning can be formalized and reused across projects.

The session evolved through multiple iterations — refining structure, expectations, and workflow. Toward the end, I asked the agent to summarize what it had learned about my development style.

## Experiment Results

Instead of raw conversation history, I forced a distilled output — something reusable by future agents (e.g. `SKILLS.md` or a similar specification file).

This is what I was given:

- Use git and commit frequently  
- Mention AI/agent contribution in `README.md`  
- Provide simple execution via shell/launcher scripts  
- Keep repositories production-ready and public-safe  
- Include clear documentation, a license, and supporting files  
- Handle edge cases (e.g. quoted paths, preserve file extensions)

Copilot also indicated it created `/memories/repo/expectations.md` with key development expectations — I’ll review that separately.

## Takeaway

Agents can externalize preferences into reusable specifications.

Repository: https://github.com/drkaziu/simple-image-hash
