# Interface for Transfer Request Protocol

This interface must be implemented for a valid TranferRequestProtocol

## Requirements

1. Must have the provided struct available:

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