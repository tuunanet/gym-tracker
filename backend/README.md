# FastAPI Backend 

## Structure planning

- Keep AI logic separate from your HTTP layer
- FastAPI routes should stay thin — they just call the agent. Agents and prompts live elsewhere.
- Mirrors how the pydantic-ai examples are structured
- The official examples separate agent logic from request-handling.
- Avoids circular imports
- If agents import schemas, and routers import agents, placing everything under one folder may create loops. Splitting avoids this.

```
backend/
    app/
        main.py
        routers/
            users.py
            ai.py        ← FastAPI routes that *call* your AI agents
        ai/              ← pydantic-ai lives here
            __init__.py
            agents.py    ← define Agent(...) or model-based agents
            prompts/
                summarize.md
                classify.md
            models/      ← Pydantic schemas for inputs/outputs
        core/
        schemas/
```
