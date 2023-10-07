# Yield Sync V1 Vault

This is defintion for the V1 Vaults.

## Requirements

1. Implements the IERC1271 standard

2. Must utilize the [YieldSyncV1VaultRegistry](./V1VaultRegistry.md).

	1. Store address into a variable
		- Implement getter if required

	2. Utilize the access control system of the registry
	
3. Must utilize an implementation of [TransferRequestProtocol](./TransferRequestProtocol.md).

	1. Store address into a variable
		- Implement getter if required
	
	2. Can be updated by `admins`

4. User can optionaly use a [SignatureProtocol](./SignatureProtocol.md).

	1. SignatureProtocol implements the [ERC-1271](https://eips.ethereum.org/EIPS/eip-1271) standard for signing a message

	2. The option to have a SignatureProtocol is optional for the deployer and admin

5. Using the authorization system of YieldSyncV1VaultRegistry, admins can do the following:
	1. Add another admin

	2. Remove an admin (Including self)
	
	3. Add a member

	4. Remove a member

6. Member should be able to process a transfer request by providing the ID of a <i>valid</i> TransferRequest

7. Member should be able to renounce memebership in a vault

8. Must be able to recieve funds by simple transaction address

9. Caling `yieldSyncV1Vault_transferRequestId_transferRequestProcess` function must be able transfer the following types of assets:
	
	1. Ether
	
	2. ERC-20 Tokens
	
	3. ERC-721 Tokens

## Implementation

### Solidity Interface

```solidity
function signatureProtocol() external view returns (address);
function transferRequestProtocol() external view returns (address);
function YieldSyncV1VaultRegistry() external view returns (IYieldSyncV1VaultRegistry);
function adminAdd(address targetAddress) external;
function adminRemove(address admin) external;
function memberAdd(address targetAddress) external;
function memberRemove(address member) external;
function signatureProtocolUpdate(address _signatureProtocol) external;
function transferRequestProtocolUpdate(address _transferRequestProtocol) external;
function yieldSyncV1Vault_transferRequestId_transferRequestProcess(uint256 transferRequestId) external;
function renounceMembership() external;
```
