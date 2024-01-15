# Asset Allocator

This is derived from the `AssetAllocatorDeployer.sol`

The objective of this smart contract is to establish a hub for directing underlying assets.

## Requirements

### 1. Receiving Tokens

- must be able to recieve and send ether, and ERC-X tokens

### 2. Management

-  Must have a manager (AOE or Smart Contract)
- A manager must be responsible for running the allocation function

### 3. Yield Sync DAO Control

- The Yield Sync DAO should have control over speicified processes

### 4. Deposits

- Tokens must be able to be deposited into this contract

- Upon depositing a token an ERC 20 is issued to represent the position

### 5. Withdrawals

- Tokens must be able to be withdrawn from this contract by turning in `Asset Allocator Position ERC-20`

- `Asset Allocator Position ERC-20` tokens that are submitted for cash out must be burnt

### 6. Position(s)

- Must be able to calculate the `percentAllocation` of a strategy using the following formula

```
T = set of all variants of strategy tokens

t = element of T = t ∈ T = token(s) of a strategy

a(t) = amount of tokens of a given strategy

t[i] = Single token of t

P(t[i]) Price of a single token of t (returned from the strategy)

V(t) = a(t) * P(t[i]) = value of t

h = (∑ t ∈ T V(t)) = Total holdings

PA(t) = (V(t)) / h = percent-allocation of h
```

- The strategy must return the value of the `strategy position ERC-20`

- Must be able to calculate the greatest difference in allocation-to-target. This is achieved by the following formula:

```
S = T

D = { (a(s) * P(s)) / (∑ t ∈ T a(t) * P(t)) - (n(s) / 100) | s ∈ S }

Lowest allocation = min(D)

```

## Optionals

1. Strategy

## Note

### Idea for Strategy

- Consider creating automated mechanism for determing distribution allocations

- Consider implementing an insurance mechanism