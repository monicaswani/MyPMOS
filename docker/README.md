# docker/

Container definitions and orchestration for PMOS.

## Contents (planned)

- `Dockerfile` — application image.
- `docker-compose.yml` — local development stack (app, Postgres, Redis, vector DB).
- `docker-compose.prod.yml` — production overrides.

## Usage

```bash
docker compose -f docker/docker-compose.yml up --build
```

Environment is supplied via the root `.env` file (see `.env.example`).
