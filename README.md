# ABI Encoder Demo

This project demonstrates different uses of `abi.encodePacked` in the context of DeFi (Decentralized Finance) applications. The `ABIEncoderDemo` contract includes multiple practical examples of how to encode data for different common scenarios in DeFi.

## 📋 Contract Description

The `ABIEncoderDemo` contract (`src/ABIEncoderDemo.sol`) contains functions that demonstrate how to use `abi.encodePacked` for:

- **Liquidity pool identifiers**: Create unique identifiers for liquidity pools (similar to Uniswap V3)
- **Trading positions**: Encode trading position data with swap parameters
- **Swap data**: Encode token paths and amounts for DEX exchanges
- **Limit orders**: Encode limit orders with maker, taker, and exchange parameters
- **Yield farming positions**: Create unique identifiers for staking positions
- **Flash loans**: Encode data for flash loans
- **Staking pool configuration**: Encode pool configuration parameters
- **Multi-pool hashes**: Create unique identifiers for users across multiple pools
- **Yield strategies**: Encode complex yield farming strategies
- **Cross-chain bridge data**: Encode information for cross-chain transfers
- **DeFi transaction IDs**: Create unique identifiers for transactions
- **Advanced orders**: Stop loss, take profit, and trailing stop orders

## 🧪 Test Suite

The test file (`test/ABIEncoderDemo.t.sol`) provides comprehensive coverage of the contract with the following test cases:

### Pool Identifier Tests

- ✅ Verifies that the pool identifier is invariant to token order
- ✅ Verifies that different fees produce different IDs

### Trading Position Tests

- ✅ Verifies correct encoding of position data including timestamp

### Swap Data Tests

- ✅ Verifies encoding of paths, amounts, and deadline
- ✅ Verifies revert when arrays have different lengths

### Limit Order Tests

- ✅ Verifies encoding of limit orders and their hash

### Yield Farming Tests

- ✅ Verifies creation of yield position identifiers
- ✅ Verifies encoding of yield strategies with array validation

### Flash Loan Tests

- ✅ Verifies encoding of flash loan data

### Staking Configuration Tests

- ✅ Verifies encoding of pool configuration including timestamp

### Multi-Pool Hash Tests

- ✅ Verifies creation of unique hashes for users across multiple pools

### Cross-Chain Bridge Tests

- ✅ Verifies encoding of data for cross-chain transfers

### Transaction ID Tests

- ✅ Verifies creation of unique identifiers for DeFi transactions

### Advanced Order Tests

- ✅ Verifies encoding of stop loss orders
- ✅ Verifies encoding of take profit orders
- ✅ Verifies encoding of trailing stop orders

## 🚀 Usage

### Prerequisites

This project uses [Foundry](https://book.getfoundry.sh/), a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.

### Installation

```shell
# Install Foundry (if you don't have it yet)
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### Build

```shell
forge build
```

### Run Tests

```shell
# Run all tests
forge test

# Run tests with more detail
forge test -vvv

# Run a specific test
forge test --match-test test_createPoolIdentifier_SameForBothTokenOrders
```

### Format Code

```shell
forge fmt
```

### Gas Snapshots

```shell
forge snapshot
```

## 📚 Foundry Documentation

For more information about Foundry, check the official documentation:
https://book.getfoundry.sh/

## 🔍 Usage Examples

### Create a Pool Identifier

```solidity
address tokenA = 0x...;
address tokenB = 0x...;
uint24 fee = 3000; // 0.3%

bytes32 poolId = demo.createPoolIdentifier(tokenA, tokenB, fee);
```

### Encode a Trading Position

```solidity
(bytes32 positionId, bytes memory encodedData) = demo.encodeTradingPosition(
    user,
    tokenIn,
    tokenOut,
    amountIn,
    minAmountOut
);
```

### Encode Swap Data

```solidity
address[] memory path = [tokenA, tokenB, tokenC];
uint256[] memory amounts = [100, 200, 300];
uint256 deadline = block.timestamp + 1 hours;

bytes memory swapData = demo.encodeSwapData(path, amounts, deadline);
```

## 📝 Important Notes

- **`abi.encodePacked`**: This function concatenates values without additional padding, which can cause collisions if not used carefully. This contract demonstrates best practices to avoid these issues.
- **Token ordering**: The contract automatically sorts tokens to ensure consistency in pool identifiers.
- **Discriminators**: Many functions include string discriminators (such as "LIMIT_ORDER_V1") to avoid collisions between different data types.
- **Timestamps**: Some functions use `block.timestamp`, so tests use `vm.warp()` to set deterministic values.
