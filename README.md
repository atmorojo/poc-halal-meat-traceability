# Archived: Proof-of-Concept Halal Meat Traceability

> **This is a proof-of-concept, archived in favor of a Laravel rewrite. Code is preserved for reference only.**

## Overview

A proof-of-concept halal meat (beef/mutton) traceability application. Tracks livestock from farm → slaughterhouse → market, recording every step in a **faux-blockchain** (sqlitedict-backed, single-node, no PoW — a toy blockchain for demonstrating provenance).

Each stakeholder in the supply chain gets a role-based dashboard.

## Faux-Blockchain

The `Blockchain` class in `src/blockchain.py` uses sqlitedict as a simple key-value store with SHA-256 hashing to link blocks. No distributed consensus, no mining difficulty — just a hash chain to demonstrate provenance tracking.

## Stakeholder Roles

| Role | Description |
|------|-------------|
| `peternak` | Farmer — registers livestock |
| `rph` | Slaughterhouse — receives animals & manages cold chain deliveries |
| `juleha` | Halal slaughterer |
| `penyelia` | Supervisor — validates halal compliance |
| `lapak` | Stall owner — receives & sells meat at market |
| `pasar` | Market oversight |
| `admin` | System administration |

## Features

- Livestock registration & lifecycle tracking
- Dual halal validation (penyelia + juleha)
- Faux-blockchain record per transaction
- QR codes for consumer-facing verification
- IoT sensor monitoring (temperature/humidity) during cold chain delivery
- JWT authentication
- Role-based dashboards (htpy templates)

## Scope & Status

This was a time-boxed proof-of-concept focused on demonstrating the core supply
chain flow and blockchain provenance concept. Not every feature was built out.

### Implemented

- Livestock registration through the supply chain lifecycle
- Dual halal validation workflow (penyelia + juleha approval)
- Faux-blockchain recording of transactions
- QR code generation for consumer-facing provenance lookup
- IoT sensor intake (temperature/humidity) during cold chain delivery
- Role-based dashboards with JWT authentication
- Transaction management (admin creates, lapak confirms receipt)

### Scoped Out

- **Reporting module** — started in this POC as `routes/report.py` but
  deprioritized to focus on core traceability. Fully implemented in the
  Laravel rewrite.
- Consumer questionnaire tied to QR codes — noted in the backlog but not
  built in this POC phase.
- Form validation — basic, not production-grade.
- Various supply chain edge cases — the POC follows the happy path.

## How to Run

```bash
pip install -r requirements.txt
uvicorn main:app --reload
```

Visit `http://127.0.0.1:8000`.

## Tech Stack

Python, FastAPI, SQLAlchemy, sqlitedict (faux-blockchain), htpy, Alembic, numpy, qrcode, PostgreSQL / SQLite.

## Acknowledgment

This project was originally based on [Erik Williams' FastAPI-Blockchain](https://github.com/EPW80/FastAPI-Blockchain). As the client's requirements evolved, it grew beyond the original scope — adding role-based supply chain workflows, IoT integration, and a more domain-specific data model — but the initial blockchain concept came from Erik's work.
