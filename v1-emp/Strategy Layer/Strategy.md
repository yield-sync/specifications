# Yield Sync V1 Strategy

This is derived from `YieldSyncV1StrategyDeployer.sol`

## Objective

The objective of this smart contract is to control the strategy.

## Features

1. Utilize an ERC-20 token <i>t</i> to keep track of position which is only mintable by an EMP

2. Should return the amount of utilized tokens to be returned for each <i>t</i>

3. Must return the value of total <i>t</i> of a wallet denominated in ETH

```
t = ERC-20 strategy position t

P(t) = Price of t derived from any method such as an oracle or liquidity pool
```

## Note

This contract should be deployed before an instance of `StrategyInteractor` is deployed. This is so that the `StrategyInteractor` contract is aware of the address to provide proper authorization.

