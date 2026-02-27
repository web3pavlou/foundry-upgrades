# Foundry Upgrades 

---

## About

This repository is based on the official educational repo:

👉 foundry-upgrades-cu

Originally created by **@PatrickAlphaC** and Cyfrin.

This version includes small adjustments to align with the latest OpenZeppelin Contracts (v5):

* In `UpgradeBox.s.sol`, replaced deprecated `upgradeTo` with:

  ```solidity
  proxy.upgradeToAndCall(address(newBox), "");
  ```

* In `DeployBox.s.sol`, added initializer calldata during proxy deployment:

  ```solidity
  bytes memory data = abi.encodeCall(BoxV1.initialize, ());
  ```

These changes ensure compatibility with modern UUPS upgrade patterns.

This repository remains purely educational.

---


## Getting Started

* Deploying an implementation contract (`BoxV1`)
* Deploying an `ERC1967Proxy`
* Initializing via constructor delegatecall
* Upgrading to `BoxV2`
* Testing upgrade behavior with Foundry


---

## Install

Clone the repository:

```bash
git clone https://github.com/web3pavlou/foundry-upgrades
cd foundry-upgrades
```

Install dependencies:

```bash
forge install
```

Build the project:

```bash
forge build
```

---

## Testing

Run all tests:

```bash
forge test
```

Run a specific test:

```bash
forge test --mt testUpgrades -vvvv
```

Tests cover:

* Proxy starts as `BoxV1`
* Upgrade to `BoxV2`
* State persistence across upgrade
* New functionality after upgrade

---

## Deployment

```bash
forge script script/DeployBox.s.sol --broadcast
```

Upgrade proxy to new implementation:

```bash
forge script script/UpgradeBox.s.sol --broadcast
```

Make sure your `.env` or `foundry.toml` is configured with RPC URL and private key(only for testing purposes).

---

## License

MIT License.
