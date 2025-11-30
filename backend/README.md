# FastAPI Backend 

## Running the backend

Build the container image with podman (or docker):

```bash
podman build -t gym-tracker-backend -f ./backend/Dockerfile
podman run -p 8000:8000 gym-tracker-backend
```

Then you can run it again with podman/docker:

```bash
podman run -p 8000:8000 gym-tracker-backend
INFO:     Started server process [1]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
INFO:     10.0.2.100:35074 - "GET / HTTP/1.1" 200 OK
INFO:     10.0.2.100:35078 - "GET /favicon.ico HTTP/1.1" 404 Not Found
```

## Structure (draft)

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
