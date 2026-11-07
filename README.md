# agentic-ai-lab
Hands-on AI agent learning with free tools: Hugging Face smolagents, local models, and Colab. Includes a documented attempt at multi-agent systems.
# Multi-Agent Attempt: Batman Filming Locations Map (Not Working Yet)

**Status:** Not working. Multi-agent setup with a free local model did not complete.

## Goal
Build a multi-agent system (manager agent + web search agent) that finds Batman filming locations and supercar factories, calculates cargo plane transfer time from Gotham, and plots the results on a world map with plotly.

Based on the Hugging Face Agents Course, Unit 2 (smolagents, multi-agent systems).

## What's in this folder
- `notebook.ipynb`: the Google Colab notebook with all attempts.
- `README.md`: this file.

## What I built
- `calculate_cargo_travel_time`: a tool using the haversine formula to estimate flight time (+10% detour, +1 hour takeoff/landing).
- A `web_agent` (DuckDuckGo search + page visiting) managed by a `manager_agent`.

## What went wrong
1. **Missing dependency:** `DuckDuckGoSearchTool` needs `ddgs`, which wasn't in the first install line. Fixed with `pip install ddgs`.
2. **Blocked import:** The manager tried `import plotly.express`, which the sandbox blocked. It was only allowed `plotly`. Fix: add `"plotly.express"` to `additional_authorized_imports`.
3. **Too slow:** On a free Colab T4 with `Qwen2.5-Coder-1.5B-Instruct`, a single agent step took about 36 minutes. The run was stopped before producing a map.

## Why it didn't finish
A 1.5B model is too weak for multi-step planning and reliable code generation. The original lesson uses a 32B model through a remote inference provider, which is why it works there.

## What I'd try next
- Run a single `CodeAgent` with the distance tool and search, using a model that fits the free tier.
- Return to multi-agent once I have access to a stronger model.
- Add the plot step separately so one failure doesn't block everything.

## Lessons learned
- Check the error line first, then the authorized imports list.
- Model size affects both quality and speed. Try the smallest model that can do the job.
- Restart the runtime after install errors, or the old import error sticks around.
