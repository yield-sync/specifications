# YieldSync EMP Strategy Deployment Guide

## Introduction

This guide outlines the steps for deploying and configuring an EMP Strategy. The YieldSync EMP Strategies are designed to interact with DeFi protocols with the goal to generate yield on deposited assets.

## Prerequisites

- Solidity ^0.8.18
- Hardhat or Truffle for deployment
- Access to an Ethereum network provider (Mainnet, Rinkeby, etc.)

## Deployment Steps

### 1. Deploy `YieldSyncV1EMPStrategy` Contract

Utilize the `YieldSyncV1EMPStrategyDeployer` contract to deploy an instance of `YieldSyncV1EMPStrategy` using the `deployYieldSyncV1EMPStrategy()` function.

This deployer will automatically register the address of the of `YieldSyncV1EMPStrategy` on the `YieldSyncV1EMPRegistry` contract. This is required so that authentication can occur on the EMP Layer can occur.

### 2. Implement and Deploy an `IYieldSyncV1EMPStrategyInteractor` Contract

This part of the deployment proccess is the most abstract aspect of the protocol. The only thing required is to implement the `IYieldSyncV1EMPStrategyInteractor` interface.

This contract should be responsible of interacting with the DeFi protocol itself as well as holding an token that is associated. That could include LP tokens or staked tokens that represent a position.

It is also important to include functions that handle all managment of the protocol. For example functions for managing Uniswap V3 pools.

### 3. Update the Strategy with Interactor Addresses

After deploying the contract that implements `IYieldSyncV1EMPStrategyInteractor`. it is time to define the address in the strategy contract.

Call the `iYieldSyncV1EMPStrategyInteractorUpdate` function on your deployed `YieldSyncV1EMPStrategy` instance contract to set the address of your strategy interactor contracts.

```solidity
// In yieldSyncV1EMPStrategy call this function
function iYieldSyncV1EMPStrategyInteractorUpdate(address interactor);
```

### 4. Set `IYieldSyncV1EMPETHValueFeed` Contract

This is the An instance of `IYieldSyncV1EMPETHValueFeed` that should be programmed out to provide the price of utilized tokens denominated in ETH.

It is required that this be programmed out otherwise the deposit and withdrawals cannot be switched on.

### 5. Configure the Strategy

#### a. Set the Utilized Tokens Purpose

Within `YieldSyncV1EMPStrategy` define the utilized ERC20 tokens, their purposes, and allocations.

```solidity
function utilizedERC20AndPurposeUpdate(address[] memory __utilizedERC20, Purpose[] memory _purpose);
```

For the above function this is the Purpose struct.

```solidity
struct Purpose
{
	bool deposit;
	bool withdraw;
	uint256 allocation;
}
```

#### b. Set the Utilized Tokens Price Feed Service Contract

Within `YieldSyncV1EMPStrategy` define the price feed service contract.

```solidity
function iYieldSyncV1EMPETHValueFeedUpdate(address _iYieldSyncV1EMPETHValueFeed)
```

### 6. Enable Depositing of ERC20

Call the function to enable depositing of the funds

```solidity
// In yieldSyncV1EMPStrategy call this function
function utilizedERC20DepositOpenToggle();
```

## Testing, Monitoring, and Management

### Testing

Conduct thorough testing to ensure that all components of your strategy work together as expected. Test the deposit, yield generation, and withdrawal functionalities.

### Monitoring

Regularly monitor the strategy's performance and exposure. Be prepared to make adjustments as needed to respond to the evolving DeFi landscape.

### Management

If the strategy needs to be managed the functions to handle these management requirements should be programmed into the `IYieldSyncV1EMPStrategyInteractor` contract.

## Conclusion

This guide provides a high-level overview of deploying and configuring the YieldSync Strategy. For more detailed information on each contract and function, refer to the specific documentation in the codebase.

