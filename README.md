# Verun Stellar MVP

The Trust Layer for Agentic Finance — now anchored on **Stellar Testnet**.

A 2-of-3 validator consensus protocol that scores AI agents and writes every verdict to Stellar as a Memo Transaction (sha256 of the verdict payload, anchored via a 1-stroop self-payment).

This repo is a Stellar port of [`verun-algorand-mvp`](https://github.com/rafaschul/verun-algorand-mvp). Same API surface, same validator logic, same UI — only the chain has changed.

## Quick start (local)

```bash
npm install
cp .env.example .env

# 1. Generate a fresh keypair and fund it via Friendbot
npm run genkey
# Copy the printed STELLAR_PUBLIC + STELLAR_SECRET into your .env

# 2. Sanity check
npm run check    # prints address + XLM balance
npm run selftx   # submits a real testnet TX, prints explorer URL

# 3. Run the API
npm run api      # http://localhost:3010
```

Smoke test the live endpoints:

```bash
chmod +x scripts/smoke-live.sh
./scripts/smoke-live.sh http://localhost:3010
# All five checks should print green-tickable values.
```

## API endpoints

| Method | Path | Purpose |
|---|---|---|
| GET  | `/api/health`          | Service heartbeat |
| GET  | `/api/validators`      | List validator set |
| GET  | `/api/config-check`    | Validate STELLAR_SECRET, Horizon reachability |
| GET  | `/api/funding-status`  | Account balance + auto-funds via Friendbot if missing |
| POST | `/api/score`           | Run validators only (no anchor) |
| POST | `/api/evaluate`        | Run validators + anchor verdict on Stellar testnet |

## Environment variables

See `.env.example`. Required: `STELLAR_SECRET`. Optional: `STELLAR_PUBLIC`, `HORIZON_URL`, `NETWORK_PASSPHRASE`, `FRIENDBOT_URL`.

## Deploy

See `DEPLOY.md` for the GitHub + Vercel walkthrough.

## License

MIT — © 2026 BCP Partners GmbH
