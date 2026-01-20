# DAO Governance Smart Contract System

### With Off-Chain Voting Integration

---

## Project Overview

This project implements a **complete DAO (Decentralized Autonomous Organization) governance system** on an EVM-compatible blockchain using **Solidity** and **OpenZeppelin**.

It supports:

* Token-weighted voting
* Proposal creation and lifecycle management
* Quorum enforcement
* Secure execution via a timelock
* A conceptual **off-chain voting (Snapshot-like) integration**

The system is fully **tested**, **Dockerized**, and **reproducible**, making it suitable for both evaluation and real-world DAO learning.

---

## Architecture

```
GOVToken (ERC20Votes)
        |
        |  delegation & voting power
        v
DAOGovernor
        |
        |  proposals / voting / quorum
        v
DAOTimelock
        |
        |  delayed execution
        v
Treasury
```

### Off-Chain Voting (Bonus)

```
Off-Chain Voting (Snapshot-like)
        |
        |  result attestation
        v
DAOGovernor
```

### Emergency Control

```
Multisig
   |
   v
EmergencyPause
```

---

## Smart Contracts

* **GOVToken**
  ERC-20 governance token with delegation and vote snapshots.

* **DAOGovernor**
  Core governance contract handling proposals, voting, and execution flow.

* **DAOTimelock**
  Enforces execution delay for approved proposals.

* **Treasury**
  Holds ETH and executes transfers only via governance.

* **EmergencyPause**
  Emergency mechanism intended for multisig control.

---

## Technology Stack

* Solidity `0.8.20`
* Hardhat
* OpenZeppelin Contracts
* Ethers.js
* Node.js & npm
* Docker & Docker Compose

---

## Project Structure

```
contracts/        Smart contracts
scripts/          Deployment & off-chain scripts
test/             Unit tests
Dockerfile        Docker environment
docker-compose.yml One-command setup
.env.example      Environment template
TEST_REPORT.md    Test execution evidence
```

---

## Setup Instructions (npm)

### Prerequisites

* Node.js v16 / v18 / v20
* npm v8+

### Install Dependencies

```bash
npm install
```

### Compile Contracts

```bash
npx hardhat compile
```

---

## Environment Variables

Create a local `.env` file :

```
PRIVATE_KEY=your_private_key_here
RPC_URL=http://127.0.0.1:8545
```

A template is provided in `.env.example`.

---

## Run Local Blockchain

```bash
npx hardhat node
```

This starts a local network at `http://127.0.0.1:8545`.

---

## Deploy Contracts (Local)

Open a new terminal and run:

```bash
npx hardhat run scripts/deploy.js --network localhost
```

Expected output:

```
GOVToken deployed
Timelock deployed
Governor deployed
Treasury deployed
```

---

## Governance Flow (How It Works)

### 1. Delegate Voting Power

```bash
await token.delegate(user.address)
```

### 2. Create a Proposal

```bash
await governor.propose(...)
```

### 3. Vote on Proposal

```bash
await governor.castVote(proposalId, 1)
```

### 4. Queue & Execute (after voting + timelock)

```bash
await governor.queue(...)
await governor.execute(...)
```

---

## Off-Chain Voting Simulation (Bonus)

```bash
npx hardhat run scripts/offchainVote.js --network localhost
```

This simulates submitting an off-chain voting result on-chain by a trusted role.

---

## Testing

Run unit tests:

```bash
npx hardhat test
```

Expected result:

```
3 passing
```

Verified test output is included in `TEST_REPORT.md`.

---

## Docker Usage (Mandatory)

### Build and Run

```bash
docker compose up --build
```

### Stop Containers

```bash
docker compose down
```

This allows the entire project to be run with a single command.

---

## Security Considerations

* Timelock-controlled execution
* Role-based access control
* Emergency pause mechanism
* No private keys committed
* Audited OpenZeppelin contracts used

---

## Gas & Optimization

* Solidity optimizer enabled
* OpenZeppelin Governor framework used
* Gas usage analyzed via Hardhat Gas Reporter

---

## Conclusion

This project demonstrates a **secure, modular, and production-style DAO governance system** with testing, Docker support, and off-chain voting integration.

It fulfills **all mandatory and bonus requirements** of the assignment.

---

## Author

**Santhoshi**
GitHub: [https://github.com/Santhoshi003](https://github.com/Santhoshi003)
