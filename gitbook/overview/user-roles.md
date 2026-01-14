# User Roles

## Platform Participants

OwnaFarm supports four distinct user roles, each with specific capabilities and interfaces.

---

## 👨‍🌾 Farmer

The capital seeker who tokenizes their invoices.

### Responsibilities

- Register and complete KYC verification
- Submit valid invoices from approved offtakers
- Receive and utilize funding for operations
- Fulfill contract obligations

### Access

- **Portal**: Farmer Frontend
- **Wallet**: Required for receiving funds

### Journey

```
Register → Submit Invoice → Await Approval → Receive Funding → Execute Contract
```

### Data Provided

| Category      | Information                                       |
| ------------- | ------------------------------------------------- |
| **Personal**  | Full name, ID, date of birth, address             |
| **Business**  | Business name, type, NPWP, bank details           |
| **Documents** | KTP, NPWP photo, bank statement, land certificate |
| **Invoice**   | Offtaker, amount, yield, duration                 |

---

## 💰 Investor

The capital provider who funds invoices through gamified investing.

### Responsibilities

- Connect wallet and acquire GOLD tokens
- Browse and evaluate available investments
- Fund invoices by purchasing "Seeds"
- Engage with game mechanics (watering, leveling)
- Harvest returns upon maturity

### Access

- **Portal**: Investor Frontend (Game App)
- **Wallet**: Required for all transactions

### Journey

```
Connect Wallet → Get GOLD → Buy Seeds → Nurture → Harvest Profits
```

### Profile Stats

| Stat             | Purpose                        |
| ---------------- | ------------------------------ |
| **Level**        | Unlock higher-tier investments |
| **XP**           | Progress toward next level     |
| **Water Points** | Resource for daily engagement  |
| **GOLD Balance** | Available investment capital   |

---

## 👨‍💼 Admin

Platform operator managing invoice approvals and system health.

### Responsibilities

- Review pending farmer registrations
- Approve or reject invoice submissions
- Monitor platform metrics
- Manage offtaker relationships
- Ensure vault liquidity

### Access

- **Portal**: Admin Dashboard (Internal)
- **Wallet**: Multi-sig for contract admin functions

### Capabilities

| Action             | Description                           |
| ------------------ | ------------------------------------- |
| `approveInvoice()` | Move invoice from Pending to Approved |
| `rejectInvoice()`  | Permanently reject an invoice         |
| `setFarmNFT()`     | Configure vault integration           |
| `depositYield()`   | Add yield reserves to vault           |

---

## 🏭 Offtaker

The end buyer whose contracts back the invoices (indirect participant).

### Role

- Issues purchase contracts to farmers
- Provides invoice legitimacy
- Fulfills payment upon delivery

### Examples

- Food manufacturers (Indofood, Nestlé)
- Agricultural cooperatives
- Export companies
- Retail chains

### Verification

Offtakers are pre-approved by platform administrators:

| Criteria               | Requirement                   |
| ---------------------- | ----------------------------- |
| **Creditworthiness**   | Financial stability verified  |
| **Track Record**       | History of honoring contracts |
| **Legal Status**       | Registered business entity    |
| **Contract Standards** | Compatible invoice format     |

---

## Role Interaction Matrix

```
             Farmer    Investor    Admin    Offtaker
Farmer         -       Funded by   Approved   Contract
Investor    Funds         -           -          -
Admin      Reviews    Monitors       -       Onboards
Offtaker   Contracts     -        Verified       -
```

---

## Permission Summary

| Role     | Submit Invoice | Invest | Approve | Harvest | Admin Functions |
| -------- | -------------- | ------ | ------- | ------- | --------------- |
| Farmer   | ✅             | ❌     | ❌      | ❌      | ❌              |
| Investor | ❌             | ✅     | ❌      | ✅      | ❌              |
| Admin    | ❌             | ❌     | ✅      | ❌      | ✅              |

---

## Next: [Invoice Tokenization →](../features/tokenization.md)
