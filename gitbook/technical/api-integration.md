# API Integration

## Developer Integration Guide

---

## Smart Contract Integration

### WAGMI Setup

```typescript
import { createConfig, http } from "wagmi";
import { mantleSepoliaTestnet } from "wagmi/chains";

export const config = createConfig({
  chains: [mantleSepoliaTestnet],
  transports: {
    [mantleSepoliaTestnet.id]: http("https://rpc.sepolia.mantle.xyz"),
  },
});
```

### Contract Constants

```typescript
const CONTRACTS = {
  GOLD_TOKEN: "0x787c8616d9b8Ccdca3B2b930183813828291dA9c",
  OWNAFARM_NFT: "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7",
};
```

### Read Contract

```typescript
import { useReadContract } from "wagmi";

const { data: invoices } = useReadContract({
  address: CONTRACTS.OWNAFARM_NFT,
  abi: OwnaFarmNFTABI,
  functionName: "getAvailableInvoices",
  args: [0n, 10n],
});
```

### Write Contract

```typescript
import { useWriteContract } from "wagmi";
import { parseEther } from "viem";

const { writeContract } = useWriteContract();

// Approve + Invest
await writeContract({
  address: CONTRACTS.GOLD_TOKEN,
  abi: GoldTokenABI,
  functionName: "approve",
  args: [CONTRACTS.OWNAFARM_NFT, parseEther("1000")],
});

await writeContract({
  address: CONTRACTS.OWNAFARM_NFT,
  abi: OwnaFarmNFTABI,
  functionName: "invest",
  args: [tokenId, parseEther("1000")],
});
```

---

## Backend API

### Base Configuration

```typescript
const API_BASE = process.env.NEXT_PUBLIC_API_URL || "http://localhost:8080";

async function fetchAPI(endpoint: string, options?: RequestInit) {
  const response = await fetch(`${API_BASE}${endpoint}`, {
    ...options,
    headers: {
      "Content-Type": "application/json",
      ...options?.headers,
    },
  });
  if (!response.ok) throw new Error("API error");
  return response.json();
}
```

### Endpoints

#### Authentication

| Endpoint      | Method | Description          |
| ------------- | ------ | -------------------- |
| `/auth/nonce` | GET    | Get nonce for wallet |
| `/auth/login` | POST   | Login with signature |

#### Farmers

| Endpoint                     | Method | Description     |
| ---------------------------- | ------ | --------------- |
| `/farmers/register`          | POST   | Register farmer |
| `/farmers/documents/presign` | POST   | Get upload URLs |

#### Crops (Investor)

| Endpoint           | Method | Description          |
| ------------------ | ------ | -------------------- |
| `/crops`           | GET    | List user crops      |
| `/crops/:id`       | GET    | Get crop details     |
| `/crops/sync`      | POST   | Sync from blockchain |
| `/crops/:id/water` | POST   | Water plant          |

#### Game

| Endpoint                | Method | Description        |
| ----------------------- | ------ | ------------------ |
| `/user/profile`         | GET    | Get profile        |
| `/leaderboard`          | GET    | Get rankings       |
| `/marketplace/invoices` | GET    | Available invoices |

---

## Go Backend Integration

### Ethereum Client

```go
import (
    "github.com/ethereum/go-ethereum/ethclient"
    "github.com/ethereum/go-ethereum/common"
)

const RPC_URL = "https://rpc.sepolia.mantle.xyz"

func NewClient() (*ethclient.Client, error) {
    return ethclient.Dial(RPC_URL)
}
```

### Read Contract

```go
func GetInvoice(tokenId int64) (*Invoice, error) {
    client, _ := NewClient()
    nft, _ := NewOwnaFarmNFT(common.HexToAddress(NFT_ADDRESS), client)

    invoice, err := nft.Invoices(nil, big.NewInt(tokenId))
    if err != nil {
        return nil, err
    }

    return &Invoice{
        Farmer:     invoice.Farmer,
        TargetFund: invoice.TargetFund,
        Status:     invoice.Status,
    }, nil
}
```

### Event Listening

```go
func WatchInvestments(ctx context.Context) error {
    client, _ := NewClient()
    nft, _ := NewOwnaFarmNFT(common.HexToAddress(NFT_ADDRESS), client)

    sink := make(chan *OwnaFarmNFTInvested)
    sub, err := nft.WatchInvested(nil, sink, nil, nil)
    if err != nil {
        return err
    }
    defer sub.Unsubscribe()

    for {
        select {
        case event := <-sink:
            // Handle investment event
        case <-ctx.Done():
            return nil
        }
    }
}
```

---

## Error Handling

### Contract Errors

```typescript
import { ContractFunctionExecutionError } from "viem";

try {
  await invest(tokenId, amount);
} catch (error) {
  if (error instanceof ContractFunctionExecutionError) {
    if (error.message.includes("InsufficientBalance")) {
      // Handle insufficient funds
    }
  }
}
```

### API Errors

| Code | Description  |
| ---- | ------------ |
| 400  | Bad request  |
| 401  | Unauthorized |
| 404  | Not found    |
| 429  | Rate limited |
| 500  | Server error |

---

[Next: Glossary](../resources/glossary.md)
