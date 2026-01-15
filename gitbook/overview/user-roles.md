# User Roles

## Platform Participants

OwnaFarm supports four user roles with distinct capabilities.

---

## Farmer

The capital seeker who tokenizes invoices.

**Access:** Farmer Portal

**Capabilities:**

- Register and complete KYC
- Submit invoices from approved offtakers
- Receive and utilize funding
- Manage farms and track status

**Data Provided:**

| Category  | Information                       |
| --------- | --------------------------------- |
| Personal  | Name, ID, address, contact        |
| Business  | Business type, NPWP, bank details |
| Documents | KTP, NPWP photo, bank statement   |
| Invoice   | Offtaker, amount, yield, duration |

---

## Investor

The capital provider who funds invoices through gaming.

**Access:** Investor App (Game)

**Capabilities:**

- Connect wallet and acquire GOLD
- Browse and evaluate investments
- Fund invoices by purchasing seeds
- Engage with game mechanics
- Harvest returns at maturity

**Profile Stats:**

| Stat         | Purpose                        |
| ------------ | ------------------------------ |
| Level        | Unlock higher-tier investments |
| XP           | Progress toward next level     |
| Water Points | Resource for daily engagement  |
| GOLD Balance | Available capital              |

---

## Admin

Platform operator managing approvals.

**Access:** Admin Dashboard

**Capabilities:**

- Review farmer registrations
- Approve or reject invoices
- Monitor platform metrics
- Manage offtaker relationships
- Ensure vault liquidity

**Contract Functions:**

| Function           | Description             |
| ------------------ | ----------------------- |
| `approveInvoice()` | Move to Approved status |
| `rejectInvoice()`  | Reject submission       |
| `depositYield()`   | Add yield reserves      |

---

## Offtaker

The buyer whose contracts back invoices (indirect participant).

**Role:**

- Issues purchase contracts to farmers
- Provides invoice legitimacy
- Fulfills payment upon delivery

**Examples:** Food manufacturers, agricultural cooperatives, export companies

**Verification Criteria:**

| Criteria         | Requirement         |
| ---------------- | ------------------- |
| Creditworthiness | Financial stability |
| Track Record     | Payment history     |
| Legal Status     | Registered entity   |

---

## Permission Matrix

| Role     | Submit Invoice | Invest | Approve | Harvest | Admin |
| -------- | -------------- | ------ | ------- | ------- | ----- |
| Farmer   | Yes            | No     | No      | No      | No    |
| Investor | No             | Yes    | No      | Yes     | No    |
| Admin    | No             | No     | Yes     | No      | Yes   |

---

[Next: Invoice Tokenization](../features/tokenization.md)
