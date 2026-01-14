# API Integration

## Integration Guide for Developers

This page provides guidance for integrating with OwnaFarm's various APIs and smart contracts.

---

## Frontend to Smart Contract

### Setup with WAGMI

```typescript
// config.ts
import { createConfig, http } from "wagmi";
import { mantleSepoliaTestnet } from "wagmi/chains";

export const config = createConfig({
  chains: [mantleSepoliaTestnet],
  transports: {
    [mantleSepoliaTestnet.id]: http("https://rpc.sepolia.mantle.xyz"),
  },
});
```

### Contract ABIs

Import ABIs from the contracts package:

```typescript
import GoldTokenABI from "@/abi/GoldToken.json";
import OwnaFarmNFTABI from "@/abi/OwnaFarmNFT.json";

const CONTRACTS = {
  GOLD_TOKEN: "0x787c8616d9b8Ccdca3B2b930183813828291dA9c",
  OWNAFARM_NFT: "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7",
};
```

### Read Contract Data

```typescript
import { useReadContract } from "wagmi";

// Get available invoices
const { data: invoices } = useReadContract({
  address: CONTRACTS.OWNAFARM_NFT,
  abi: OwnaFarmNFTABI,
  functionName: "getAvailableInvoices",
  args: [0n, 10n], // offset, limit
});

// Get GOLD balance
const { data: balance } = useReadContract({
  address: CONTRACTS.GOLD_TOKEN,
  abi: GoldTokenABI,
  functionName: "balanceOf",
  args: [userAddress],
});
```

### Write Contract Data

```typescript
import { useWriteContract, useWaitForTransactionReceipt } from "wagmi";
import { parseEther } from "viem";

function InvestButton({ tokenId, amount }) {
  const { writeContract, data: hash } = useWriteContract();

  const { isLoading, isSuccess } = useWaitForTransactionReceipt({ hash });

  const handleInvest = async () => {
    // Step 1: Approve GOLD
    await writeContract({
      address: CONTRACTS.GOLD_TOKEN,
      abi: GoldTokenABI,
      functionName: "approve",
      args: [CONTRACTS.OWNAFARM_NFT, parseEther(amount.toString())],
    });

    // Step 2: Invest
    await writeContract({
      address: CONTRACTS.OWNAFARM_NFT,
      abi: OwnaFarmNFTABI,
      functionName: "invest",
      args: [tokenId, parseEther(amount.toString())],
    });
  };

  return <button onClick={handleInvest}>Buy Seed</button>;
}
```

---

## Frontend to Backend

### API Base Configuration

```typescript
// api.ts
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

### Farmer Registration

```typescript
// POST /api/farmers/register
interface FarmerRegistration {
  personalInfo: {
    fullName: string;
    email: string;
    phoneNumber: string;
    idNumber: string;
    dateOfBirth: string;
    address: string;
    province: string;
    city: string;
  };
  businessInfo: {
    businessName: string;
    businessType: string;
    npwp: string;
    bankName: string;
    bankAccountNumber: string;
    yearsOfExperience: number;
  };
  documents: {
    ktpPhoto: File;
    selfieWithKtp: File;
    npwpPhoto: File;
    bankStatement: File;
  };
}

async function registerFarmer(data: FarmerRegistration) {
  const formData = new FormData();
  // ... append data

  return fetchAPI("/api/farmers/register", {
    method: "POST",
    body: formData,
  });
}
```

### Game State Endpoints

| Endpoint                 | Method | Description                |
| ------------------------ | ------ | -------------------------- |
| `/api/user/profile`      | GET    | Get user profile and stats |
| `/api/game/water`        | POST   | Water a plant, earn XP     |
| `/api/game/daily-reward` | POST   | Claim daily reward         |
| `/api/crops/:id/cctv`    | GET    | Get CCTV link for farm     |
| `/api/leaderboard`       | GET    | Get investor rankings      |

### Example: Watering a Plant

```typescript
// POST /api/game/water
interface WaterRequest {
  cropId: string;
}

interface WaterResponse {
  success: boolean;
  xpGained: number;
  waterRemaining: number;
  newLevel?: number;
}

async function waterPlant(cropId: string): Promise<WaterResponse> {
  return fetchAPI("/api/game/water", {
    method: "POST",
    body: JSON.stringify({ cropId }),
  });
}
```

---

## Backend to Blockchain

### Go-Ethereum Setup

```go
package blockchain

import (
    "github.com/ethereum/go-ethereum/ethclient"
    "github.com/ethereum/go-ethereum/common"
)

const (
    RPC_URL = "https://rpc.sepolia.mantle.xyz"
    NFT_ADDRESS = "0xC51601dde25775bA2740EE14D633FA54e12Ef6C7"
)

func NewClient() (*ethclient.Client, error) {
    return ethclient.Dial(RPC_URL)
}
```

### Reading Contract State

```go
func GetInvoice(tokenId int64) (*Invoice, error) {
    client, _ := NewClient()

    nft, _ := NewOwnaFarmNFT(common.HexToAddress(NFT_ADDRESS), client)

    invoice, err := nft.Invoices(nil, big.NewInt(tokenId))
    if err != nil {
        return nil, err
    }

    return &Invoice{
        Farmer:      invoice.Farmer,
        TargetFund:  invoice.TargetFund,
        FundedAmount: invoice.FundedAmount,
        YieldBps:    invoice.YieldBps,
        Duration:    invoice.Duration,
        Status:      invoice.Status,
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
            log.Printf("Investment: tokenId=%d, amount=%s",
                event.TokenId, event.Amount.String())
            // Sync to database
        case err := <-sub.Err():
            return err
        case <-ctx.Done():
            return nil
        }
    }
}
```

---

## Authentication

### Privy Integration (Frontend)

```typescript
import { usePrivy } from "@privy-io/react-auth";

function AuthButton() {
  const { login, logout, authenticated, user } = usePrivy();

  if (authenticated) {
    return (
      <div>
        <span>{user?.wallet?.address}</span>
        <button onClick={logout}>Disconnect</button>
      </div>
    );
  }

  return <button onClick={login}>Connect Wallet</button>;
}
```

### JWT Verification (Backend)

```go
func AuthMiddleware() gin.HandlerFunc {
    return func(c *gin.Context) {
        token := c.GetHeader("Authorization")

        claims, err := verifyPrivyToken(token)
        if err != nil {
            c.AbortWithStatus(401)
            return
        }

        c.Set("userId", claims.UserId)
        c.Set("wallet", claims.WalletAddress)
        c.Next()
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
      toast.error("Not enough GOLD");
    } else if (error.message.includes("InvalidStatus")) {
      toast.error("Invoice not available");
    }
  }
}
```

### API Errors

```typescript
interface APIError {
  code: string;
  message: string;
}

async function handleAPICall() {
  try {
    const data = await fetchAPI("/endpoint");
    return data;
  } catch (error) {
    if (error.code === "RATE_LIMITED") {
      toast.error("Too many requests");
    }
    throw error;
  }
}
```

---

## Next: [Glossary →](../resources/glossary.md)
