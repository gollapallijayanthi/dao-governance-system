#  DAO Governance Smart Contract System

### With Conceptual Off-Chain Voting Integration

---

##  Project Overview

This project implements a **complete DAO (Decentralized Autonomous Organization) governance system** on an EVM-compatible blockchain using **Solidity**, **Hardhat**, and **OpenZeppelin Contracts**.

The system demonstrates how decentralized governance works through:

- Token-weighted voting
- Proposal creation and lifecycle management
- Quorum enforcement
- Secure execution using a timelock
- Conceptual **off-chain voting (Snapshot-like) integration**

The project is fully **tested**, **Dockerized**, and **reproducible**, making it suitable for evaluation, learning, and portfolio demonstration of real-world DAO governance architecture.

---

##  Architecture

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

---

###  Off-Chain Voting (Conceptual)

```

Off-Chain Voting (Snapshot-like)
|
|  result attestation
v
DAOGovernor

```

This demonstrates how off-chain voting systems can feed verified results back on-chain.

---

### 🚨 Emergency Control (Conceptual)

```

Multisig Wallet
|
v
EmergencyPause

```

An emergency pause mechanism is included to demonstrate DAO safety design patterns.

---

##  Smart Contracts

### **GOVToken**
- ERC-20 governance token
- Supports delegation and vote snapshotting
- Built using `ERC20Votes` and `ERC20Permit`

---

### **DAOGovernor**
- Core governance contract
- Handles proposal creation, voting, quorum, and execution
- Built using OpenZeppelin Governor framework

---

### **DAOTimelock**
- Enforces mandatory execution delay
- Prevents immediate execution of proposals
- Owns and executes approved governance actions

---

### **Treasury**
- Holds ETH
- Allows transfers only through successful governance proposals

---

### **EmergencyPause**
- Conceptual emergency mechanism
- Intended for multisig-controlled governance safety

---

##  Technology Stack

- **Solidity** `0.8.20`
- **Hardhat 3**
- **OpenZeppelin Contracts**
- **Ethers.js**
- **Node.js 22 LTS**
- **Docker & Docker Compose**

---

##  Project Structure

```

contracts/           Smart contracts
scripts/             Deployment & simulation scripts
test/                Unit tests
artifacts/            Hardhat build output (git-ignored)
cache/                Hardhat cache (git-ignored)
Dockerfile            Docker environment
docker-compose.yml    One-command execution
hardhat.config.js     Hardhat configuration
TEST_REPORT.md        Verified test results
README.md             Documentation

````

---

##  Setup Instructions (Local)

### Prerequisites

- Node.js **22 LTS**
- npm v10+

---

### Install Dependencies

```bash
npm install
````

---

### Compile Contracts

```bash
npx hardhat compile
```

---

##  Environment Variables

Create a `.env` file:

```
PRIVATE_KEY=your_private_key_here
RPC_URL=http://127.0.0.1:8545
```

A template is provided in `.env.example`.

---

##  Run Local Blockchain

```bash
npx hardhat node
```

Local network runs at:

```
http://127.0.0.1:8545
```

---

##  Deploy Contracts (Local)

In a new terminal:

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

##  Governance Flow

### 1️ Delegate Voting Power

```js
await token.delegate(user.address);
```

---

### 2️ Create Proposal

```js
await governor.propose(...);
```

---

### 3️ Vote on Proposal

```js
await governor.castVote(proposalId, 1);
```

Vote options:

* `0` → Against
* `1` → For
* `2` → Abstain

---

### 4️ Queue & Execute

```js
await governor.queue(...);
await governor.execute(...);
```

Execution is only possible after the timelock delay.

---

## Off-Chain Voting Simulation (Bonus)

```bash
npx hardhat run scripts/offchainVote.js --network localhost
```

This script demonstrates how off-chain voting results could be submitted on-chain by a trusted role, similar to Snapshot-based governance models.

---

##  Testing

Run unit tests:

```bash
npx hardhat test
```

Expected output:

```
3 passing
```

Verified results are included in:

```
TEST_REPORT.md
```

---

##  Docker Usage

### Build & Run

```bash
docker compose up --build
```

### Stop Containers

```bash
docker compose down
```

Docker ensures:

* identical environments
* zero local dependency issues
* CI/CD-ready execution

---

##  Security Considerations

* Timelock-controlled execution
* Role-based access control
* Delegated voting power only
* Emergency pause mechanism (conceptual)
* No private keys committed
* Audited OpenZeppelin contracts used

---

##  Gas & Optimization

* Solidity optimizer enabled
* Optimizer runs: `50`
* OpenZeppelin Governor framework for efficiency
* Gas statistics generated during test execution

---

##  Conclusion

This project demonstrates a **modular, secure, and production-style DAO governance system**, featuring:

* Token-weighted voting
* Proposal lifecycle management
* Quorum enforcement
* Timelock-secured execution
* Conceptual off-chain voting integration
* Full unit testing
* Dockerized reproducibility

It reflects real-world DAO governance design patterns and fulfills all mandatory requirements of the assignment.

---

