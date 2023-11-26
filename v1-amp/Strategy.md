# Yield Sync Strategy

This is derived from the `StrategyDeployer.sol`

## Tasks

1. Should utilize an ERC-20 token <i>t</i> to keep track of position

2. Should return the amount of utilized tokens to be returned for each <i>t</i>

3. Must return the value of <i>t</i> denominated in ETH

```
t = ERC-20 strategy position t

P(t) = Price of t derived from any method such as an oracle or liquidity pool
```

## Notes
