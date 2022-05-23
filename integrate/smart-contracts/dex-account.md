---
description: >-
  The DexAccount defines the logic for managing inside of the dex pool.
---

# DexAccount

Smart contract responsible for managing user transactions (withdraw/deposit tokens, withdraw/deposit liquidity, add pair, exchange) inside of the dex pool. 

Derives following classes and interfaces: *DexContractBase, IDexAccount, IAcceptTokensTransferCallback, IUpgradableByRequest, IResetGas*

## Getters

### getRoot

Gets root address of the specific dex root.

```
function getRoot() override external view responsible returns (address)
```
**Return values:**

| Type    | Description                           |
|---------|---------------------------------------|
| address | Address of the account's root address |

### getOwner

Gets the account owner.

```
function getOwner() override external view responsible returns (address) 
```

**Return values:**

| Type    | Description                   |
|---------|-------------------------------|
| address | Address of the account’s owner|

### getVersion

Gets the current version of the account.

```
function getVersion() override external view responsible returns (uint32)
```

**Return values**

| Type    | Description     |
|---------|-----------------|
| uint32  | Current version |

### getVault

Gets the vault of the account.

```
function getVault() override external view responsible returns (address)
```

**Return values:**

| Type    | Description           |
|---------|-----------------------|
| address | Address of the vault  |

### getWalletData 

Use token_root to check whether the specified token exists in wallets list, if it does returns wallet address and it’s balance, if not, returns 0 for address and balance respectively.

```
function getWalletData(address token_root) override external view responsible returns (address wallet, uint128 balance)
```

**Parameters:**

| Name       | Type    | Description        |
|------------|---------|--------------------|
| token_root | address | token root address |

| Name    | Type    | Description                             |
|---------|---------|-----------------------------------------|
| wallet  | address | Wallet address for the specified token  |
| balance | uint128 | Token balance in the wallet             |


### getWallets

```
function getWallets() external view returns (mapping(address => address))
```

Gets list of all the token wallets for this account.

**Return value:**

| Type    | Description                                                 |
|---------|-------------------------------------------------------------|
| address | List of all token wallets addresses for the certain account |

### getBalances

```
function getBalances() external view returns (mapping(address => uint128))
```

Gets list of all the token balances for this account

**Return value:**

| Type    | Description                                                                     |
|---------|---------------------------------------------------------------------------------|
| uint128 | List of all token balances from different token wallets for the certain account |
