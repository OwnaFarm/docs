# Function Reference

## Complete Function Documentation

---

## GoldToken

Standard ERC-20 with minting capability.

### Read Functions

| Function                    | Returns | Description       |
| --------------------------- | ------- | ----------------- |
| `balanceOf(address)`        | uint256 | GOLD balance      |
| `allowance(owner, spender)` | uint256 | Approved amount   |
| `totalSupply()`             | uint256 | Total circulation |
| `name()`                    | string  | "OwnaFarm Gold"   |
| `symbol()`                  | string  | "GOLD"            |
| `decimals()`                | uint8   | 18                |

### Write Functions

| Function                         | Access | Description        |
| -------------------------------- | ------ | ------------------ |
| `transfer(to, amount)`           | Public | Transfer GOLD      |
| `approve(spender, amount)`       | Public | Approve spender    |
| `transferFrom(from, to, amount)` | Public | Delegated transfer |
| `mint(to, amount)`               | Owner  | Mint new GOLD      |

---

## GoldFaucet

Testnet token distribution.

### Read Functions

| Function                      | Returns | Description              |
| ----------------------------- | ------- | ------------------------ |
| `canClaim(address)`           | bool    | Claim eligibility        |
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

Core invoice and investment contract.

### Submit Invoice

```solidity
function submitInvoice(
    bytes32 offtakerId,
    uint128 targetFund,
    uint16 yieldBps,
    uint32 duration
) external returns (uint256 tokenId)
```

| Parameter  | Example   | Description           |
| ---------- | --------- | --------------------- |
| offtakerId | 0x4f46... | Buyer identifier hash |
| targetFund | 10000e18  | 10,000 GOLD           |
| yieldBps   | 1500      | 15% yield             |
| duration   | 2592000   | 30 days               |

### Invest

```solidity
function invest(uint256 tokenId, uint128 amount) external
```

**Requirements:**

- Invoice status is Approved
- GOLD spending approved
- Amount within target

### Harvest

```solidity
function harvest(uint256 investmentId) external
```

**Requirements:**

- Investment exists
- Not already claimed
- Duration passed

### Admin Functions

| Function                  | Access | Description            |
| ------------------------- | ------ | ---------------------- |
| `approveInvoice(tokenId)` | Admin  | Approve for investment |
| `rejectInvoice(tokenId)`  | Admin  | Reject submission      |

### View Functions

| Function                              | Description            |
| ------------------------------------- | ---------------------- |
| `invoices(tokenId)`                   | Get invoice details    |
| `getInvestment(investor, id)`         | Get investment details |
| `investmentCount(investor)`           | Count investments      |
| `getPendingInvoices(offset, limit)`   | List pending           |
| `getAvailableInvoices(offset, limit)` | List available         |

---

## OwnaFarmVault

Yield reserve management.

| Function                           | Access  | Description             |
| ---------------------------------- | ------- | ----------------------- |
| `setFarmNFT(address)`              | Admin   | Set NFT contract (once) |
| `depositYield(amount)`             | Admin   | Add yield reserve       |
| `withdrawYield(to, amount)`        | FarmNFT | Pay investor yield      |
| `emergencyWithdraw(token, amount)` | Owner   | Emergency recovery      |

---

## Data Structures

### Invoice

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

### Investment

```solidity
struct Investment {
    uint128 amount;
    uint32 tokenId;
    uint32 investedAt;
    bool claimed;
}
```

---

## Common Patterns

### Approve Before Invest

```javascript
await goldToken.approve(nftAddress, amount);
await ownaFarmNFT.invest(tokenId, amount);
```

### Check Harvest Eligibility

```javascript
const investment = await nft.getInvestment(investor, id);
const invoice = await nft.invoices(investment.tokenId);
const maturity = investment.investedAt + invoice.duration;
const canHarvest = Date.now() / 1000 >= maturity && !investment.claimed;
```

---

## Error Codes

| Error                 | Cause                 |
| --------------------- | --------------------- |
| InsufficientBalance   | Not enough GOLD       |
| InsufficientAllowance | Need to approve first |
| InvoiceNotApproved    | Wrong invoice status  |
| AlreadyClaimed        | Already harvested     |
| NotMature             | Duration not passed   |
| ExceedsTarget         | Investment too large  |

---

[Next: Tech Stack](../technical/tech-stack.md)
