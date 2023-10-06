# Asset Allocator

This is derived from the `Asset Allocator Deployer`.

The objective of this smart contract is to establish a hub for directing underlying assets.

## Requirements

1. Must have a manager (AOE or Smart Contract)
2. Must be subject to some control by the yield-sync organization
3. Tokens must be able to be deposited into this contract
	1. Must have an ERC20 token position tracking system
4. Tokens must be able to be withdrawn from this contract
	2. ERC20 tokens associated must be able to be burned via this contract
5. A manager must be responsible for running the allocation function

## Optionals

1. Strategy
