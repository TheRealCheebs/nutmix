# Project Structure

- `cmd/` — Main applications for this project
- `internal/` — Private application and library code (includes generated files like `.pb.go`, `_templ.go`)
- `pkg/` — Public libraries intended for use by other projects
- `api/` — API-related code
- `test/` — Test utilities and setups
- `Dockerfile`, `docker-compose.yml`, `docker-compose-dev.yml` — Containerization files
- `justfile` — Project automation and build recipes
- `.env`, `env.example` — Environment configuration
- `.gitignore` — Ignore rules for secrets, generated files, and build artifacts
- `.github/workflows/` — CI/CD workflows
- `docs/` — Project documentation
