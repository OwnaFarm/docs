# Glossary

## Key Terms and Definitions

Quick reference for terminology used throughout OwnaFarm documentation.

---

## Platform Terms

| Term             | Definition                                                                        |
| ---------------- | --------------------------------------------------------------------------------- |
| **OwnaFarm**     | The platform connecting farmers with investors through gamified invoice financing |
| **Seed**         | A tokenized invoice represented as a virtual plant that investors can purchase    |
| **Garden**       | The investor's portfolio view showing all active investments as growing crops     |
| **Harvest**      | The action of claiming principal plus yield when an invoice matures               |
| **GOLD**         | The platform's ERC-20 token used for all investments and rewards                  |
| **Water Points** | In-game resource used for daily plant interactions                                |
| **XP**           | Experience points earned through platform engagement                              |
| **Level**        | Investor tier based on accumulated XP, unlocking higher-yield opportunities       |

---

## User Roles

| Term         | Definition                                              |
| ------------ | ------------------------------------------------------- |
| **Farmer**   | A user who submits invoices for funding                 |
| **Investor** | A user who funds invoices by purchasing seeds           |
| **Offtaker** | The buyer/company that issued the invoice to the farmer |
| **Admin**    | Platform operator managing approvals and system health  |

---

## Financial Terms

| Term                     | Definition                                                    |
| ------------------------ | ------------------------------------------------------------- |
| **Invoice**              | A document representing money owed by an offtaker to a farmer |
| **Invoice Tokenization** | Converting a real-world invoice into a blockchain asset       |
| **Principal**            | The original investment amount                                |
| **Yield**                | The return/profit on an investment (expressed as %)           |
| **Basis Points (bps)**   | Unit for yield: 100 bps = 1%                                  |
| **Maturity**             | The date when an invoice becomes payable                      |
| **RWA**                  | Real World Assets - physical assets tokenized on blockchain   |

---

## Blockchain Terms

| Term               | Definition                                                          |
| ------------------ | ------------------------------------------------------------------- |
| **Smart Contract** | Self-executing code on the blockchain                               |
| **ERC-20**         | Token standard for fungible tokens (GOLD)                           |
| **ERC-1155**       | Multi-token standard for NFTs (invoice tokens)                      |
| **NFT**            | Non-Fungible Token representing unique ownership                    |
| **Gas**            | Transaction fee paid to the blockchain network                      |
| **Wallet**         | Software for managing blockchain addresses and signing transactions |
| **Mantle Network** | Layer 2 blockchain used by OwnaFarm                                 |
| **L2 / Layer 2**   | Scaling solution built on top of Ethereum                           |

---

## Technical Terms

| Term      | Definition                                                  |
| --------- | ----------------------------------------------------------- |
| **Wei**   | Smallest unit of tokens (1 GOLD = 10^18 wei)                |
| **ABI**   | Application Binary Interface for smart contract interaction |
| **RPC**   | Remote Procedure Call for blockchain communication          |
| **WAGMI** | React hooks library for Ethereum                            |
| **Viem**  | TypeScript library for Ethereum                             |
| **Privy** | Authentication service for Web3                             |

---

## Invoice Statuses

| Status        | Code | Meaning               |
| ------------- | ---- | --------------------- |
| **Pending**   | 0    | Awaiting admin review |
| **Approved**  | 1    | Open for investment   |
| **Rejected**  | 2    | Did not pass review   |
| **Funded**    | 3    | Fully invested        |
| **Completed** | 4    | All claims processed  |

---

## Calculation Formulas

### Yield Calculation

```
Yield Amount = Principal × (yieldBps / 10,000)
Total Return = Principal + Yield Amount
```

### Duration Conversion

```
duration (seconds) = days × 24 × 60 × 60
duration (seconds) = days × 86,400
```

### Token Conversion

```
raw amount (wei) = human amount × 10^18
human amount = raw amount / 10^18
```

---

## Abbreviations

| Abbreviation | Full Form                         |
| ------------ | --------------------------------- |
| **API**      | Application Programming Interface |
| **BE**       | Backend                           |
| **FE**       | Frontend                          |
| **DB**       | Database                          |
| **SC**       | Smart Contract                    |
| **TX**       | Transaction                       |
| **KYC**      | Know Your Customer                |
| **PWA**      | Progressive Web App               |
| **ORM**      | Object-Relational Mapping         |
| **JWT**      | JSON Web Token                    |

---

## Common Values

### Time Durations

| Duration | Seconds   |
| -------- | --------- |
| 1 hour   | 3,600     |
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

---

**Need help?** Join our community channels for support.
