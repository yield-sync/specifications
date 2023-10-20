# Asset Allocator

This is derived from the `AssetAllocatorDeployer.sol`

The objective of this smart contract is to establish a hub for directing underlying assets.

## Requirements

1. must be able to recieve and send ether, and ERC-X tokens

2. Must have a manager (AOE or Smart Contract)

3. Must be subject to some control by the yield-sync organization

4. Tokens must be able to be deposited into this contract

	1. Upon depositing a token an ERC 20 is issued to represent the position

5. Tokens must be able to be withdrawn from this contract by cashing out

	1. ERC20 token that is submitted must be burnt

6. A manager must be responsible for running the allocation function

7. Must be able to calculate the `percentAllocation` of a strategy using the following formula
	```
	PA = percent-allocation

	a(x) = amount of x

	P(x) = price of x

	T = set of all tokens

	t = element of T or t ∈ T

	PA = (a(t1) * P(t)) / (∑ t ∈ T a(t) * P(t))
	```
## Optionals

1. Strategy

## Note

### Idea for Strategy

- Consider creating automated mechanism for determing distribution allocations

- Consider implementing an insurance mechanism