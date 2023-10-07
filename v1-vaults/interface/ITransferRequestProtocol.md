# Interface for Transfer Request Protocol

This interface must be implemented for a valid TranferRequestProtocol

## Requirements

1. Must have `TransferRequest` struct defined:

```solidity
struct TransferRequest
{
	bool forERC20;
	bool forERC721;
	address creator;
	address to;
	address token;
	uint256 amount;
	uint256 created;
	uint256 tokenId;
}
```
2. Must implement the following interface:

```solidity
function yieldSyncV1Vault_transferRequestId_transferRequest(address yieldSyncV1Vault, uint256 transferRequestId) external view returns (TransferRequest memory tranferRequest);
function yieldSyncV1Vault_transferRequestId_transferRequestProcess(address yieldSyncV1Vault, uint256 transferRequestId) external;
function yieldSyncV1Vault_transferRequestId_transferRequestStatus(address yieldSyncV1Vault, uint256 transferRequestId) external view returns (bool readyToBeProcessed, bool approved, string memory message);
function yieldSyncV1VaultInitialize(address initiator, address yieldSyncV1Vault) external;
```

## Implementation Guide

### Note

1. It is up to the deployer to create their own `TransferRequestProtocol`

2. `yieldSyncV1VaultInitialize` is the function that is called when a V1 Vault is deployed. It is up to the implemented `TransferRequestProtocol` to handle any presetting before the deployment.
	- An example could be a a function for configuring the properties by the deployer called before the deployment of the V1 Vault. When configured, unpon the call of the `yieldSyncV1VaultInitialize` function the properties are handed off.

3. Keeep in mind that V1Vault will process a transaction based on `TransferRequest` struct above.

4. It is expected that the TransferRequest is deleted (if necessary) by the `yieldSyncV1Vault_transferRequestId_transferRequestProcess` function.
