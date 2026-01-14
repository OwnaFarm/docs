# Tech Stack

## Complete Technology Overview

OwnaFarm is built with modern, production-ready technologies across all layers.

---

## Architecture Summary

```
┌─────────────────────────────────────────────────────────────────┐
│                        FRONTEND LAYER                           │
├────────────────────────────┬────────────────────────────────────┤
│      Farmer Portal         │          Investor App             │
│      (Next.js 16)          │          (Next.js 16)             │
│      Tailwind CSS          │          Tailwind CSS             │
│      WAGMI + Privy         │          WAGMI                    │
│      Zustand               │          Framer Motion            │
└────────────────────────────┴────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                        BACKEND LAYER                            │
├─────────────────────────────────────────────────────────────────┤
│                       Go + Gin Framework                        │
│                       GORM (PostgreSQL)                         │
│                       Valkey (Redis-compatible)                 │
│                       go-ethereum                               │
│                       Cloudflare R2                             │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                      BLOCKCHAIN LAYER                           │
├─────────────────────────────────────────────────────────────────┤
│                    Foundry + Solidity                           │
│                    Mantle Sepolia (L2)                          │
│                    ERC-20 + ERC-1155                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Frontend Technologies

### Core Framework

| Technology     | Version | Purpose                         |
| -------------- | ------- | ------------------------------- |
| **Next.js**    | 16.x    | React framework with App Router |
| **React**      | 19.x    | UI component library            |
| **TypeScript** | 5.x     | Type-safe JavaScript            |

### Styling

| Technology        | Purpose                         |
| ----------------- | ------------------------------- |
| **Tailwind CSS**  | Utility-first CSS framework     |
| **Radix UI**      | Accessible component primitives |
| **Framer Motion** | Animations and transitions      |
| **Lucide React**  | Icon library                    |

### Web3 Integration

| Technology         | Purpose                          |
| ------------------ | -------------------------------- |
| **WAGMI**          | React hooks for Ethereum         |
| **Viem**           | TypeScript Ethereum client       |
| **Privy**          | Social login + wallet connection |
| **TanStack Query** | Data fetching and caching        |

### State Management

| Technology          | Purpose                      |
| ------------------- | ---------------------------- |
| **Zustand**         | Lightweight state management |
| **React Hook Form** | Form handling                |
| **Zod**             | Schema validation            |

---

## Backend Technologies

### Core Stack

| Technology | Version | Purpose            |
| ---------- | ------- | ------------------ |
| **Go**     | 1.22+   | Backend language   |
| **Gin**    | 1.x     | HTTP web framework |
| **GORM**   | 2.x     | ORM for database   |

### Databases & Caching

| Technology     | Purpose                                      |
| -------------- | -------------------------------------------- |
| **PostgreSQL** | Primary relational database                  |
| **Valkey**     | Caching and session store (Redis-compatible) |

### Blockchain Integration

| Technology       | Purpose                 |
| ---------------- | ----------------------- |
| **go-ethereum**  | Ethereum client library |
| **ABI Bindings** | Contract interaction    |

### Storage & Services

| Technology        | Purpose                      |
| ----------------- | ---------------------------- |
| **Cloudflare R2** | Object storage for documents |
| **S3 SDK**        | R2 API compatibility         |

---

## Smart Contract Technologies

### Development

| Technology       | Purpose                     |
| ---------------- | --------------------------- |
| **Foundry**      | Development framework       |
| **Solidity**     | Contract language (^0.8.20) |
| **OpenZeppelin** | Audited contract libraries  |

### Standards

| Standard          | Implementation         |
| ----------------- | ---------------------- |
| **ERC-20**        | GoldToken              |
| **ERC-1155**      | OwnaFarmNFT            |
| **AccessControl** | Role-based permissions |

### Network

| Property         | Value                  |
| ---------------- | ---------------------- |
| **Network**      | Mantle Sepolia         |
| **Type**         | L2 (Optimistic Rollup) |
| **Chain ID**     | 5003                   |
| **Native Token** | MNT                    |

---

## Development Tools

### Frontend

```bash
# Package Manager
pnpm

# Build Tools
next build
turbopack (dev mode)

# Linting
eslint
```

### Backend

```bash
# Build
go build

# Testing
go test

# Hot Reload
air
```

### Smart Contracts

```bash
# Build
forge build

# Test
forge test

# Deploy
forge script

# Verify
forge verify-contract
```

---

## Infrastructure

### Deployment

| Layer    | Platform             |
| -------- | -------------------- |
| Frontend | Vercel               |
| Backend  | Docker / Cloud Run   |
| Database | Cloud SQL / Supabase |
| Storage  | Cloudflare R2        |

### Monitoring

| Tool             | Purpose             |
| ---------------- | ------------------- |
| Vercel Analytics | Frontend metrics    |
| Prometheus       | Backend metrics     |
| Mantle Explorer  | On-chain monitoring |

---

## Security Considerations

| Layer               | Measures                          |
| ------------------- | --------------------------------- |
| **Frontend**        | CSP headers, input validation     |
| **Backend**         | JWT auth, rate limiting, CORS     |
| **Smart Contracts** | OpenZeppelin libs, access control |
| **Infrastructure**  | SSL/TLS, secrets management       |

---

## Next: [System Flow →](system-flow.md)
