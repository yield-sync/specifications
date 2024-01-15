# Yield Sync V1 Strategy Controller

This is derived from `YieldSyncV1StrategyControllerDeployer.sol`

## Objective

The objective of this smart contract is to control the strategy.

## Tasks

1. Should utilize an ERC-20 token <i>t</i> to keep track of position

2. Should return the amount of utilized tokens to be returned for each <i>t</i>

3. Must return the value of total <i>t</i> of a wallet denominated in ETH

```
t = ERC-20 strategy position t

P(t) = Price of t derived from any method such as an oracle or liquidity pool
```

## Note

This should be deployed before the strategy so that the strategy is aware of the address of the controller and provides it the authorization it needs.

