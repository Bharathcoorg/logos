# Edgeverse Chain: System Architecture and Product Specification

**Version:** 1.0  
**Date:** 2025  
**Author:** Edgeverse Team

## Executive Summary

Edgeverse Chain is a next-generation blockchain platform built on the Abundance ABC Stack, a high-performance Rollup L1 framework that achieves throughput of 1 Gigagas per second. As a sovereign rollup using Celestia for data availability and consensus, Edgeverse provides a comprehensive ecosystem for extending DeFi, gaming, and other high-speed execution activities for the Substrate ecosystem. The platform leverages the ABC Stack's exceptional performance capabilities along with verifier nodes and TSS-controlled vaults to power key operations including bridging, swapping, staking, and yield routing.

Rather than keeping locked assets idle, Edgeverse moves them to TSS vaults and enables the use of native tokens on the Edgeverse chain, allowing users to interact with EVM dApps instantly using their Substrate wallets. Every account on Edgeverse chain has an Substrate address mapped to it with lock and mint logic, enabling seamless interaction between different blockchain ecosystems. This architecture is specifically designed to support applications that require web2-like performance with blockchain security, including fully on-chain games, high-throughput DeFi protocols, and compute-intensive applications.

This document provides a detailed overview of the Edgeverse Chain architecture, its core components, product flows, and technical specifications.

## Table of Contents

1. [Introduction](#1-introduction)
2. [System Architecture Overview](#2-system-architecture-overview)
3. [Core Components](#3-core-components)
4. [Product Modules](#4-product-modules)
   - [Substrate Adopter](#41-substrate-adopter)
   - [EdgeBridge](#42-edgebridge)
     - [Standard Bridge](#421-standard-bridge)
     - [Fast Bridge](#422-fast-bridge)
     - [Yield Routes](#423-yield-routes)
     - [Whitelisted dApp Contracts](#424-whitelisted-dapp-contracts)
   - [EdgeSwap](#43-edgeswap)
   - [SCO (Staked Coin Offering)](#44-sco-staked-coin-offering)
   - [EdgeName Service](#45-edgename-service)
   - [EVM DeFi Access](#46-evm-defi-access)
   - [Memecoin Launcher](#47-memecoin-launcher)
5. [Edgeverse Pallet](#5-edgeverse-pallet)
6. [Gas Fee Model](#6-gas-fee-model)
7. [Security Model](#7-security-model)
8. [Conclusion](#8-conclusion)

## 1. Introduction

### 1.1 Vision and Mission

Edgeverse Chain aims to create a seamless, secure, and efficient blockchain ecosystem that enables native asset interoperability across multiple chains. Our mission is to provide a comprehensive platform that supports the full spectrum of DeFi activities while maintaining the highest standards of security and user experience.

### 1.2 Key Differentiators

- **Native Asset Support**: Use tokens like DOT, KSM, BTC, ETH directly without wrapping
- **TSS-Based Security**: Distributed key management for cross-chain operations
- **High-Speed Execution**: 1 Gigagas/second throughput for web2-like performance
- **Yield Generation**: Built-in DeFi capabilities for all supported assets
- **Modular Architecture**: Separation of concerns between execution, data availability, and settlement
- **EVM Compatibility**: Every account mapped to EVM address for seamless interaction
- **EVM-Based DeFi for Substrate**: Enabling Substrate users to access EVM DeFi ecosystem
- **Memecoin Launcher**: Pump.fun-style platform for creating and trading tokens using native assets
- **Substrate Integration**: Direct interaction using Substrate wallets for all operations

### 1.3 Target Use Cases

- Cross-chain asset transfers and swaps
- Staking and yield farming across multiple chains
- EVM-based DeFi access for Substrate token holders
- High-performance on-chain gaming and metaverse applications
- Memecoin creation and trading with native assets
- Decentralized applications requiring multi-chain functionality
- Enterprise solutions needing secure cross-chain operations

## 2. System Architecture Overview

Edgeverse Chain is built on the Abundance ABC Stack, a sovereign rollup L1 framework that completely decouples bridge functionality from the execution layer and leverages Celestia for consensus and data availability. This provides a modular architecture that achieves exceptional throughput by focusing solely on efficient execution while enabling modular bridging solutions based on specific application needs.

### 2.1 High-Level Architecture

The Edgeverse ecosystem consists of the following key components:

1. **Abundance ABC Stack**: The core blockchain built as a sovereign rollup L1 framework with 1 Gigagas/second throughput
2. **Celestia Integration**: Provides data availability and consensus for the rollup
3. **Edgeverse Pallet**: Specialized module for TSS coordination and cross-chain operations
4. **Verifier Node Network**: Validates cross-chain operations and maintains security
5. **TSS-Controlled Vaults**: Secure multi-signature vaults for asset custody
6. **Light Clients**: Enable efficient verification of cross-chain transactions

### 2.2 Architecture Diagram

```
+-------------------------------------+
|        Edgeverse Ecosystem          |
+-------------------------------------+
|                                     |
|  +-------------------------------+  |
|  |   Abundance ABC Stack         |  |
|  |   Sovereign Rollup L1         |  |
|  |   - 1 Gigagas/second          |  |
|  |   - Edgeverse Pallet          |  |
|  |   - Celestia Integration      |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   Verifier Node Network       |  |
|  |   - Cross-chain Validation    |  |
|  |   - Event Monitoring          |  |
|  |   - Proof Generation          |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   TSS-Controlled Vaults       |  |
|  |   - Multi-sig Asset Custody   |  |
|  |   - Threshold Signatures      |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   Product Modules             |  |
|  |   - Substrate Adopter         |  |
|  |   - EdgeBridge                |  |
|  |     - Standard Bridge         |  |
|  |     - Fast Bridge            |  |
|  |     - Yield Routes           |  |
|  |     - Whitelisted dApps      |  |
|  |   - EdgeSwap                  |  |
|  |   - SCO                       |  |
|  |   - EdgeName Service          |  |
|  |   - EVM DeFi Access           |  |
|  |   - Memecoin Launcher         |  |
|  +-------------------------------+  |
|                                     |
+-------------------------------------+
```

### 2.3 Technical Stack

- **Blockchain Framework**: Abundance ABC Stack (Sovereign Rollup L1)
- **Data Availability & Consensus**: Celestia
- **Execution Performance**: 1 Gigagas per second throughput
- **Smart Contract Support**: EVM compatibility
- **Cross-Chain Protocol**: TSS-based bridging with verifier attestations
- **Storage Layer**: Rollup state storage + Celestia for data availability

## 3. Core Components

### 3.1 Abundance ABC Stack

The Edgeverse Chain is built on the Abundance ABC Stack, a high-performance sovereign rollup L1 framework, providing a flexible and modular blockchain platform with the following features:

- **Sovereign Rollup Architecture**: Complete decoupling of bridge functionality from execution layer
- **Celestia Integration**: Leverages Celestia for data availability and consensus
- **High Throughput**: Achieves 1 Gigagas per second execution capacity
- **Modular Design**: Separation of concerns between different blockchain functions
- **Governance**: On-chain governance for protocol upgrades and parameter changes
- **State Management**: Efficient state storage and transition mechanisms
- **Event System**: Comprehensive event emission for tracking
- **EVM Compatibility**: Every account has an EVM address mapping for seamless interaction
- **Optimized Execution**: Focus solely on efficient execution without settlement layer constraints
- **Parallel Processing**: Handle multiple operations simultaneously

### 3.2 Verifier Node Network

Verifier nodes form a decentralized network responsible for validating cross-chain operations:

- **Event Monitoring**: Track events across multiple blockchains
- **Proof Generation**: Create cryptographic proofs of events
- **Consensus**: Reach agreement on the validity of operations
- **Attestation**: Sign messages confirming the validity of transactions
- **Slashing**: Face penalties for malicious or incorrect behavior

### 3.3 TSS-Controlled Vaults

TSS (Threshold Signature Scheme) vaults provide secure custody for assets across multiple chains:

- **Distributed Key Generation**: No single entity holds the complete private key
- **Threshold Signatures**: Require multiple parties to sign transactions
- **Multi-Chain Support**: Manage assets on various blockchains
- **Secure Operations**: Execute transactions based on verifier consensus
- **Active Asset Management**: Rather than keeping assets idle, they can be deployed to generate yield

### 3.4 Light Clients

Light clients enable efficient verification of cross-chain transactions:

- **Header Verification**: Validate blockchain headers without full node requirements
- **Proof Verification**: Check the validity of transaction proofs
- **Resource Efficiency**: Operate with minimal computational resources
- **Cross-Chain Communication**: Enable secure interaction between chains

## 4. Product Modules

### 4.1 Substrate Adopter

The Substrate Adopter module enables the use of native Substrate tokens (DOT, KSM, etc.) on Edgeverse without traditional bridging.

#### 4.1.1 Key Features

- **Native Token Support**: Use DOT, KSM, and other Substrate tokens directly
- **Lockproof Validation**: Verify token locks via light clients and verifiers
- **Virtual Balance Registry**: Track token balances across chains
- **Universal Compatibility**: Use adopted tokens across all Edgeverse modules

#### 4.1.2 Technical Implementation

- **Light Client Integration**: Verify Substrate chain state
- **Verifier Consensus**: Validate token locks and releases
- **Virtual Registry**: Maintain a registry of adopted token balances
- **Cross-Module Compatibility**: Enable adopted tokens in all platform features

#### 4.1.3 Substrate Adopter Flow

```
+-------------+     +-----------------+     +----------------+     +----------------+
| User        |     | Source Chain    |     | Verifier Nodes |     | Edgeverse     |
| (with DOT)  |     | (Polkadot)      |     |                |     | Chain         |
+-------------+     +-----------------+     +----------------+     +----------------+
       |                    |                       |                      |
       | Lock DOT           |                       |                      |
       |-------------------->                       |                      |
       |                    | Emit Lock Event       |                      |
       |                    |----------------------->                      |
       |                    |                       | Validate Lockproof   |
       |                    |                       |------------------+   |
       |                    |                       |                  |   |
       |                    |                       |<-----------------+   |
       |                    |                       |                      |
       |                    |                       | Move to TSS Vault    |
       |                    |                       |------------------+   |
       |                    |                       |                  |   |
       |                    |                       |<-----------------+   |
       |                    |                       |                      |
       |                    |                       | Update Virtual       |
       |                    |                       | Registry & Mint      |
       |                    |                       |---------------------->
       |                    |                       |                      |
       |                    |                       |                      | Register vDOT
       |                    |                       |                      | to User's
       |                    |                       |                      | Substrate/EVM
       |                    |                       |                      | Account
       |                    |                       |                      |-------------+
       |                    |                       |                      |             |
       |                    |                       |                      |<------------+
       |                    |                       |                      |
       |                    |                       | Confirm Update       |
       |                    |                       |<----------------------
       |                    |                       |                      |
       | Notification       |                       |                      |
       <--------------------|------------------------|----------------------
       |                    |                       |                      |
       | Use vDOT in        |                       |                      |
       | Edgeverse DeFi     |                       |                      |
       |---------------------------------------------------------->       |
       |                    |                       |                      |
       |                    |                       |                      | Process
       |                    |                       |                      | Transaction
       |                    |                       |                      |-------------+
       |                    |                       |                      |             |
       |                    |                       |                      |<------------+
       |                    |                       |                      |
       | Confirmation       |                       |                      |
       <----------------------------------------------------------|       |
       |                    |                       |                      |
```

**Flow Explanation:**

1. User locks DOT on the Polkadot chain
2. The lock event is emitted and detected by verifier nodes
3. Verifiers validate the lockproof using light clients
4. Instead of keeping assets idle, verifiers move the locked DOT to TSS vaults
5. Verifiers update the virtual registry and mint equivalent vDOT on Edgeverse
6. The minted vDOT is registered to the user's Substrate address (which is mapped to an EVM account)
7. User receives notification of successful adoption
8. User can now use vDOT across all Edgeverse modules, including EVM dApps
9. When returning, vDOT is burned and native DOT is released from the TSS vault

### 4.2 EdgeBridge

EdgeBridge is a TSS-based cross-chain bridge that enables secure and efficient asset transfers between Edgeverse and other blockchains. It includes standard bridging, fast bridging, yield routes, and support for whitelisted dApps.

#### 4.2.1 Standard Bridge

The standard bridge provides secure and reliable asset transfers between chains.

**Key Features:**
- Native token bridge using threshold-signature-controlled vaults
- Support for BTC, ETH, DOT, KSM, and other chains
- Verifier-based validation of lock/unlock events
- Comprehensive audit trail for all operations

**Standard Bridge Flow:**

```
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
| User        |     | Source Chain    |     | Verifier Nodes |     | TSS Vault     |     | Edgeverse     |
| (with ETH)  |     | (Ethereum)      |     |                |     |                |     | Chain         |
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
       |                    |                       |                      |                      |
       | Deposit ETH        |                       |                      |                      |
       |-------------------->                       |                      |                      |
       |                    | Lock in TSS Vault     |                      |                      |
       |                    |--------------------------------------------->                      |
       |                    |                       |                      |                      |
       |                    | Emit Deposit Event    |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Validate Deposit     |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Generate Proof       |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Request Mint         |                      |
       |                    |                       |------------------------------------------------->
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Mint vETH to
       |                    |                       |                      |                      | User's Account
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       | Confirm Mint         |                      |
       |                    |                       |<-------------------------------------------------
       |                    |                       |                      |                      |
       | Notification       |                       |                      |                      |
       <--------------------|------------------------|----------------------|----------------------
       |                    |                       |                      |                      |
       | Use vETH on        |                       |                      |                      |
       | Edgeverse          |                       |                      |                      |
       |---------------------------------------------------------->       |                      |
       |                    |                       |                      |                      |
```

**Flow Explanation:**

1. User deposits ETH on Ethereum
2. ETH is locked in a TSS vault
3. Verifier nodes validate the deposit
4. Verifiers generate a cryptographic proof
5. Verifiers enable ETH usage on Edgeverse
6. Edgeverse enables ETH usage in the user's account (with mapped EVM address)
7. User receives notification of successful bridge
8. User can now use ETH on Edgeverse, including in EVM dApps
9. When bridging back, ETH access is revoked and native ETH is released from the TSS vault

#### 4.2.2 Fast Bridge

The Fast Bridge provides near-instant asset transfers using dedicated liquidity pools.

**Key Features:**
- Immediate token availability through liquidity pools
- Higher fees to compensate liquidity providers
- Background settlement for pool rebalancing
- Same security guarantees as the standard bridge

**Fast Bridge Flow:**

```
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
| User        |     | Source Chain    |     | Verifier Nodes |     | Liquidity Pool |     | Edgeverse     |
| (with BTC)  |     | (Bitcoin)       |     |                |     |                |     | Chain         |
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
       |                    |                       |                      |                      |
       | Deposit BTC        |                       |                      |                      |
       |-------------------->                       |                      |                      |
       |                    | Lock in TSS Vault     |                      |                      |
       |                    |--------------------------------------------->                      |
       |                    |                       |                      |                      |
       |                    | Emit Deposit Event    |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Validate Deposit     |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Request Fast Release |                      |
       |                    |                       |--------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Request Mint         |
       |                    |                       |                      |--------------------->
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Mint vBTC to
       |                    |                       |                      |                      | User's Account
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       |                      | Confirm Mint         |
       |                    |                       |                      |<---------------------|
       |                    |                       |                      |                      |
       | Notification       |                       |                      |                      |
       <--------------------|------------------------|----------------------|----------------------
       |                    |                       |                      |                      |
       | Use vBTC on        |                       |                      |                      |
       | Edgeverse          |                       |                      |                      |
       |---------------------------------------------------------->       |                      |
       |                    |                       |                      |                      |
       |                    |                       | Process Background   |                      |
       |                    |                       | Settlement           |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Rebalance Pool       |                      |
       |                    |                       |--------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Update Balances      |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
```

**Flow Explanation:**

1. User deposits BTC on Bitcoin
2. BTC is locked in a TSS vault
3. Verifier nodes validate the deposit
4. Verifiers request fast release from the liquidity pool
5. Liquidity pool enables BTC usage on Edgeverse
6. Edgeverse enables BTC usage in the user's account (with mapped EVM address)
7. User receives notification of successful bridge
8. User can immediately use BTC on Edgeverse
9. In the background, verifiers process the settlement and rebalance the liquidity pool

#### 4.2.3 Yield Routes

Yield Routes enable locked assets to generate returns while they're in TSS vaults.

**Key Features:**
- Locked assets deployed to yield-generating protocols
- Yield shared among users, validators, and treasury
- Risk management through diversification
- Optional participation with user consent

**Yield Route Flow:**

```
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
| User        |     | TSS Vault       |     | Verifier Nodes |     | Yield Protocol |     | Edgeverse     |
| (with vDOT) |     | (with DOT)      |     |                |     |                |     | Chain         |
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
       |                    |                       |                      |                      |
       | Opt-in for         |                       |                      |                      |
       | Yield Generation   |                       |                      |                      |
       |---------------------------------------------------------->       |                      |
       |                    |                       |                      |                      |
       |                    |                       | Analyze Yield        |                      |
       |                    |                       | Opportunities        |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Select Optimal       |                      |
       |                    |                       | Strategy             |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    | Request Asset         |                      |                      |
       |                    | Deployment            |                      |                      |
       |                    <-----------------------|                      |                      |
       |                    |                       |                      |                      |
       |                    | Approve Deployment    |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    | Deploy Assets         |                      |                      |
       |                    |--------------------------------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Generate Yield       |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
       |                    | Collect Yield         |                      |                      |
       |                    |<---------------------------------------------|                      |
       |                    |                       |                      |                      |
       |                    | Report Yield          |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Calculate            |                      |
       |                    |                       | Distribution         |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Update Yield         |                      |
       |                    |                       | Registry             |                      |
       |                    |                       |------------------------------------------------->
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Record Yield
       |                    |                       |                      |                      | Distribution
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       | Confirm Update       |                      |
       |                    |                       |<-------------------------------------------------
       |                    |                       |                      |                      |
       | Yield Report       |                       |                      |                      |
       <--------------------|------------------------|----------------------|----------------------
       |                    |                       |                      |                      |
```

**Flow Explanation:**

1. User opts in for yield generation on their locked assets
2. Verifiers analyze yield opportunities across protocols
3. Verifiers select the optimal strategy based on risk/reward
4. TSS vault approves asset deployment
5. Assets are deployed to the selected yield protocol
6. Protocol generates yield over time
7. TSS vault collects the generated yield
8. Verifiers calculate the distribution (users, validators, treasury)
9. Yield distribution is recorded on Edgeverse chain
10. User receives a yield report

#### 4.2.4 Whitelisted dApp Contracts

Whitelisted dApp Contracts receive special incentives to encourage integration with the Edgeverse ecosystem.

**Key Features:**
- Double reward incentives for whitelisted contracts
- Special benefits for contracts using Substrate tokens
- Governance approval process for whitelisting
- Enhanced user rewards for interacting with whitelisted dApps

**Whitelisted dApp Flow:**

```
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
| Developer   |     | Governance      |     | Edgeverse     |     | Whitelisted    |     | User          |
|             |     | Module          |     | Chain         |     | Contract       |     |               |
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
       |                    |                       |                      |                      |
       | Submit Contract    |                       |                      |                      |
       | for Whitelist      |                       |                      |                      |
       |-------------------->                       |                      |                      |
       |                    |                       |                      |                      |
       |                    | Review Contract       |                      |                      |
       |                    |------------------+    |                      |                      |
       |                    |                  |    |                      |                      |
       |                    |<-----------------+    |                      |                      |
       |                    |                       |                      |                      |
       |                    | Approve Contract      |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Add to Whitelist     |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Configure Rewards    |                      |
       |                    |                       |--------------------->                      |
       |                    |                       |                      |                      |
       | Notify Approval    |                       |                      |                      |
       <--------------------|                       |                      |                      |
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Interact with
       |                    |                       |                      |                      | Contract
       |                    |                       |                      <---------------------|
       |                    |                       |                      |                      |
       |                    |                       |                      | Process Interaction  |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
       |                    |                       |                      | Request Enhanced     |
       |                    |                       |                      | Rewards              |
       |                    |                       |                      |--------------------->
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Verify Whitelist
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Apply Double
       |                    |                       |                      |                      | Rewards
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Distribute
       |                    |                       |                      |                      | Rewards
       |                    |                       |                      |                      |------------>
       |                    |                       |                      |                      |
```

**Flow Explanation:**

1. Developer submits their contract for whitelist consideration
2. Governance reviews the contract for security and compatibility
3. Upon approval, the contract is added to the whitelist registry
4. Enhanced reward configuration is applied to the contract
5. Developer is notified of the approval
6. User interacts with the whitelisted contract
7. Contract processes the interaction
8. Contract requests enhanced rewards for the user
9. Edgeverse verifies the contract's whitelist status
10. Double rewards are applied
11. Rewards are distributed to the user

### 4.3 EdgeSwap

EdgeSwap is an AMM DEX that enables cross-chain swaps using native assets without wrapping.

#### 4.3.1 Key Features

- **Cross-Chain Swaps**: Swap between tokens on different chains
- **Native Asset Support**: No wrapped tokens required
- **EDG Token Routing**: Use EDG for efficient routing and settlement
- **Reward Distribution**: 75% LP reward share + protocol yield split

#### 4.3.2 Technical Implementation

- **AMM Pools**: Automated Market Maker liquidity pools
- **Offchain Route Calculation**: Compute optimal swap routes offchain
- **TSS Vault Integration**: Secure asset custody during swaps
- **Settlement Mechanism**: Finalize swaps with verifier confirmation

#### 4.3.3 EdgeSwap Flow

```
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
| User        |     | Edgeverse      |     | Offchain       |     | TSS Vault     |     | External       |
| (with DOT)  |     | Chain          |     | Router         |     |                |     | Chain          |
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
       |                    |                       |                      |                      |
       | Request Swap       |                       |                      |                      |
       | DOT -> ETH         |                       |                      |                      |
       |-------------------->                       |                      |                      |
       |                    |                       |                      |                      |
       |                    | Forward Request       |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Calculate Route      |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Request DOT Lock     |                      |
       |                    |                       |---------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Lock DOT             |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
       |                    |                       | Confirm Lock         |                      |
       |                    |                       |<----------------------                      |
       |                    |                       |                      |                      |
       |                    |                       | Request ETH Release  |                      |
       |                    |                       |---------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Release ETH          |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
       |                    |                       | Confirm Release      |                      |
       |                    |                       |<----------------------                      |
       |                    |                       |                      |                      |
       |                    |                       | Update Balances      |                      |
       |                    |                       |---------------------->                      |
       |                    |                       |                      |                      |
       |                    | Confirm Swap          |                      |                      |
       |                    <-----------------------|                      |                      |
       |                    |                       |                      |                      |
       | Receive ETH        |                       |                      |                      |
       <--------------------|                       |                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Background Cross-Chain Settlement           |
       |                    |                       |------------------------------------------------->
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Process
       |                    |                       |                      |                      | Settlement
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       | Confirm Settlement   |                      |
       |                    |                       |<-------------------------------------------------
       |                    |                       |                      |                      |
```

**Flow Explanation:**

1. User requests to swap DOT for ETH on Edgeverse
2. Request is forwarded to the offchain router
3. Router calculates the optimal swap route
4. Router requests locking of user's DOT in the TSS vault
5. TSS vault confirms the lock
6. Router requests release of ETH from the TSS vault
7. TSS vault releases ETH
8. Router updates balances on Edgeverse
9. Swap is confirmed and user receives ETH
10. In the background, the router handles cross-chain settlement if needed
11. External chain processes the settlement
12. Settlement is confirmed back to the router

### 4.4 SCO (Staked Coin Offering)

SCO is a staking platform that allows users to commit EDG or adopted tokens to earn project-based rewards.

#### 4.4.1 Key Features

- **Flexible Staking**: Stake EDG or adopted tokens
- **Project-Based APYs**: Earn rewards from specific projects
- **Multiple Lock Durations**: 30/180/365 days options
- **TSS-Based Distribution**: Secure reward distribution via TSS vaults

#### 4.4.2 Technical Implementation

- **Staking Contracts**: Manage token locks and rewards
- **Verifier Tracking**: Monitor staking periods and conditions
- **TSS Distribution**: Distribute rewards via secure vaults
- **Fee Structure**: 1% claim fee (35% validators, 35% verifiers, 30% treasury)

#### 4.4.3 SCO Flow

```
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
| User        |     | Edgeverse      |     | Verifier       |     | TSS Vault     |     | Project        |
| (with EDG)  |     | Chain          |     | Network        |     |                |     | Token          |
+-------------+     +-----------------+     +----------------+     +----------------+     +----------------+
       |                    |                       |                      |                      |
       | Stake EDG          |                       |                      |                      |
       | (180-day lock)     |                       |                      |                      |
       |-------------------->                       |                      |                      |
       |                    |                       |                      |                      |
       |                    | Lock EDG in Vault     |                      |                      |
       |                    |--------------------------------------------->                      |
       |                    |                       |                      |                      |
       |                    | Emit Stake Event      |                      |                      |
       |                    |----------------------->                      |                      |
       |                    |                       |                      |                      |
       |                    |                       | Track Staking Period |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | ... (180 days) ...   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Maturity Reached     |                      |
       |                    |                       |------------------+   |                      |
       |                    |                       |                  |   |                      |
       |                    |                       |<-----------------+   |                      |
       |                    |                       |                      |                      |
       |                    |                       | Request Reward       |                      |
       |                    |                       | Distribution         |                      |
       |                    |                       |--------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Request Project      |
       |                    |                       |                      | Tokens               |
       |                    |                       |                      |--------------------->
       |                    |                       |                      |                      |
       |                    |                       |                      |                      | Release Tokens
       |                    |                       |                      |                      |-------------+
       |                    |                       |                      |                      |             |
       |                    |                       |                      |                      |<------------+
       |                    |                       |                      |                      |
       |                    |                       |                      | Prepare Distribution |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
       |                    |                       | Notify Maturity      |                      |
       |                    |                       |----------------------|--------------------->
       |                    |                       |                      |                      |
       |                    | Update Stake Status   |                      |                      |
       |                    <-----------------------|                      |                      |
       |                    |                       |                      |                      |
       | Notify Claim Ready |                       |                      |                      |
       <--------------------|                       |                      |                      |
       |                    |                       |                      |                      |
       | Claim Rewards      |                       |                      |                      |
       |-------------------->                       |                      |                      |
       |                    |                       |                      |                      |
       |                    | Request Distribution  |                      |                      |
       |                    |--------------------------------------------->                      |
       |                    |                       |                      |                      |
       |                    |                       |                      | Release EDG +        |
       |                    |                       |                      | Project Tokens       |
       |                    |                       |                      |------------------+   |
       |                    |                       |                      |                  |   |
       |                    |                       |                      |<-----------------+   |
       |                    |                       |                      |                      |
       |                    | Confirm Distribution  |                      |                      |
       |                    <----------------------------------------------|                      |
       |                    |                       |                      |                      |
       | Receive Tokens     |                       |                      |                      |
       <--------------------|                       |                      |                      |
       |                    |                       |                      |                      |
```

**Flow Explanation:**

1. User stakes EDG for a 180-day lock period
2. EDG is locked in the TSS vault
3. Stake event is emitted and detected by verifiers
4. Verifiers track the staking period
5. After 180 days, maturity is reached
6. Verifiers request reward distribution from the TSS vault
7. TSS vault requests project tokens
8. Project releases tokens to the TSS vault
9. TSS vault prepares the distribution
10. Verifiers notify Edgeverse chain of maturity
11. User is notified that rewards are ready to claim
12. User claims rewards
13. Edgeverse requests distribution from TSS vault
14. TSS vault releases EDG (principal) plus project tokens (rewards)
15. Distribution is confirmed and user receives tokens

### 4.5 EdgeName Service

EdgeName Service provides a readable naming system for blockchain addresses across the ecosystem.

#### 4.5.1 Key Features

- **Readable Names**: user@dot, user@edg, etc.
- **Cross-Chain Resolution**: Map to Substrate/EVM addresses
- **Verifier Resolution**: Names resolved via verifier network
- **Governance Control**: Prefix whitelisting via governance

#### 4.5.2 Technical Implementation

- **Name Registry**: Store name-to-address mappings
- **Resolution Protocol**: Resolve names to addresses
- **Verifier Consensus**: Validate name registrations and updates
- **Governance Integration**: Manage prefix whitelisting

#### 4.5.3 EdgeName Flow

```
+-------------+     +-----------------+     +----------------+     +----------------+
| User        |     | Edgeverse      |     | Verifier       |     | Name           |
|             |     | Chain          |     | Network        |     | Registry       |
+-------------+     +-----------------+     +----------------+     +----------------+
       |                    |                       |                      |
       | Register           |                       |                      |
       | "alice@edg"        |                       |                      |
       |-------------------->                       |                      |
       |                    |                       |                      |
       |                    | Verify Availability   |                      |
       |                    |--------------------------------------------->
       |                    |                       |                      |
       |                    |                       |                      | Check Registry
       |                    |                       |                      |-------------+
       |                    |                       |                      |             |
       |                    |                       |                      |<------------+
       |                    |                       |                      |
       |                    | Confirm Availability  |                      |
       |                    <---------------------------------------------|
       |                    |                       |                      |
       |                    | Emit Registration     |                      |
       |                    | Event                 |                      |
       |                    |----------------------->                      |
       |                    |                       |                      |
       |                    |                       | Validate Registration|
       |                    |                       |------------------+   |
       |                    |                       |                  |   |
       |                    |                       |<-----------------+   |
       |                    |                       |                      |
       |                    |                       | Update Registry      |
       |                    |                       |--------------------->
       |                    |                       |                      |
       |                    |                       |                      | Store Mapping
       |                    |                       |                      |-------------+
       |                    |                       |                      |             |
       |                    |                       |                      |<------------+
       |                    |                       |                      |
       |                    |                       | Confirm Update       |
       |                    |                       <---------------------|
       |                    |                       |                      |
       |                    | Registration Complete |                      |
       |                    <-----------------------|                      |
       |                    |                       |                      |
       | Confirm Registration|                      |                      |
       <--------------------|                       |                      |
       |                    |                       |                      |
```

**Flow Explanation:**

1. User requests to register "alice@edg"
2. Edgeverse checks name availability in the registry
3. Registry confirms availability
4. Registration event is emitted and detected by verifiers
5. Verifiers validate the registration request
6. Verifiers update the name registry
7. Registry stores the name-to-address mapping
8. Update is confirmed back to verifiers
9. Registration completion is confirmed to Edgeverse
10. User receives confirmation of successful registration

### 4.6 EVM DeFi Access

The EVM DeFi Access module enables Substrate token holders to seamlessly participate in EVM-based DeFi protocols without requiring technical knowledge of different ecosystems.

#### 4.6.1 Key Features

- **Substrate-to-EVM Bridge**: Direct access to EVM DeFi for Substrate users
- **Wallet Integration**: Use Substrate wallets to interact with EVM protocols
- **Protocol Aggregation**: Access multiple EVM DeFi protocols through a unified interface
- **Yield Optimization**: Automated strategies for maximizing returns across EVM protocols
- **Risk Assessment**: Protocol risk scoring and monitoring
- **Gas Optimization**: Efficient transaction batching and gas management

#### 4.6.2 Technical Implementation

- **Account Mapping**: Automatic mapping between Substrate and EVM addresses
- **Transaction Routing**: Intelligent routing of transactions between ecosystems
- **Protocol Adapters**: Standardized interfaces for various EVM DeFi protocols
- **Yield Aggregator**: Optimization algorithms for yield farming
- **Risk Oracle**: Real-time risk assessment of protocols

#### 4.6.3 EVM DeFi Access Flow

```
+-------------+     +-----------------+     +----------------+     +----------------+
| User        |     | Edgeverse      |     | Protocol       |     | EVM DeFi       |
| (Substrate) |     | Chain          |     | Router         |     | Protocol       |
+-------------+     +-----------------+     +----------------+     +----------------+
       |                    |                       |                      |
       | Request DeFi       |                       |                      |
       | Interaction        |                       |                      |
       |-------------------->                       |                      |
       |                    |                       |                      |
       |                    | Forward Request       |                      |
       |                    |----------------------->                      |
       |                    |                       |                      |
       |                    |                       | Prepare Transaction  |
       |                    |                       |------------------+   |
       |                    |                       |                  |   |
       |                    |                       |<-----------------+   |
       |                    |                       |                      |
       |                    |                       | Execute via          |
       |                    |                       | Mapped EVM Address   |
       |                    |                       |---------------------->
       |                    |                       |                      |
       |                    |                       |                      | Process
       |                    |                       |                      | Transaction
       |                    |                       |                      |-------------+
       |                    |                       |                      |             |
       |                    |                       |                      |<------------+
       |                    |                       |                      |
       |                    |                       | Confirm Execution    |
       |                    |                       <----------------------|
       |                    |                       |                      |
       |                    | Return Result         |                      |
       |                    <-----------------------|                      |
       |                    |                       |                      |
       | Transaction        |                       |                      |
       | Confirmation       |                       |                      |
       <--------------------|                       |                      |
       |                    |                       |                      |
```

**Flow Explanation:**

1. User initiates a DeFi interaction using their Substrate wallet
2. Edgeverse forwards the request to the Protocol Router
3. Router prepares the transaction for the target EVM protocol
4. Router executes the transaction using the user's mapped EVM address
5. EVM DeFi protocol processes the transaction
6. Protocol confirms execution to the Router
7. Router returns the result to Edgeverse
8. User receives confirmation of the successful interaction

### 4.7 Memecoin Launcher

The Memecoin Launcher provides a pump.fun-style platform for creating and trading tokens using native assets directly from Substrate wallets.

#### 4.7.1 Key Features

- **One-Click Token Creation**: Create new tokens with minimal effort
- **Native Asset Support**: Use any supported native asset for token creation and trading
- **Direct Substrate Wallet Integration**: Create and trade tokens directly using Substrate wallets
- **Automated Liquidity Pool Creation**: Instant liquidity for new tokens
- **Social Features**: Share token launches, follow creators, and discover trending tokens
- **Customizable Tokenomics**: Set supply, distribution, and other parameters

#### 4.7.2 Technical Implementation

- **Token Factory**: Standardized token creation templates
- **Liquidity Management**: Automated pool creation and management
- **Trading Interface**: User-friendly trading experience
- **Substrate Wallet Integration**: Direct connection to Substrate ecosystem
- **Social Graph**: Track and share token activity

#### 4.7.3 Memecoin Launcher Flow

```
+-------------+     +-----------------+     +----------------+     +----------------+
| User        |     | Edgeverse      |     | Token          |     | Liquidity      |
| (Substrate) |     | Chain          |     | Factory        |     | Pools          |
+-------------+     +-----------------+     +----------------+     +----------------+
       |                    |                       |                      |
       | Create Token       |                       |                      |
       | Request            |                       |                      |
       |-------------------->                       |                      |
       |                    |                       |                      |
       |                    | Forward Request       |                      |
       |                    |----------------------->                      |
       |                    |                       |                      |
       |                    |                       | Create Token         |
       |                    |                       |------------------+   |
       |                    |                       |                  |   |
       |                    |                       |<-----------------+   |
       |                    |                       |                      |
       |                    |                       | Create Liquidity     |
       |                    |                       | Pool                 |
       |                    |                       |---------------------->
       |                    |                       |                      |
       |                    |                       |                      | Initialize Pool
       |                    |                       |                      |-------------+
       |                    |                       |                      |             |
       |                    |                       |                      |<------------+
       |                    |                       |                      |
       |                    |                       | Confirm Creation     |
       |                    |                       <----------------------|
       |                    |                       |                      |
       |                    | Confirm Token         |                      |
       |                    <-----------------------|                      |
       |                    |                       |                      |
       | Token Created      |                       |                      |
       <--------------------|                       |                      |
       |                    |                       |                      |
```

**Flow Explanation:**

1. User requests to create a new token using their Substrate wallet
2. Edgeverse forwards the request to the Token Factory
3. Token Factory creates the token with specified parameters
4. Token Factory initiates liquidity pool creation
5. Liquidity pool is initialized with the new token and base asset
6. Creation is confirmed back to the Token Factory
7. Token Factory confirms successful creation to Edgeverse
8. User receives confirmation and can immediately begin trading

## 5. Edgeverse Pallet

The Edgeverse Pallet is a specialized module that manages TSS coordination and other critical functions within the ABC Stack framework.

### 5.1 Key Functions

- **TSS Coordination**: Manage threshold signature operations
- **Vault Signing Requests**: Process and validate signing requests
- **Verifier Slashing**: Implement penalties for malicious verifiers
- **Contract Call Authorization**: Control which contracts can call specific functions
- **Session Key Rotation**: Manage secure key rotation for validators and verifiers

### 5.2 Technical Implementation

- **ABC Stack Integration**: Deep integration with the ABC Stack framework
- **Event System**: Comprehensive event emission for tracking
- **Storage Management**: Efficient state storage for TSS operations
- **Security Controls**: Robust permission and authorization systems

### 5.3 Pallet Architecture

```
+-------------------------------------+
|        Edgeverse Pallet            |
+-------------------------------------+
|                                     |
|  +-------------------------------+  |
|  |   TSS Coordination Module     |  |
|  |   - Key Generation            |  |
|  |   - Signature Aggregation     |  |
|  |   - Threshold Management      |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   Vault Management Module     |  |
|  |   - Signing Requests          |  |
|  |   - Vault Operations          |  |
|  |   - Asset Tracking            |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   Verifier Control Module     |  |
|  |   - Verifier Registration     |  |
|  |   - Slashing Conditions       |  |
|  |   - Reward Distribution       |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   Authorization Module        |  |
|  |   - Contract Whitelisting     |  |
|  |   - Function Permissions      |  |
|  |   - Access Control            |  |
|  +-------------------------------+  |
|                                     |
|  +-------------------------------+  |
|  |   Session Management Module   |  |
|  |   - Key Rotation              |  |
|  |   - Session Validation        |  |
|  |   - Security Controls         |  |
|  +-------------------------------+  |
|                                     |
+-------------------------------------+
```

## 6. Gas Fee Model

Edgeverse Chain implements a Custom Gas Token System that provides maximum flexibility for users.

### 6.1 Custom Gas Token System

- **Multi-Token Support**: Pay fees in EDG or any token with ≥$50K liquidity
- **Auto-Swap Mechanism**: Tokens automatically swapped to EDG during execution
- **Universal Application**: Applies to all operations (swap, bridge, SCO)
- **Verification Layer**: All gas token operations verified by verifier nodes
- **EVM Compatibility**: Seamless fee payment via mapped EVM addresses

### 6.2 Node Licensing Model

Edgeverse implements a comprehensive node licensing model for both verifier nodes and Celestia light nodes:

- **Verifier Node Licenses**: Operators purchase licenses to run verifier nodes that validate cross-chain operations, verify gas token swaps, and secure the network
- **Celestia Light Node Licenses**: Operators can run Celestia light nodes to support data availability and consensus for the sovereign rollup
- **Tiered License Structure**: Multiple tiers available with different stake requirements, hardware specifications, and reward potentials
- **Decentralization Incentives**: License distribution designed to ensure geographical and operational diversity
- **Technical Requirements**: Specific hardware and connectivity requirements to ensure optimal network performance
- **Compliance Framework**: Clear guidelines for node operators to maintain network integrity

### 6.3 Emergency Controls via Unified Governance

Emergency controls are managed through the Edgeware/Edgeverse Unified Governance system:

- **Unified Governance**: Shared governance between Edgeware and Edgeverse chains
- **Pause Mechanism**: Ability to temporarily halt specific operations
- **Multi-Signature Control**: Critical functions require multiple approvals
- **Emergency Response**: Rapid response protocols for security incidents
- **Recovery Procedures**: Predefined processes for various emergency scenarios

## 7. Security Model

### 7.1 TSS Security

The Threshold Signature Scheme (TSS) is a cornerstone of Edgeverse's security model:

- **Distributed Key Generation**: No single entity holds the complete private key
- **Threshold Requirements**: Require t-of-n validators to sign transactions
- **Key Rotation**: Regular key rotation to mitigate compromise risks
- **Slashing Conditions**: Economic penalties for malicious behavior

### 7.2 Verifier Network Security

The verifier network provides an additional layer of security:

- **Byzantine Fault Tolerance**: Operate under BFT assumptions
- **Consensus Requirements**: Require supermajority agreement for critical operations
- **Economic Security**: Verifiers stake EDG tokens as collateral
- **Slashing Mechanism**: Penalties for incorrect or malicious behavior

### 7.3 Audit Trail

All operations in the Edgeverse ecosystem generate a permanent, immutable record:

- **Event Logging**: Comprehensive event emission for all operations
- **Verifier Attestations**: Cryptographic proofs of operation validity
- **Chain Storage**: Permanent storage of critical events on-chain
- **Transparency**: Public accessibility of audit trails

### 7.4 Emergency Controls

In case of critical events, the system includes emergency controls:

- **Pause Mechanism**: Ability to temporarily halt operations
- **Governance Intervention**: Collective decision-making for critical issues
- **Fallback Procedures**: Predefined procedures for various failure scenarios
- **Recovery Mechanisms**: Processes to restore normal operation after incidents

## 8. Conclusion

Edgeverse Chain represents a significant advancement in blockchain interoperability and DeFi capabilities. By leveraging the Abundance ABC Stack's sovereign rollup architecture with its 1 Gigagas per second throughput and the security of TSS vaults, Edgeverse creates a comprehensive ecosystem for cross-chain operations.

The platform's core features—Substrate Adopter, EdgeBridge (with Standard Bridge, Fast Bridge, Yield Routes, and Whitelisted dApps), EdgeSwap, SCO, EdgeName Service, EVM DeFi Access, and Memecoin Launcher—provide a complete solution for users and developers seeking to leverage the benefits of multiple blockchains without the complexity typically associated with cross-chain operations. The high-performance execution layer enables web2-like experiences for DeFi, gaming, and token creation while maintaining the security and decentralization benefits of blockchain technology.

With its focus on security, efficiency, and user experience, Edgeverse Chain is positioned to become a leading platform for the next generation of blockchain applications, particularly those requiring seamless interaction across multiple chains and ecosystems.

The innovative approach of moving locked assets to TSS vaults rather than keeping them idle, combined with the automatic mapping between Substrate and EVM addresses, creates a seamless experience for users while maximizing the utility and efficiency of the platform.
