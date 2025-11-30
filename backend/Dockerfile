FROM python:3.12-slim

# Install uv.
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Copy the application into the container.
COPY . /app

# Install the application dependencies.
WORKDIR /app
RUN uv sync --frozen --no-cache

# Do not run as root user
RUN useradd app
USER app

# Run the application.
CMD ["/app/.venv/bin/uvicorn", "app.main:app", "--port", "8000", "--host", "0.0.0.0"]
