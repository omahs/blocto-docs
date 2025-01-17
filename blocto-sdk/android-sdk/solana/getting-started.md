# Getting Started

### Installation

Add the dependency below to your module's `build.gradle` file

```groovy
dependencies {
    implementation "com.portto.sdk:solana:$bloctoSdkVersion"
}
```

### Usage

Initialize Blocto SDK

```kotlin
BloctoSDK.init(
    appId = "YOUR_APP_ID", // required
    env = BloctoEnv.PROD   // optional (default is BloctoEnv.PROD)
)
```

{% hint style="info" %}
`env`: Specify the cluster. `BloctoEnv.PROD` for **mainnet-beta** and `BloctoEnv.DEV` for **devnet**. Default is `BloctoEnv.PROD`.
{% endhint %}
