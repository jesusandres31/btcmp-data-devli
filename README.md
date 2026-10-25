# Devlights Bootcamp 5.0 | Data & Cloud

## Starting the containers

Requirement: [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running.

From the repo root:

```bash
docker compose up 

or 

docker compose up -d
```

This starts two services:

| Service    | Container              | URL / Port              | Credentials                            |
|------------|------------------------|-------------------------|----------------------------------------|
| PostgreSQL | `my_postgres_bootcamp` | `localhost:5433`        | `myuser` / `mypassword`, DB `postgres` |
| pgAdmin    | `my_pgadmin_bootcamp`  | http://localhost:8080   | `admin@example.com` / `adminpassword`  |

Check that they are running:

```bash
docker compose ps
```

## Connecting to the database

**From the terminal (psql):**

```bash
docker exec -it my_postgres_bootcamp psql -U myuser -d postgres
```

**From pgAdmin:** open http://localhost:8080 and register a new server with:

- Host: `postgres-db` (the service name on the Docker network, not `localhost`)
- Port: `5432`
- Username: `myuser`
- Password: `mypassword`

**From an external client (DBeaver, VS Code, etc.):** host `localhost`, port `5433`.

## Useful commands

```bash
docker compose logs -f postgres-db   # follow the logs
docker compose stop                  # stop without removing anything
docker compose down                  # stop and remove the containers
```

Postgres data is stored in the `./pgdata` folder, so it survives a `docker compose down`. To start from scratch, delete that folder.
