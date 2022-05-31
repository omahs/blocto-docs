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
    debug = true           // optional (default is false)
)
```

{% hint style="info" %}
`debug`: Specify the cluster. `true` for **mainnet-beta** and `false` for **devnet**. Default is `false`.
{% endhint %}