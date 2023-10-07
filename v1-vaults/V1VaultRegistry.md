# Yield Sync V1 Vault Registry

## Requirements

1. A V1Vault can call the following functions:

	1. adminAdd() - Add an address under V1Vault's address

	2. adminRemove() - Remove an address under V1Vault's address

	3. memberAdd() - Add an address under V1Vault's address

	4. memberRemovbe() - Remove an address under V1Vault's address

2. Must keep record of V1Vaults associated with an admin

3. Must keep record of admins associated with V1Vaults

4. Must keep record of V1Vaults associated with an member

5. Must keep record of member associated with V1Vaults

6. Must keep record of access to a V1Vault for each participant

## Implementation

```solidity
function admin_yieldSyncV1Vaults(address admin) external view returns (address[] memory);
function member_yieldSyncV1Vaults(address member) external view returns (address[] memory);
function yieldSyncV1Vault_admins(address yieldSyncV1Vault) external view returns (address[] memory);
function yieldSyncV1Vault_members(address yieldSyncV1Vault) external view returns (address[] memory);
function yieldSyncV1Vault_participant_access(address yieldSyncV1Vault, address participant) external view returns (bool admin, bool member);
function adminAdd(address yieldSyncV1Vault, address admin) external;
function adminRemove(address yieldSyncV1Vault, address admin) external;
function memberAdd(address yieldSyncV1Vault, address member) external;
function memberRemove(address yieldSyncV1Vault, address member) external;
```
