# Relay4U — Pentest Sandbox

A self-contained, local Docker stack of the Relay4U prospecting tool (PostgreSQL + backend + frontend), built specifically so security researchers and pentesters can run the whole application on their own machine and test it.

This is **not** the production or staging environment. It's a disposable sandbox: everything runs locally, no real data ever exists in it, and it sends no real emails.

## Quickstart

Requires [Docker](https://docs.docker.com/get-docker/) and Docker Compose.

```bash
git clone https://github.com/prospect-tool-relay4u-eu/prospect-tool-docker.git
cd prospect-tool-docker
docker compose up
```

Then open:
- **App**: http://localhost:4200
- **API**: http://localhost:8080/api
- **Swagger UI**: http://localhost:8080/swagger-ui.html

## How to sign in

There's no pre-seeded account — register your own through the app:

1. Go to http://localhost:4200/register and create an account with any email address.
2. The sandbox **never sends real emails**. Your 6-digit verification code is printed to the backend's logs instead:
   ```bash
   docker compose logs backend | grep "SANDBOX"
   ```
3. Enter the code at http://localhost:4200/verify-email, then log in.
4. Create a project, define fields, and start poking at it.

## What's in the box

| Service | Image | Port |
|---|---|---|
| `db` | `postgres:16-alpine` | (internal only) |
| `backend` | `ghcr.io/prospect-tool-relay4u-eu/relay4u-be` | `8080` |
| `frontend` | `ghcr.io/prospect-tool-relay4u-eu/relay4u-fe` | `4200` |

Source code for the two application images:
- [`prospect-tool-be`](https://github.com/prospect-tool-relay4u-eu/prospect-tool-be) — Spring Boot backend
- [`prospect-tool-fe`](https://github.com/prospect-tool-relay4u-eu/prospect-tool-fe) — Angular frontend

## Resetting data

Postgres data is kept in a named volume, so it survives normal restarts:

```bash
docker compose down    # stop containers, keep data
docker compose up      # data is still there
```

For a full clean slate:

```bash
docker compose down -v   # also deletes the database volume
```

## Reporting findings

Please open a [GitHub issue](https://github.com/prospect-tool-relay4u-eu/prospect-tool-docker/issues/new/choose) on this repo using the pentest finding template. See [SECURITY.md](SECURITY.md) for scope and reporting details.

## Known limitations

- The `backend`/`frontend` images are built and released independently from their own repos and both track `:latest`. They're normally released together, but versions could in principle drift out of sync (e.g. a newer backend API not yet matched by the published frontend). Not an issue for typical testing — just something to be aware of if things look inconsistent after a fresh `docker compose pull`.

## License

This project is licensed under the [MIT License](LICENSE).
