# TokenShop Smart Contract

A **decentralized token shop** that lets users buy ERC20 tokens (`MyERC20`) by sending ETH. The exchange rate is dynamically calculated using **Chainlink's ETH/USD price feed**.

## Features
- **Dynamic Pricing**: Tokens are priced at **2 USD** (adjustable) using real-time ETH/USD rates from Chainlink.
- **Simple Purchase**: Users send ETH to the contract and receive tokens automatically.
- **Owner Withdrawals**: Only the contract owner can withdraw accumulated ETH.
- **Security**: Reverts on zero-value transactions.

## Contract Details
- **Network**: Sepolia (Chainlink ETH/USD feed: `0x694AA1769357215DE4FAC081bf1f309aDC325306`).
- **Token**: Custom `MyERC20` (must be deployed separately).
- **Dependencies**:
  - OpenZeppelin (`Ownable`).
  - Chainlink (`AggregatorV3Interface`).

## How It Works
1. **User Sends ETH**: The `receive()` function triggers the purchase.
2. **Price Calculation**: ETH is converted to USD value using Chainlink, then to tokens at a fixed rate.
3. **Token Minting**: Tokens are minted to the user’s address.
4. **Owner Withdrawals**: The owner can withdraw ETH via `withdraw()`.

## Setup
1. Deploy `MyERC20.sol` (or replace with an existing ERC20).
2. Deploy `TokenShop.sol` with the `MyERC20` address.
3. Fund the contract with ETH (for Chainlink gas costs).

## Security Notes
- **No Reentrancy Protection**: Consider adding OpenZeppelin’s `ReentrancyGuard`.
- **Price Feed Risks**: Validate Chainlink data (e.g., check for stale prices).
- **Hardcoded Feed**: Update the Chainlink address for other networks.

## License
MIT
