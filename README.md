# Foundry Smart Contract Lottery

A decentralized raffle contract built with Foundry, integrating Chainlink VRF for randomness and Chainlink Automation for upkeep.

## Getting Started

### Requirements

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [foundry](https://getfoundry.sh/)

Verify installation:

```
git --version
forge --version
```

### Quick Setup

```
git clone <your-repo-url>
cd SmartContractLottery/
forge build
```

## Installation

This project uses these dependencies:

- Foundry Standard Library (`forge-std`)
- Chainlink Contracts (`chainlink-brownie-contracts`)
- OpenZeppelin Contracts (`openzeppelin-contracts`)
- Solmate (`solmate`)
- Foundry DevOps (`foundry-devops`)

Install all at once:

```
make install
```

Or install individually:

```
forge install cyfrin/foundry-devops
forge install smartcontractkit/chainlink-brownie-contracts
forge install foundry-rs/forge-std
forge install transmissions11/solmate
forge install openzeppelin-labs/openzeppelin-contracts
```

## Usage

### Local Development

Start a local Anvil node:

```
make anvil
```

In another terminal, deploy locally:

```
make deploy
```

### Testing

Run all tests:

```
forge test
```

Run with gas reporting:

```
forge snapshot
```

Check test coverage:

```
forge coverage
```

### Deployment to Testnet

1. Copy `.env.example` to `.env` and fill in your values:

```
cp .env.example .env
```

Then edit `.env`:

```
SEPOLIA_RPC_URL=<your-rpc-url>
PRIVATE_KEY=<your-private-key>
ETHERSCAN_API_KEY=<your-etherscan-api-key>
```

WARNING: Use a test wallet with no real funds.

2. Get testnet ETH from [faucets.chain.link](https://faucets.chain.link/)

3. Deploy:

```
make deploy ARGS="--network sepolia"
```

This automatically creates a Chainlink VRF subscription and adds your contract as a consumer.

### Scripts

Create a VRF Subscription:

```
make createSubscription ARGS="--network sepolia"
```

Add your contract as a consumer:

```
make addConsumer ARGS="--network sepolia"
```

Enter the raffle using cast:

```
cast send <RAFFLE_ADDRESS> "enterRaffle()" --value 0.1ether --private-key <PRIVATE_KEY> --rpc-url $SEPOLIA_RPC_URL
```

### Code Formatting

```
forge fmt
```

## Project Structure

```
src/
  Raffle.sol          Main lottery contract
script/
  DeployRaffle.s.sol  Deployment script
  Interactions.s.sol  Interaction scripts
test/
  unit/               Unit tests
  integration/        Integration tests
  mocks/              Mock contracts
```

## Key Features

- Chainlink VRF V2.5 for secure randomness (uses `uint256` subId)
- Chainlink Automation for automated winner selection
- Entrance fee requirement for participation
- Automated interval-based draws
- Winner selection and prize distribution

## Network Setup

Update subscription details in `scripts/HelperConfig.s.sol` if you already have a Chainlink VRF subscription.

## Resources

- [Foundry Docs](https://book.getfoundry.sh/)
- [Chainlink VRF Docs](https://docs.chain.link/vrf)
- [Chainlink Automation Docs](https://docs.chain.link/chainlink-automation)
