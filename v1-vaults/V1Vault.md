# Yield Sync V1 Vault

This is defintion for the V1 Vaults.

## Requirements

1. Implements the IERC1271 standard

2. Implements [OpenZeppelin](https://www.openzeppelin.com/)'s ReentrancyGuard

3. Must utilize a [YieldSyncV1VaultRegistry](./V1VaultRegistry.md) implementation.
	1. Store address into a variable
	
4. Must utilize a [TransferRequestProtocol](./TransferRequestProtocol.md) implementation.
	1. Store address into a variable
	2. Can be updated by `admins`

5. User can assign a signatureProtocol for signing a message
	1. In Solidity this is the [ERC-1271](https://eips.ethereum.org/EIPS/eip-1271) standard 

6. 

## Deployment Process

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
