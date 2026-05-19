# AI usage disclosure

## Tool used

**Cursor** (AI-assisted IDE / agent)

## How the tool was used

- Database schema design and SQL migrations from `implementation-details.md`
- Project scaffolding (layered architecture: handler, service, repository, domain)
- PostgreSQL repository SQL implementations
- Service-layer refactor (`CreateTransfer` helpers, idempotency, workflow)
- Unit tests with an in-memory store (per `ASSIGNMENT.md` testing requirements)
- Troubleshooting: Docker port conflicts (5432 vs 5433), `golang-migrate`, Go toolchain (`GOTOOLCHAIN=local`)
- Documentation: `README.md` guidance, end-to-end testing steps, `run.md`

Business logic and design decisions were reviewed and iterated through prompts; the candidate should be able to explain the PR and implementation in an interview.

---

## Prompts used (chronological)

1. **Postgres + migration**
   > add postgres database configution in this repo, and create a dababase migration from schema mentioned in @implementation-details.md

2. **README**
   > write me a Readme file for this project

3. **Project structure (no business logic)**
   > start implementing using @implementation-details.md and @ASSIGNMENT.md , only implement structure, keep business logic implementation for me, i would implement that, thanks

4. **Repository `Create` guidance**
   > how would you implement this?
   > (with `TransferRepository.Create` stub in `internal/repository/postgres/transfer.go`)

5. **Repository SQL**
   > write all required queries in repository/postgres

6. **Service helpers**
   > can add functions for inside working of createtransfer in @internal/service/transfer.go

7. **Unit tests**
   > can write unit tests coverage mentioned in @ASSIGNMENT.md file, thanks

8. **Go toolchain / `make test`**
   > `make test` → `go: download go1.24 ... toolchain not available` (and follow-ups for go1.22 / go1.23)

9. **End-to-end testing**
   > how can i test end to end?

10. **Docker verify query**
    > `docker compose exec postgres psql ...` → `no configuration file provided: not found`

11. **This file + run guide**
    > add all prompts given to you in @AI-usage.md and add run.md file for how to run the code locally for someone totally new to it

---

## Notes for reviewers

- Full agent session transcripts can be exported from Cursor if required by the assignment.
- Prompts above are the substantive user requests; brief system/task notifications are omitted.
