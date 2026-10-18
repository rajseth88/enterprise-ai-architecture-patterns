FROM mcr.microsoft.com/devcontainers/python:1-3.11-bullseye

# Install PostgreSQL client tools for CLI testing (pg_isready, psql)
RUN apt-get update && apt-get install -y --no-install-recommends \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*
