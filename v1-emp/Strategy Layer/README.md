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

This deployer will automatically register the address of the `YieldSyncV1EMPRegistry` contract. This is required so that authentication on the EMP level can occur.

### 2. Implement and Deploy Strategy Logic Contracts

Implement a contract that contain the logic for interacting with DeFi protocols. This contracts should implement the `IYieldSyncV1EMPStrategyInteractor` interface.

This part of the deployment proccess has more abstraction then the previous step.

### 3. Update the Strategy with Interactor Addresses

Call the iYieldSyncV1EMPStrategyInteractorUpdate function on your deployed YieldSyncV1EMPStrategy instance to set the addresses of your strategy logic contracts.

```solidity
// In yieldSyncV1EMPStrategy call this function
function iYieldSyncV1EMPStrategyInteractorUpdate(address interactor);
```

### 4. Configure the Strategy

```solidity
// Context
struct Purpose
{
	bool deposit;
	bool withdraw;
	uint256 allocation;
}
````

Configure your strategy by setting utilized ERC20 tokens, their purposes, and allocations. Ensure that deposits and withdrawals are toggled as per your strategy's readiness to manage user funds.

```solidity
// In yieldSyncV1EMPStrategy call this function
function utilizedERC20AndPurposeUpdate(address[] memory __utilizedERC20, Purpose[] memory _purpose);
```

### 5. Integration Testing

Conduct thorough testing to ensure that all components of your strategy work together as expected. Test the deposit, yield generation, and withdrawal functionalities.

### 6. Enable Despotiing of ERC20

Call the function to enable depositing of the funds

```solidity
// In yieldSyncV1EMPStrategy call this function
function utilizedERC20DepositOpenToggle();
```

## Monitoring and Management

Regularly monitor the strategy's performance and exposure. Be prepared to make adjustments as needed to respond to the evolving DeFi landscape.

## Conclusion

This guide provides a high-level overview of deploying and configuring the YieldSync Strategy. For more detailed information on each contract and function, refer to the specific documentation in the codebase.

