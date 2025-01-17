---
description: Use blocto-connector to connect Blocto wallet SDK with web3-react easily
---

# Web3-React Connector

If you are using `web3-react` for your project, we provide a connector module for you to connect Blocto wallet SDK easily.

{% hint style="warning" %}
Note that Blocto SDK for Ethereum-like chains is still in **Beta**. APIs are subject to breaking changes.
{% endhint %}

Install from npm/yarn

```bash
$ yarn add @blocto/blocto-connector
```

Import and initiate Blocto-Connector

```javascript
import { BloctoConnector } from '@blocto/blocto-connector'

const connector = new BloctoConnector({
  chainId: NETWORK_CHAIN_ID,
  rpc: NETWORK_URL
})
```

#### Blocto Connector parameters

| Parameter | Type   | Description                                                                                            | Required |
| --------- | ------ | ------------------------------------------------------------------------------------------------------ | -------- |
| `chainId` | Number | <p>EVM chain ID to connect to</p><p>Reference: <a href="https://chainid.network/">EVM Networks</a></p> | **Yes**  |
| `rpc`     | String | JSON RPC endpoint                                                                                      | **Yes**  |

#### Parameters Example

{% tabs %}
{% tab title="Ethereum Mainnet" %}
```javascript
const connector = new BloctoConnector({
    chainId: 1,
    rpc: 'https://mainnet.infura.io/v3/YOUR_INFURA_ID',
});
```
{% endtab %}

{% tab title="Ethereum Testnet (Rinkeby)" %}
```javascript
const connector = new BloctoConnector({
    chainId: 4,
    rpc: 'https://rinkeby.infura.io/v3/YOUR_INFURA_ID',
});
```
{% endtab %}

{% tab title="BSC Mainnet" %}
```javascript
const connector = new BloctoConnector({
    chainId: 56,
});
```
{% endtab %}

{% tab title="BSC Testnet (Chapel)" %}
```javascript
const connector = new BloctoConnector({
    chainId: 97,
});
```
{% endtab %}
{% endtabs %}

| Network                  | Chain ID |
| ------------------------ | -------- |
| Ethereum Mainnet         | 1        |
| Ethereum Rinkeby Testnet | 4        |
| BSC Mainnet              | 56       |
| BSC Chapel Testnet       | 97       |
| Polygon Mainnet          | 137      |
| Polygon Mumbai Testnet   | 80001    |
| Avalanche Mainnet        | 43114    |
| Avalanche Fuji Testnet   | 43113    |

#### Usage

After connector is ready, now you can activate it using `useWeb3React` hook provided by `web3-react` . Now your code might look like:

```jsx
import React from 'react'
import { Web3ReactProvider } from '@web3-react/core'
import { Web3Provider } from '@ethersproject/providers'
import { useWeb3React } from '@web3-react/core'
import { BloctoConnector } from '@blocto/blocto-connector'

export const connector = new BloctoConnector({
  chainId: NETWORK_CHAIN_ID,
  rpc: NETWORK_URL
})

function getLibrary(provider: any): Web3Provider {
  // this will vary according to whether you use e.g. ethers or web3.js
  const library = new Web3Provider(provider)
  library.pollingInterval = 12000
  return library
}

export const Wallet = () => {
  const { chainId, account, activate, active } = useWeb3React<Web3Provider>()

  const onClick = () => {
    activate(connector)
  }

  return (
    <div>
      <div>ChainId: {chainId}</div>
      <div>Account: {account}</div>
      {active ? (
        <div>✅</div>
      ) : (
        <button type="button" onClick={onClick}>
          Connect
        </button>
      )}
    </div>
  )
}

export const App = () => {
  return (
    <Web3ReactProvider getLibrary={getLibrary}>
      <Wallet />
    </Web3ReactProvider>
  )
}
```

`web3-react` uses [Context](https://reactjs.org/docs/context.html) to efficiently store this data, and inject it wherever you need it in your application. For more information using `web3-react`, please check out

* [Web3-React](https://github.com/NoahZinsmeister/web3-react)
* [Web3-React Documentation](https://github.com/NoahZinsmeister/web3-react/tree/v6/docs)
