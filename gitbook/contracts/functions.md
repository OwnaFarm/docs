# Contract Functions

## Complete Function Reference

This page documents all callable functions across OwnaFarm smart contracts.

---

## GoldToken

Standard ERC-20 token with minting capability.

### Read Functions

| Function                    | Returns | Description               |
| --------------------------- | ------- | ------------------------- |
| `balanceOf(address)`        | uint256 | GOLD balance of address   |
| `allowance(owner, spender)` | uint256 | Approved amount           |
| `totalSupply()`             | uint256 | Total GOLD in circulation |
| `name()`                    | string  | "OwnaFarm Gold"           |
| `symbol()`                  | string  | "GOLD"                    |
| `decimals()`                | uint8   | 18                        |

### Write Functions

| Function                         | Access | Description        |
| -------------------------------- | ------ | ------------------ |
| `transfer(to, amount)`           | Public | Transfer GOLD      |
| `approve(spender, amount)`       | Public | Approve spender    |
| `transferFrom(from, to, amount)` | Public | Transfer on behalf |
| `mint(to, amount)`               | Owner  | Mint new GOLD      |

---

## GoldFaucet

Token distribution for testnet users.

### Read Functions

| Function                      | Returns | Description              |
| ----------------------------- | ------- | ------------------------ |
| `canClaim(address)`           | bool    | True if user can claim   |
| `timeUntilNextClaim(address)` | uint256 | Seconds until next claim |
| `claimAmount()`               | uint256 | GOLD per claim           |
| `cooldownTime()`              | uint256 | Seconds between claims   |

### Write Functions

| Function                   | Access | Description         |
| -------------------------- | ------ | ------------------- |
| `claim()`                  | Public | Claim free GOLD     |
| `deposit(amount)`          | Public | Add GOLD to faucet  |
| `setClaimAmount(amount)`   | Admin  | Change claim amount |
| `setCooldownTime(seconds)` | Admin  | Change cooldown     |
| `withdraw(amount)`         | Admin  | Withdraw GOLD       |

---

## OwnaFarmNFT

Core contract for invoices and investments.

### Invoice Functions

#### Submit Invoice

```solidity
function submitInvoice(
    bytes32 offtakerId,   // Buyer identifier
    uint128 targetFund,   // Amount to raise (18 decimals)
    uint16 yieldBps,      // Yield in basis points
    uint32 duration       // Lock period in seconds
) external returns (uint256 tokenId)
```

| Parameter  | Example                   | Description              |
| ---------- | ------------------------- | ------------------------ |
| offtakerId | `0x4f46465441...`         | bytes32 hash of buyer ID |
| targetFund | `10000000000000000000000` | 10,000 GOLD              |
| yieldBps   | `1500`                    | 15% yield                |
| duration   | `2592000`                 | 30 days in seconds       |

#### Admin Functions

| Function                  | Access | Description            |
| ------------------------- | ------ | ---------------------- |
| `approveInvoice(tokenId)` | Admin  | Approve for investment |
| `rejectInvoice(tokenId)`  | Admin  | Reject invoice         |

### Investment Functions

#### Invest in Invoice

```solidity
function invest(
    uint256 tokenId,  // Invoice ID
    uint128 amount    // GOLD amount (18 decimals)
) external
```

**Prerequisites**:

1. Invoice status must be `Approved`
2. Investor must have approved GOLD spending
3. Amount must not exceed remaining target

#### Harvest Returns

```solidity
function harvest(
    uint256 investmentId  // Index of investment
) external
```

**Prerequisites**:

1. Investment must exist
2. Not already claimed
3. Duration period must have passed

### View Functions

| Function                              | Parameters       | Returns             |
| ------------------------------------- | ---------------- | ------------------- |
| `invoices(tokenId)`                   | uint256          | Invoice struct      |
| `getInvestment(investor, id)`         | address, uint256 | Investment struct   |
| `investmentCount(investor)`           | address          | uint256             |
| `getPendingInvoices(offset, limit)`   | uint256, uint256 | Invoice[]           |
| `getPendingCount()`                   | -                | uint256             |
| `getAvailableInvoices(offset, limit)` | uint256, uint256 | Invoice[]           |
| `getAvailableCount()`                 | -                | uint256             |
| `balanceOf(account, id)`              | address, uint256 | uint256 (NFT count) |

### Data Structures

**Invoice Struct**:

```solidity
struct Invoice {
    address farmer;
    uint128 targetFund;
    uint128 fundedAmount;
    uint16 yieldBps;
    uint32 duration;
    uint32 createdAt;
    uint8 status;
    bytes32 offtakerId;
}
```

**Investment Struct**:

```solidity
struct Investment {
    uint128 amount;
    uint32 tokenId;
    uint32 investedAt;
    bool claimed;
}
```

---

## OwnaFarmVault

Yield reserve management.

### Write Functions

| Function                           | Access     | Description            |
| ---------------------------------- | ---------- | ---------------------- |
| `setFarmNFT(address)`              | Admin      | Set OwnaFarmNFT (once) |
| `depositYield(amount)`             | Admin      | Add yield reserve      |
| `withdrawYield(to, amount)`        | FarmNFT    | Pay investor yield     |
| `emergencyWithdraw(token, amount)` | SuperAdmin | Emergency recovery     |

---

## Common Patterns

### Approve Before Invest

```javascript
// Step 1: Approve GOLD spending
await goldToken.approve(ownaFarmNFT.address, amount);

// Step 2: Invest
await ownaFarmNFT.invest(tokenId, amount);
```

### Check If Can Harvest

```javascript
const investment = await ownaFarmNFT.getInvestment(investor, investmentId);
const invoice = await ownaFarmNFT.invoices(investment.tokenId);

const maturityTime = investment.investedAt + invoice.duration;
const canHarvest = Date.now() / 1000 >= maturityTime && !investment.claimed;
```

### Calculate Yield

```javascript
const yieldAmount = (principal * yieldBps) / 10000n;
const totalReturn = principal + yieldAmount;
```

---

## Error Codes

| Error                   | Cause                        |
| ----------------------- | ---------------------------- |
| `InsufficientBalance`   | Not enough GOLD              |
| `InsufficientAllowance` | Need to approve first        |
| `InvalidStatus`         | Invoice not in correct state |
| `AlreadyClaimed`        | Investment already harvested |
| `NotMature`             | Duration not passed          |
| `AmountExceedsTarget`   | Investment too large         |

---

## Next: [Tech Stack →](../technical/tech-stack.md)
