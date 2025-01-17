# Prerequisite

## Latest Version

* [Portto.Blocto.Core](https://github.com/portto/blocto-unity-sdk/releases/tag/protto.blocto.core.0.2.1)
* [Portto.Blocto.Evm](https://github.com/portto/blocto-unity-sdk/releases/tag/portto.blocto.evm.0.1.0)
* [Portto.Blocto.Solana](https://github.com/portto/blocto-unity-sdk/releases/tag/portto.blocto.solana.0.1.1)
* [Portto.Blocto.Flow](https://github.com/portto/blocto-unity-sdk/releases/tag/protto.blocto.flow.0.2.5)

Blocto Unity SDK supports two flows depending on whether the Blocto app is installed or not.

* **Blocto app installed**\
  ****Based on development environment, you need to download the corresponding Blocto app for testing:
  * [prod](https://apps.apple.com/tw/app/blocto-%E5%8A%A0%E5%AF%86%E8%B2%A8%E5%B9%A3%E9%8C%A2%E5%8C%85-by-portto/id1481181682)
  * [dev](https://appdistribution.firebase.dev/i/50335e7876650bce) (after joining app distribution, you need to wait for releasing next version)
* **Blocto app not installed**\
  SDK would open browser using Web SDK in your dApp to use the Blocto service. In Android, Blocto SDK provider `CloseWebView` method to close web view when user click back button.

```csharp
if(Input.GetKey(KeyCode.Escape))
{
    walletProvider.CloseWebView();
}
```

You can setting `ForcedUseWebView` for use of the Web SDK instead the Blocto app.

```csharp
walletProvider.ForcedUseWebView = true;
```

## iOS Universal Links & Android Deep Link

Blocto Unity SDK uses iOS[ Universal Links](https://developer.apple.com/ios/universal-links/) or Android [Deep Link](https://developer.android.com/training/app-links/deep-linking) to bring back information from Blocto wallet app to yours.\
If you do not set iOS Universal Links or Android Deep Link in Developer Dashboard ([production](https://developers.blocto.app/), [dev](https://developers-dev.blocto.app/)) or any situation that can't open your app correctly.

* iOS Universal Links setting. please add Associated Domains in Xcode project setting and add new path **`/blocto`** to your apple-app-site-association

<figure><img src="../../.gitbook/assets/UniversalLink (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Please add a new path **`/blocto`** to your apple-app-site-association
* Android Deep Links setting, please add **`activity`** and **`intent-filter`** in yours AndroidManifest.xml

```xml
<activity android:exported="true"
          android:launchMode="singleTop"
          android:name="com.blocto.unity.CallbackActivity" 
          android:process="e.unity3d">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="blocto" />
    </intent-filter>
</activity>
```

## Unity Build Setting

In Android, please add `activity`, `intent-filter`, `uses-permission` and `queries` in yours AndroidManifest.xml

```xml
<application
        android:allowBackup="true"
        android:icon="@drawable/app_icon"
        android:label="@string/app_name">
    <activity android:name="com.unity3d.player.UnityPlayerActivity"
              android:launchMode="singleTask"
              android:label="@string/app_name"
              android:configChanges="fontScale|keyboard|keyboardHidden|locale|mnc|mcc|navigation|orientation|screenLayout|screenSize|smallestScreenSize|uiMode|touchscreen">
        <meta-data android:name="unityplayer.UnityActivity" android:value="true"/>
        <meta-data android:name="unityplayer.ForwardNativeEventsToDalvik" android:value="true" />
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.BROWSABLE" />
            <category android:name="android.intent.category.DEFAULT" />
        </intent-filter>
    </activity>
</application>
<uses-permission android:name="android.permission.INTERNET" />
<queries>
    <package android:name="com.portto.blocto" />
    <package android:name="com.portto.blocto.staging" />
    <package android:name="com.portto.blocto.dev" />
</queries>
```
