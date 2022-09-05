---
description: Initialize FCL and add Blocto as a wallet provider
---

# Getting Started

### Installation

Add the dependency below to your module's `build.gradle` file

```groovy
dependencies {
    implementation "com.portto.fcl:$fclVersion"
}
```

### Initialization

To initialize FCL, call `Fcl.init()`.

```kotlin
Fcl.init(
    env = Network.TESTNET,
    appDetail = AppDetail(),
    supportedWallets = walletProviderList
)
```

{% hint style="info" %}
FCL requires some essential information for initialization:

* env: The network on which the app was built. i.e. `Network.TESTNET` or `Network.MAINNET`
* appDetail: The information of the app.
* supportedWallets: A list of **wallet providers** supported by the app.
{% endhint %}

### Wallet Provider

A wallet provider is the instance of a Flow wallet. The following is an example of adding `Blocto` as a wallet provider.

```kotlin
val walletProviderList = listOf(Blocto.getInstance(YOUR_BLOCTO_APP_ID))

Fcl.init(
    env = Network.TESTNET,
    appDetail = AppDetail(),
    supportedWallets = walletProviderList
)
```

{% hint style="info" %}
To obtain a **Blocto App ID**, please refer to the [instructions](../../register-app-id.md).&#x20;

If you initialize FCL with `Network.TESTNET`, FCL utilizes Blocto **testing** App ID; Likewise, if you initialize FCL with `Network.MAINNET`, FCL utilizes Blocto **production** App ID.
{% endhint %}