# YieldSync EMP Strategy Deployment Guide

## Introduction

This guide outlines the steps for deploying and configuring an EMP Strategy. The YieldSync EMP Strategies are designed to interact with DeFi protocols with the goal to generate yield on deposited assets.

## Prerequisites

- Solidity ^0.8.18
- Hardhat or Truffle for deployment
- Access to an Ethereum network provider (Mainnet, Rinkeby, etc.)

## Deployment Steps

### 1. Deploy `YieldSyncV1EMPStrategy` Contract

Utilize the `YieldSyncV1EMPStrategyDeployer` contract to deploy an instance of `YieldSyncV1EMPStrategy` using the the following function:

```sol
function deployYieldSyncV1EMPStrategy(string memory _name, string memory _symbol)
	external
	payable
	returns (address yieldSyncV1EMPStrategy_)
;
```

This deployer will automatically register the address of the of `YieldSyncV1EMPStrategy` on the `YieldSyncV1EMPRegistry` contract. This is required so that authentication can occur on the EMP Layer.

### 2. Implement and Deploy an `IYieldSyncV1EMPStrategyInteractor` Contract

The objective of this contract should be to be able to interact with the desired DeFi protocol of choice.

This part of the deployment proccess is the most abstract aspect of the protocol. Being that the contract is only required to implement the interface, it allows the developer to chose what other functions can be programmed out.

It is also important to include functions that handle all managment of the protocol. For example functions for managing Uniswap V3 pools.

#### Requirements

1. Should implement the `IYieldSyncV1EMPStrategyInteractor` interface
2. Should hold any and all tokens related to the DeFi protocol (Ex. LP Tokens)

#### Recommendations

1. it is a good idea to include functions that allow tarnsferring out ERC20 from the smart contract in case of an emergency, adaptation of a new contract, or any other reason to withdraw ERC20
2. Make sure that the contract only allows the authorized callers to call the functions. This should include:
	a. EMPStrategy
	b. Manager of the strategy (can be referrenced from EMPStrategy or programmed out)

### 3. Implement and Deploy an `IYieldSyncV1EMPETHValueFeed` Contract

This is an instance of `IYieldSyncV1EMPETHValueFeed` that should be programmed out to provide the price of utilized tokens denominated in ETH.

This is required to be programmed out and referenced so that deposit and withdrawals cannot be switched on.

#### Considerations

If the devleoper is not interested in programming this contract from scratch an existing ETH Value Feed service can be utilized. It is up to the developer to find one.

### 4. Configure the Strategy

These can be done in any order.

#### a. Set the Utilized Tokens Purpose

Within `YieldSyncV1EMPStrategy` define the utilized ERC20 tokens, their purposes, and allocations.

ONE_HUNDRED_PERCENT is 1e18. so allocation must not exceed that amount.

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

##### Notes

The sum of all the allocations in the `Purpose[]` must add up to ONE_HUNDRED_PERCENT. Anything more or less will be invalid and cause the function to revert.

#### b. Set the Utilized Tokens Price Feed Service Contract

Within `YieldSyncV1EMPStrategy` define the price feed service contract.

```solidity
function iYieldSyncV1EMPETHValueFeedUpdate(address _iYieldSyncV1EMPETHValueFeed) external;
```

#### c. Set the Strategy Interactor Contract

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
function utilizedERC20DepositOpenToggle();
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

