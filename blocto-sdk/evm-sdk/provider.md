---
description: A thin JSON-RPC wrapper for interacting with chains and Blocto wallet.
---

# Provider

Blocto SDK comes with an [EIP-1193](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1193.md) compatible provider, you can use it to interact with Ethereum-like chains.

{% hint style="warning" %}
Note that Blocto SDK for Ethereum-like chains is still in **Beta**.  
APIs are subject to breaking changes.
{% endhint %}

### Installation

Install from npm/yarn

```bash
$ yarn add web3
$ yarn add @blocto/sdk
```

... or via CDN

```javascript
<script src="https://unpkg.com/@blocto/sdk@0.2.0/dist/blocto-sdk.umd.js" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
```

### **Usage**

Initiate the Blocto provider 

```javascript
import Web3 from 'web3'
import BloctoSDK from '@blocto/sdk'

const bloctoSDK = new BloctoSDK({
    ethereum: {
        // (required) chainId to be used
        chainId: '0x1', 
        // (required for Ethereum) JSON RPC endpoint
        rpc: 'https://mainnet.infura.io/v3/YOUR_INFURA_ID',
    },
    
    // (optional) Blocto app ID
    appId: 'YOUR_BLOCTO_APP_ID',
});
```

#### Blocto Provider parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>ethereum.chainId</code>
      </td>
      <td style="text-align:left">String (hex)</td>
      <td style="text-align:left">
        <p>EVM chain ID to connect to</p>
        <p>Reference: <a href="https://chainid.network/">EVM Networks</a>
        </p>
      </td>
      <td style="text-align:left"><b>Yes</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ethereum.rpc</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">JSON RPC endpoint</td>
      <td style="text-align:left"><b>Yes </b>(only for Ethereum)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>appId</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Blocto dApp ID</td>
      <td style="text-align:left"><b>No</b>
      </td>
    </tr>
  </tbody>
</table>

#### Examples

{% tabs %}
{% tab title="Ethereum Mainnet" %}
```javascript
const bloctoSDK = new BloctoSDK({
    ethereum: {
        chainId: '0x1', // 1
        rpc: 'https://mainnet.infura.io/v3/YOUR_INFURA_ID',
    },
    appId: 'YOUR_BLOCTO_APP_ID',
});
```
{% endtab %}

{% tab title="Ethereum Testnet \(Rinkeby\)" %}
```javascript
const bloctoSDK = new BloctoSDK({
    ethereum: {
        chainId: '0x4', // 4
        rpc: 'https://rinkeby.infura.io/v3/YOUR_INFURA_ID',
    },
    appId: 'YOUR_BLOCTO_APP_ID',
});
```
{% endtab %}

{% tab title="BSC Mainnet" %}
```javascript
const bloctoSDK = new BloctoSDK({
    ethereum: {
        chainId: '0x38', // 56
    },
    appId: 'YOUR_BLOCTO_APP_ID',
});
```
{% endtab %}

{% tab title="BSC Testnet \(Chapel\)" %}
```javascript
const bloctoSDK = new BloctoSDK({
    ethereum: {
        chainId: '0x61', // 97
    },
    appId: 'YOUR_BLOCTO_APP_ID',
});
```
{% endtab %}
{% endtabs %}

| Network | Chain ID |
| :--- | :--- |
| Ethereum Mainnet | 1 |
| Ethereum Rinkeby Testnet | 4 |
| BSC Mainnet | 56 |
| BSC Chapel Testnet | 97 |
| Polygon Mainnet | 137 |
| Polygon Mumbai Testnet | 80001 |
| Avalanche Mainnet | 43114 |
| Avalanche Fuji Testnet | 43113 |

**Connect to Blocto wallet**  
Once the connection request is fired, there would be a prompt modal to guide user to register/login to Blocto wallet

```javascript
// EIP-1193 way (recommended)
const accounts = bloctoSDK.ethereum.request({ method: 'eth_requestAccounts' })

// Alternative: EIP-1102 way
// CAVEATS! it's deprecated and may be removed from future version
const accounts = await bloctoSDK.ethereum.enable()
```

After connected with Blocto wallet, you can start to send JSON-RPC request with blocto provider

```javascript
// sign a message
bloctoSDK.ethereum.request({
  method: 'eth_sign', 
  params: ["0xyourethaddress", "0x48656c6c6f20776f726c64"
] })
```


