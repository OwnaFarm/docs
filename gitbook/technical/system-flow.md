# System Flow

## Data Flow Architecture

---

## High-Level Flow

```mermaid
graph LR
    subgraph Users
        F[Farmer]
        I[Investor]
    end

    subgraph Frontend
        FP[Farmer Portal]
        IA[Investor App]
    end

    subgraph Backend
        API[Go API]
        DB[(Database)]
        S3[Storage]
    end

    subgraph Blockchain
        SC[Smart Contracts]
    end

    F --> FP --> API --> DB
    FP --> S3
    I --> IA --> API
    IA --> SC
    API --> SC
```

---

## Farmer Registration

```mermaid
sequenceDiagram
    participant F as Farmer
    participant FE as Portal
    participant BE as Backend
    participant R2 as Storage
    participant DB as Database

    F->>FE: Fill form
    FE->>BE: POST /farmers/register
    BE->>R2: Upload documents
    BE->>DB: Save profile
    BE-->>FE: {farmerId, status}
```

| Location | Data                            |
| -------- | ------------------------------- |
| Database | Personal info, business details |
| Storage  | KTP, NPWP, bank statement       |

---

## Invoice Submission

```mermaid
sequenceDiagram
    participant F as Farmer
    participant FE as Portal
    participant BE as Backend
    participant SC as Contract

    F->>FE: Submit invoice
    FE->>BE: POST /invoices
    BE->>SC: submitInvoice()
    SC-->>BE: tokenId
    BE-->>FE: {tokenId, status}
```

---

## Investment Flow

```mermaid
sequenceDiagram
    participant I as Investor
    participant FE as App
    participant SC as Contract
    participant BE as Backend

    I->>FE: Select seed
    FE->>SC: approve() + invest()
    SC-->>FE: Investment recorded
    FE->>BE: POST /crops/sync
    BE-->>FE: Game state updated
```

---

## Harvest Flow

```mermaid
sequenceDiagram
    participant I as Investor
    participant FE as App
    participant SC as Contract
    participant V as Vault

    I->>FE: Click Harvest
    FE->>SC: harvest()
    SC->>V: withdrawYield()
    V-->>SC: GOLD transferred
    SC-->>FE: Complete
```

---

## Game Engagement

```mermaid
sequenceDiagram
    participant I as Investor
    participant FE as App
    participant BE as Backend
    participant DB as Database

    I->>FE: Water plant
    FE->>BE: POST /game/water
    BE->>DB: Update XP, water
    BE-->>FE: {xpGained, waterRemaining}
```

| Data  | Storage  | Updates         |
| ----- | -------- | --------------- |
| XP    | Database | Per interaction |
| Level | Database | On threshold    |
| Water | Database | Daily regen     |

---

## Admin Approval

```mermaid
sequenceDiagram
    participant A as Admin
    participant AD as Dashboard
    participant SC as Contract

    A->>AD: View pending
    AD->>SC: getPendingInvoices()
    A->>AD: Approve
    AD->>SC: approveInvoice()
    SC-->>AD: Status: Approved
```

---

## Layer Responsibilities

| Layer      | Handles             | Does Not Handle        |
| ---------- | ------------------- | ---------------------- |
| Frontend   | UI, wallet, caching | Business logic         |
| Backend    | Auth, game, files   | Financial transactions |
| Blockchain | Financial state     | User metadata          |

---

[Next: API Integration](api-integration.md)
