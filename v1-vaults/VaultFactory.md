# Yield Sync V1 Vault Factory

This is defintion for the V1 Vaults deployer.

## Requirements

1. Must have authorization for Yield Sync governance
1. Must store the address of the Yield Sync governance contract
2. Must store the address of the Yield Sync Registry contract
3. Must store the fee
	1. Can be 0
	2. Can be updated
	3. Must be able to transfer collected fees to specified address
4. Must keep track of vault ID
	1. Must keep track of IDs
		1. A mapping of vault address -> ID
		2. A mapping of ID -> vault address
		3. Every vault must have a unique ID
5. Must allow a AOE or Smart Contract to deploy a v1 vault

## Implementation

### Solidity Interface

```solidity
function YieldSyncGovernance() external view returns (address);
function YieldSyncV1VaultRegistry() external view returns (address);
function fee() external view returns (uint256);
function yieldSyncV1VaultIdTracker() external view returns (uint256);
function yieldSyncV1Vault_yieldSyncV1VaultId(address yieldSyncV1Vault) external view returns (uint256);
function yieldSyncV1VaultId_yieldSyncV1Vault(uint256 yieldSyncV1VaultId) external view returns (address);
function deployYieldSyncV1Vault(address signatureProtocol, address transferRequestProtocol, address[] memory admins, address[] memory members) external payable returns (address deployedYieldSyncV1Vault);
function etherTransfer(address to) external;
function feeUpdate(uint256 _fee) external;
```
