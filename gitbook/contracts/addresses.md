# Deployed Addresses

## Mantle Sepolia Testnet

**Chain ID:** 5003  
**Explorer:** https://sepolia.mantlescan.xyz

---

## Contract Addresses

| Contract      | Address                                                                                                                           |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| GoldToken     | [`0x787c8616d9b8Ccdca3B2b930183813828291dA9c`](https://sepolia.mantlescan.xyz/address/0x787c8616d9b8Ccdca3B2b930183813828291dA9c) |
| GoldFaucet    | [`0x5644F393a2480BE5E63731C30fCa81F9e80277a7`](https://sepolia.mantlescan.xyz/address/0x5644F393a2480BE5E63731C30fCa81F9e80277a7) |
| OwnaFarmNFT   | [`0xC51601dde25775bA2740EE14D633FA54e12Ef6C7`](https://sepolia.mantlescan.xyz/address/0xC51601dde25775bA2740EE14D633FA54e12Ef6C7) |
| OwnaFarmVault | [`0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa`](https://sepolia.mantlescan.xyz/address/0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa) |

---

## Integration Constants

### JavaScript/TypeScript

```javascript
const CONTRACTS = {
  GOLD_TOKEN: "0x787c8616d9b8Ccdca3B2b930183813828291dA9c",
  GOLD_FAUCET: "0x5644F393a2480BE5E63731C30fCa81F9e80277a7",
  OWNAFARM_NFT: "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7",
  OWNAFARM_VAULT: "0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa",
};
```

### Go

```go
const (
    GoldTokenAddress     = "0x787c8616d9b8Ccdca3B2b930183813828291dA9c"
    GoldFaucetAddress    = "0x5644F393a2480BE5E63731C30fCa81F9e80277a7"
    OwnaFarmNFTAddress   = "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7"
    OwnaFarmVaultAddress = "0x3b561Df673F08A566A09fEd718f5bdB8018C2CDa"
)
```

---

## Network Configuration

### RPC Endpoint

```
https://rpc.sepolia.mantle.xyz
```

### MetaMask Configuration

| Setting      | Value                          |
| ------------ | ------------------------------ |
| Network Name | Mantle Sepolia Testnet         |
| RPC URL      | https://rpc.sepolia.mantle.xyz |
| Chain ID     | 5003                           |
| Symbol       | MNT                            |
| Explorer     | https://sepolia.mantlescan.xyz |

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

| Human       | Wei                     |
| ----------- | ----------------------- |
| 1 GOLD      | 1000000000000000000     |
| 100 GOLD    | 100000000000000000000   |
| 10,000 GOLD | 10000000000000000000000 |

---

## Verification Status

All contracts verified on Mantle Sepolia Explorer with published source code.

| Contract      | Verified |
| ------------- | -------- |
| GoldToken     | Yes      |
| GoldFaucet    | Yes      |
| OwnaFarmNFT   | Yes      |
| OwnaFarmVault | Yes      |

---

## Mainnet Deployment

Mainnet deployment pending after security audit and beta testing.

---

[Next: Function Reference](functions.md)
