# The builder image, used to build the virtual environment
FROM python:3.11-buster as builder

# Install poetry & zsh
RUN apt-get update && apt-get install -y zsh && rm -rf /var/lib/apt/lists/*
RUN pip install poetry==1.5.1

ENV POETRY_NO_INTERACTION=1 \
    POETRY_VIRTUALENVS_IN_PROJECT=1 \
    POETRY_VIRTUALENVS_CREATE=1 \
    POETRY_CACHE_DIR=/tmp/poetry_cache

WORKDIR /app

COPY pyproject.toml poetry.lock ./
RUN touch README.md

RUN --mount=type=cache,target=$POETRY_CACHE_DIR poetry install --without dev --no-root

FROM python:3.11-slim-buster as runtime

ENV VIRTUAL_ENV=/app/.venv \
    PATH="/app/.venv/bin:$PATH"

COPY --from=builder ${VIRTUAL_ENV} ${VIRTUAL_ENV}

COPY project ./project

## if building a completely standalone application, uncomment this to run the application as last step of docker-compose up
## CMD ["chainlit", "run", "app/main.py"] 