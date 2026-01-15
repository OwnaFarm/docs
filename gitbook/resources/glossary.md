# Glossary

## Terms and Definitions

---

## Platform Terms

| Term             | Definition                                                                    |
| ---------------- | ----------------------------------------------------------------------------- |
| **OwnaFarm**     | Platform connecting farmers with investors through gamified invoice financing |
| **Seed**         | Tokenized invoice represented as a virtual plant                              |
| **Garden**       | Investor portfolio showing active investments as crops                        |
| **Harvest**      | Action of claiming principal plus yield at maturity                           |
| **GOLD**         | Platform ERC-20 token for investments and rewards                             |
| **Water Points** | In-game resource for daily plant interactions                                 |
| **XP**           | Experience points from platform engagement                                    |
| **Level**        | Investor tier based on accumulated XP                                         |

---

## User Roles

| Term         | Definition                                  |
| ------------ | ------------------------------------------- |
| **Farmer**   | User who submits invoices for funding       |
| **Investor** | User who funds invoices by purchasing seeds |
| **Offtaker** | Buyer/company that issued the invoice       |
| **Admin**    | Platform operator managing approvals        |

---

## Financial Terms

| Term                   | Definition                                             |
| ---------------------- | ------------------------------------------------------ |
| **Invoice**            | Document representing money owed by offtaker to farmer |
| **Tokenization**       | Converting real-world asset to blockchain asset        |
| **Principal**          | Original investment amount                             |
| **Yield**              | Return/profit on investment (percentage)               |
| **Basis Points (bps)** | Unit for yield: 100 bps = 1%                           |
| **Maturity**           | Date when invoice becomes payable                      |
| **RWA**                | Real World Assets - tokenized physical assets          |

---

## Blockchain Terms

| Term               | Definition                                 |
| ------------------ | ------------------------------------------ |
| **Smart Contract** | Self-executing code on blockchain          |
| **ERC-20**         | Fungible token standard (GOLD)             |
| **ERC-1155**       | Multi-token standard (invoice NFTs)        |
| **NFT**            | Non-Fungible Token for unique ownership    |
| **Gas**            | Transaction fee for blockchain operations  |
| **Wallet**         | Software for managing blockchain addresses |
| **Mantle Network** | Layer 2 blockchain used by OwnaFarm        |
| **L2**             | Layer 2 scaling solution on Ethereum       |

---

## Technical Terms

| Term      | Definition                                         |
| --------- | -------------------------------------------------- |
| **Wei**   | Smallest token unit (1 GOLD = 10^18 wei)           |
| **ABI**   | Application Binary Interface for contracts         |
| **RPC**   | Remote Procedure Call for blockchain communication |
| **WAGMI** | React hooks library for Ethereum                   |
| **Viem**  | TypeScript Ethereum library                        |

---

## Invoice Statuses

| Status    | Code | Meaning               |
| --------- | ---- | --------------------- |
| Pending   | 0    | Awaiting admin review |
| Approved  | 1    | Open for investment   |
| Rejected  | 2    | Did not pass review   |
| Funded    | 3    | Fully invested        |
| Completed | 4    | All claims processed  |

---

## Formulas

### Yield Calculation

```
Yield Amount = Principal x (yieldBps / 10000)
Total Return = Principal + Yield Amount
```

### Duration Conversion

```
Seconds = Days x 86400
```

### Token Conversion

```
Wei = Human Amount x 10^18
```

---

## Abbreviations

| Abbr | Full Form                         |
| ---- | --------------------------------- |
| API  | Application Programming Interface |
| BE   | Backend                           |
| FE   | Frontend                          |
| DB   | Database                          |
| SC   | Smart Contract                    |
| TX   | Transaction                       |
| KYC  | Know Your Customer                |
| PWA  | Progressive Web App               |

---

## Common Values

### Time Durations

| Duration | Seconds   |
| -------- | --------- |
| 1 day    | 86,400    |
| 7 days   | 604,800   |
| 30 days  | 2,592,000 |
| 90 days  | 7,776,000 |

### Yield Rates

| Percentage | Basis Points |
| ---------- | ------------ |
| 1%         | 100          |
| 5%         | 500          |
| 10%        | 1,000        |
| 15%        | 1,500        |
| 20%        | 2,000        |
