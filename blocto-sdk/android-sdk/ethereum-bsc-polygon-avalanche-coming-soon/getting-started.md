# Getting Started

### Installation

Add the dependency below to your module's `build.gradle` file

```
dependencies {
    implementation "com.portto.sdk:evm:$bloctoSdkVersion"
}
```

### Usage

Initialize Blocto SDK

```
BloctoSDK.init(
    appId = "YOUR_APP_ID", // required
    debug = true           // optional (default is false)
)
```

{% hint style="info" %}
`debug`: Specify the cluster. `true` for **mainnet** and `false` for **testnet**. Default is `false`.
{% endhint %}