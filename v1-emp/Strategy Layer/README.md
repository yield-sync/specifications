# YieldSync EMP Strategy Deployment Guide

## Introduction

This guide outlines the steps for deploying and configuring an EMP Strategy. The YieldSync EMP Strategies are designed to interact with DeFi protocols with the goal to generate yield on deposited assets.

## Prerequisites

- Solidity ^0.8.19
- Hardhat or Truffle for deployment
- Access to an Ethereum network provider (Mainnet, Rinkeby, etc.)

## Deployment Steps

### 1. Deploy `YieldSyncV1EMPStrategy` Contract

Utilize the `YieldSyncV1EMPStrategyDeployer` contract to deploy an instance of `YieldSyncV1EMPStrategy` using the following function:

```solidity
function deployYieldSyncV1EMPStrategy(string memory _name, string memory _symbol) external payable returns (address yieldSyncV1EMPStrategy_);
```

This deployer will automatically register the address of the `YieldSyncV1EMPStrategy` on the `YieldSyncV1EMPRegistry` contract. This is required so that authentication can occur on the EMP Layer when this strategy is attached to it.

### 2. Set the utilized ERC 20 Tokens

Utilize the following function on the `YieldSyncV1EMPStrategy`

```solidity
function utilizedERC20Update(address[] memory __utilizedERC20, Utilization[] memory _utilization) external;
```

### 3. Set the Price Feed Contract

Within `YieldSyncV1EMPStrategy` define the price feed service contract.

```solidity
function iYieldSyncV1EMPETHValueFeedUpdate(address _iYieldSyncV1EMPETHValueFeed) external;
```

### 3. Implement and Deploy an `IYieldSyncV1EMPStrategyInteractor` Contract

*This part of the deployment proccess is the most abstract aspect of the protocol*

The developer is required to program out a contract that interfaces and communicates with the underlying DeFi protocol. Being that the contract is only required to implement the interface, it allows the developer to be able to add as many functions as they like.

#### Requirements

1. Should implement the `IYieldSyncV1EMPStrategyInteractor` interface
2. Should hold any and all tokens related to the DeFi protocol (Ex. LP Tokens)
3. Should have all functions that handle the managment of the protocol (Ex. Uniswap V3 pools range setting)

#### Recommendations

1. It is a good idea to include functions that allow the tarnsferring of all ERC20 tokens from the smart contract in case of an emergency, migration to a new contract, etc.
2. Make sure that the contract only allows the authorized callers to call the functions. This should include:
	a. EMPStrategy
	b. Manager of the strategy (can be referrenced from EMPStrategy or programmed out)

#### Note

It is important to consider that the more complicated the contract, the less trust users may have.

### 4. Set the Strategy Interactor Contract

After deploying the contract that implements `IYieldSyncV1EMPStrategyInteractor` the devloper must define the address in the strategy contract.

Call the `iYieldSyncV1EMPStrategyInteractorUpdate()` function on your deployed `YieldSyncV1EMPStrategy` instance contract to set the address of your strategy interactor contracts.

```solidity
// In yieldSyncV1EMPStrategy call this function
function iYieldSyncV1EMPStrategyInteractorUpdate(address interactor) external;
```

### 5. Enable Depositing of ERC20

Call the function to enable depositing of the funds

```solidity
// In yieldSyncV1EMPStrategy call this function
function utilizedERC20DepositOpenToggle() external;
```

### 6. Enable Withdrawing of ERC20

Call the function to enable depositing of the funds

```solidity
// In yieldSyncV1EMPStrategy call this function
function utilizedERC20WithdrawOpenToggle() external;
```

## Testing, Monitoring, and Management

### Testing

Conduct thorough testing to ensure that all components of your strategy work together as expected. Test the deposit, yield generation, and withdrawal functionalities.

### Monitoring

Regularly monitor the strategy's performance and exposure. Be prepared to make adjustments as needed to respond to the evolving DeFi landscape.

### Management

If the strategy needs to be managed the functions to handle these management requirements should be programmed into the `IYieldSyncV1EMPStrategyInteractor` contract.

## Updating `IYieldSyncV1EMPStrategyInteractor` and/or `IYieldSyncV1EMPETHValueFeed`

If you are required to update the `IYieldSyncV1EMPStrategyInteractor` contract and/or the `IYieldSyncV1EMPETHValueFeed` then you must stop all transfer of deposting and withdrawing ERC20 tokens.

If you are going to do this, then make sure all assets are transferred out of the `IYieldSyncV1EMPStrategyInteractor`

## Conclusion

This guide provides a high-level overview of deploying and configuring the YieldSync Strategy. For more detailed information on each contract and function, refer to the specific documentation in the codebase.

