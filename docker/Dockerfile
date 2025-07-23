FROM python:3.12-alpine

WORKDIR /app

# ENV UV_COMPILE_BYTECODE=1

ENV UV_NO_CACHE=1

RUN --mount=type=bind,source=./app/uv.lock,target=uv.lock \
    --mount=type=bind,source=./app/pyproject.toml,target=pyproject.toml \
    --mount=from=ghcr.io/astral-sh/uv,source=/uv,target=/bin/uv \
    uv sync --locked --no-install-project --no-dev

ADD ./app /app

RUN --mount=from=ghcr.io/astral-sh/uv,source=/uv,target=/bin/uv \
    uv sync --locked --no-dev

ENV PATH="/app/.venv/bin:$PATH"

EXPOSE 8000

CMD ["fastapi", "run"]

