# Deployed Addresses

## Mantle Sepolia Testnet

> **Chain ID**: 5003  
> **Explorer**: https://sepolia.mantlescan.xyz

---

## Contract Addresses

| Contract          | Address                                      | Explorer                                                                                    |
| ----------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **GoldToken**     | `0x787c8616d9b8Ccdca3B2b930183813828291dA9c` | [View ↗](https://sepolia.mantlescan.xyz/address/0x787c8616d9b8Ccdca3B2b930183813828291dA9c) |
| **GoldFaucet**    | `0x5644F393a2480BE5E63731C30fCa81F9e80277a7` | [View ↗](https://sepolia.mantlescan.xyz/address/0x5644F393a2480BE5E63731C30fCa81F9e80277a7) |
| **OwnaFarmNFT**   | `0xC51601dde25775bA2740EE14D633FA54e12Ef6C7` | [View ↗](https://sepolia.mantlescan.xyz/address/0xC51601dde25775bA2740EE14D633FA54e12Ef6C7) |
| **OwnaFarmVault** | `0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa` | [View ↗](https://sepolia.mantlescan.xyz/address/0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa) |

---

## Quick Copy

### For Frontend Integration

```javascript
// Contract Addresses - Mantle Sepolia
const CONTRACTS = {
  GOLD_TOKEN: "0x787c8616d9b8Ccdca3B2b930183813828291dA9c",
  GOLD_FAUCET: "0x5644F393a2480BE5E63731C30fCa81F9e80277a7",
  OWNAFARM_NFT: "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7",
  OWNAFARM_VAULT: "0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa",
};
```

### For Backend Integration

```go
// Contract Addresses - Mantle Sepolia
const (
    GoldTokenAddress    = "0x787c8616d9b8Ccdca3B2b930183813828291dA9c"
    GoldFaucetAddress   = "0x5644F393a2480BE5E63731C30fCa81F9e80277a7"
    OwnaFarmNFTAddress  = "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7"
    OwnaFarmVaultAddress = "0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa"
)
```

---

## Network Configuration

### RPC Endpoints

| Network        | RPC URL                          |
| -------------- | -------------------------------- |
| Mantle Sepolia | `https://rpc.sepolia.mantle.xyz` |

### Add to MetaMask

| Setting         | Value                            |
| --------------- | -------------------------------- |
| Network Name    | Mantle Sepolia Testnet           |
| RPC URL         | `https://rpc.sepolia.mantle.xyz` |
| Chain ID        | `5003`                           |
| Currency Symbol | `MNT`                            |
| Block Explorer  | `https://sepolia.mantlescan.xyz` |

---

## Token Information

### GOLD Token

| Property | Value         |
| -------- | ------------- |
| Name     | OwnaFarm Gold |
| Symbol   | GOLD          |
| Decimals | 18            |
| Type     | ERC-20        |

### Decimal Conversion

| Human Readable | Wei (Raw Value)            |
| -------------- | -------------------------- |
| 1 GOLD         | `1000000000000000000`      |
| 100 GOLD       | `100000000000000000000`    |
| 1,000 GOLD     | `1000000000000000000000`   |
| 10,000 GOLD    | `10000000000000000000000`  |
| 100,000 GOLD   | `100000000000000000000000` |

---

## Verification Status

All contracts are verified on Mantle Sepolia Explorer:

| Contract      | Verified | Source Code |
| ------------- | -------- | ----------- |
| GoldToken     | ✅       | Published   |
| GoldFaucet    | ✅       | Published   |
| OwnaFarmNFT   | ✅       | Published   |
| OwnaFarmVault | ✅       | Published   |

---

## Mainnet Deployment

> 🚧 **Coming Soon**
>
> Mainnet deployment will be announced after:
>
> - Security audit completion
> - Beta testing conclusion
> - Community review period

---

## Next: [Contract Functions →](functions.md)
