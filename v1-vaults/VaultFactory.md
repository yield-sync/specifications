# Yield Sync V1 Vault Factory

This is defintion for the V1 Vaults deployer.

## Requirements

1. Must have authorization for Yield Sync governance
2. Must store the address of the Yield Sync Registry contract
3. Must keep track of vault ID
	1. Must keep track of IDs
		1. A mapping of vault address -> ID
		2. A mapping of ID -> vault address
		3. Every vault must have a unique ID
4. Must have a fee
	1. Can be 0
	2. Can be updated
	3. Must be able to transfer collected fees to specified address
5. Must allow a AOE or Smart Contract to deploy a v1 vault

## Functions

`f(x) -> return`
```
YieldSyncGovernance() -> (address);
YieldSyncV1VaultRegistry() -> (address);
fee() -> (uint256);
yieldSyncV1VaultIdTracker() -> (uint256);
yieldSyncV1Vault_yieldSyncV1VaultId(address yieldSyncV1Vault) -> (uint256);
yieldSyncV1VaultId_yieldSyncV1Vault(uint256 yieldSyncV1VaultId) -> (address);
deployYieldSyncV1Vault(address signatureProtocol, address transferRequestProtocol, address[] admins, address[] members) -> (address deployedYieldSyncV1Vault);
feeUpdate(uint256 _fee);
etherTransfer(address to);
```
