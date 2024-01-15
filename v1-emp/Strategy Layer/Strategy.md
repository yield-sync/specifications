# Yield Sync V1 Strategy

This is derived from `YieldSyncV1StrategyDeployer.sol`

## Objective

The objective of this smart contract is to control the strategy.

## Features

1. Must store the address of EMP deployer

2. Utilize an ERC-20 token <i>t</i> to keep track of position which is only mintable by an EMP

3. Should utilize some ETH value service for each utilized token.

4. Should utilize a Strategy Interactor.

```
t = ERC-20 strategy position t

P(t) = Price of t derived from any method such as an oracle or liquidity pool
```

## Note

This contract should be deployed before an instance of `StrategyInteractor` is deployed. This is so that the `StrategyInteractor` contract is aware of the address to provide proper authorization.

