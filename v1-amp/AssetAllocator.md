# Asset Allocator

This is derived from the `Asset Allocator Deployer`.

The objective of this smart contract is to establish a hub for directing underlying assets.

## Requirements
1. must be able to recieve and send ether, and ERC-X tokens
2. Must have a manager (AOE or Smart Contract)
3. Must be subject to some control by the yield-sync organization
4. Tokens must be able to be deposited into this contract
	1. Must have an ERC20 token position tracking system
5. Tokens must be able to be withdrawn from this contract
	1. ERC20 tokens associated must be able to be burned via this contract
6. A manager must be responsible for running the allocation function

## Optionals

1. Strategy

## Note

- Consider creating automated mechanism for determing distribution allocations