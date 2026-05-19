# Application architecture

Layered layout for the wallet transfer service. Business logic is intentionally left as `TODO` for you to implement.

## Layers

```text
HTTP request
    → handler     (validation, JSON mapping)
    → service     (idempotency, transactions, workflow)
    → repository  (SQL, pessimistic locking)
    → PostgreSQL
```

## Packages

| Package | Responsibility |
|---------|----------------|
| `internal/domain` | `Transfer`, `Wallet`, `LedgerEntry`, states, domain errors |
| `internal/handler` | `POST /transfers`, `GET /health` |
| `internal/service` | `TransferService.CreateTransfer` orchestration |
| `internal/repository` | Interfaces + transaction context |
| `internal/repository/postgres` | PostgreSQL stubs with `TODO` SQL |
| `cmd/server` | Wiring and HTTP server |

## Implementation checklist

1. **`domain/transfer.go`** — `CanTransitionTo`, complete `ValidateTransferRequest`
2. **`service/transfer.go`** — full `CreateTransfer` workflow (see comment in file)
3. **`repository/postgres/*.go`** — SQL with `FOR UPDATE` on wallets inside `store.Tx().WithTransaction`
4. **Idempotency** — read/save `idempotency_records`; return stored response on replay

## Concurrency (from implementation-details.md)

Use pessimistic locking: call `WalletRepository.LockByID` inside a transaction so concurrent debits on the same wallet serialize.

## Run locally

```bash
make db-up
make db-migrate
make run
```
