# BitVault Protocol

**Next-Generation Bitcoin-Backed DeFi Infrastructure on Stacks**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Clarity](https://img.shields.io/badge/Language-Clarity-brightgreen.svg)](https://clarity-lang.org/)
[![Stacks](https://img.shields.io/badge/Built%20on-Stacks-blue.svg)](https://stacks.co/)

## 🚀 Overview

BitVault is a revolutionary decentralized finance protocol that enables Bitcoin holders to unlock liquidity through over-collateralized stablecoin minting and automated market making on Stacks Layer 2. The protocol represents a paradigm shift in Bitcoin DeFi, offering institutional-grade infrastructure for Bitcoin-native financial primitives.

### Key Features

- **🔒 Over-Collateralized Vaults**: Secure Bitcoin collateral with 150% minimum collateralization ratio
- **💰 Stablecoin Minting**: Generate USD-pegged stablecoins backed by Bitcoin
- **🌊 Automated Market Making**: Dual-asset liquidity pools for efficient trading
- **📊 Oracle Integration**: Real-time BTC/USD price feeds for accurate valuations
- **⚡ Instant Liquidation**: Automated position management at 130% threshold
- **🛡️ Risk Management**: Comprehensive safety mechanisms and parameter controls

## 🏗️ Architecture

### System Overview

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Bitcoin L1    │    │   Stacks L2     │    │  BitVault DApp  │
│                 │◄──►│                 │◄──►│                 │
│  BTC Holdings   │    │ Smart Contracts │    │  User Interface │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │
                              ▼
                    ┌─────────────────┐
                    │  Core Modules   │
                    │                 │
                    │ • Vault System  │
                    │ • AMM Pool      │
                    │ • Oracle Feed   │
                    │ • Liquidation   │
                    └─────────────────┘
```

### Contract Architecture

The BitVault protocol consists of four core modules:

#### 1. **Collateral Vault System**

- **Purpose**: Manages Bitcoin deposits and stablecoin minting
- **Components**:
  - Vault creation and management
  - Collateral ratio calculations
  - Stablecoin minting/burning
  - Position health monitoring

#### 2. **Automated Market Maker (AMM)**

- **Purpose**: Provides liquidity and trading functionality
- **Components**:
  - Dual-asset liquidity pools (BTC/Stablecoin)
  - LP token mechanics
  - Fee collection system
  - Slippage protection

#### 3. **Oracle Price Feed**

- **Purpose**: Maintains accurate BTC/USD pricing
- **Components**:
  - Price validation mechanisms
  - Owner-controlled updates
  - Price ceiling enforcement
  - Historical price tracking

#### 4. **Risk Management Layer**

- **Purpose**: Ensures protocol safety and stability
- **Components**:
  - Collateralization monitoring
  - Liquidation thresholds
  - Parameter validation
  - Emergency controls

## 📊 Data Flow

### Vault Creation & Stablecoin Minting

```
User BTC Deposit → Vault Creation → Collateral Check → Stablecoin Mint
      ↓                ↓               ↓               ↓
   Transfer BTC    Update Vault    Check 150% Min   Credit Balance
```

### Liquidity Provision

```
BTC + Stablecoin → Pool Deposit → LP Token Calc → Position Update
       ↓              ↓             ↓              ↓
   Asset Transfer  Reserve Update  Token Issue   Provider Record
```

### Price Oracle Update

```
External Price → Validation → State Update → Collateral Recheck
      ↓            ↓            ↓             ↓
   Owner Call   Range Check   Oracle Var   Vault Health
```

## 🔧 Protocol Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| **Minimum Collateral Ratio** | 150% | Required over-collateralization |
| **Liquidation Threshold** | 130% | Position liquidation trigger |
| **Minimum Deposit** | 0.01 BTC | Smallest vault deposit allowed |
| **Pool Fee Rate** | 0.3% | Trading fee for AMM operations |
| **Max Price Ceiling** | $1M USD | Maximum BTC price accepted |
| **Max Mint Amount** | $10K USD | Maximum stablecoin mint per tx |

## 🏗️ Smart Contract Functions

### Public Functions

#### Vault Operations

- `deposit-collateral(btc-amount)` - Deposit Bitcoin as collateral
- `mint-stablecoin(amount)` - Mint stablecoins against collateral
- `burn-stablecoin(amount)` - Burn stablecoins to reduce debt

#### Liquidity Pool Operations

- `add-liquidity(btc-amount, stable-amount)` - Provide dual-asset liquidity
- `remove-liquidity(lp-tokens)` - Withdraw liquidity position

#### Administrative Functions

- `initialize(initial-price)` - Initialize protocol with BTC price
- `update-price(new-price)` - Update BTC/USD oracle price

### Read-Only Functions

- `get-vault-details(owner)` - Retrieve vault information
- `get-collateral-ratio(owner)` - Calculate current collateral ratio
- `get-pool-details()` - View pool reserves and metrics
- `get-lp-details(provider)` - Check liquidity provider position

## 🧪 Development Setup

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) - Smart contract development
- [Node.js](https://nodejs.org/) (v16+) - JavaScript runtime
- [Stacks CLI](https://docs.stacks.co/) - Stacks blockchain tools

### Installation

```bash
# Clone the repository
git clone https://github.com/sarah-osam/bitvault.git
cd bitvault

# Install dependencies
npm install

# Check contract syntax
clarinet check

# Run tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Project Structure

```
bitvault/
├── contracts/
│   └── bitvault.clar          # Main protocol contract
├── tests/
│   └── bitvault.test.ts       # Comprehensive test suite
├── settings/
│   ├── Devnet.toml           # Development network config
│   ├── Testnet.toml          # Testnet configuration
│   └── Mainnet.toml          # Mainnet configuration
├── Clarinet.toml             # Project configuration
├── package.json              # Node.js dependencies
└── README.md                 # This file
```

## 🧪 Testing

The protocol includes comprehensive test coverage:

```bash
# Run all tests
npm test

# Run specific test file
npx vitest bitvault.test.ts

# Generate coverage report
npm run test:report
```

### Test Categories

- **Unit Tests**: Individual function validation
- **Integration Tests**: Multi-function workflow testing
- **Edge Cases**: Boundary condition verification
- **Security Tests**: Attack vector prevention
- **Gas Optimization**: Cost efficiency validation

## 🚀 Deployment

### Testnet Deployment

```bash
# Deploy to Stacks testnet
clarinet deployments apply --network testnet

# Verify deployment
clarinet console --network testnet
```

### Mainnet Deployment

```bash
# Deploy to Stacks mainnet
clarinet deployments apply --network mainnet

# Initialize protocol
stx call-contract-func bitvault initialize [initial-btc-price]
```

## 🛡️ Security Considerations

### Protocol Safety Mechanisms

1. **Over-Collateralization**: 150% minimum ratio prevents undercollateralized positions
2. **Price Validation**: Oracle price bounds prevent manipulation
3. **Access Control**: Owner-only administrative functions
4. **Amount Limits**: Maximum transaction and balance caps
5. **State Validation**: Comprehensive input validation and error handling

### Audit Status

- [ ] Internal security review
- [ ] External audit (planned)
- [ ] Bug bounty program (planned)
- [ ] Formal verification (planned)

## 📈 Economics

### Fee Structure

- **Pool Trading Fee**: 0.3% on all AMM swaps
- **Liquidation Penalty**: 10% of liquidated collateral
- **Protocol Fee**: 0.1% on stablecoin minting

### Tokenomics

- **Stablecoin Supply**: Elastic based on collateral deposits
- **LP Tokens**: Proportional ownership of pool reserves
- **Yield Sources**: Trading fees, liquidation penalties

## 🤝 Contributing

We welcome contributions to BitVault! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow Clarity best practices
- Add comprehensive tests for new features
- Update documentation for API changes
- Ensure all tests pass before submitting

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
