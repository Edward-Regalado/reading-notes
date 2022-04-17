# Google AdMob

- is a mobile advertising platform that you can use to generate revenuce form your application.

## Key capabilities

### Earn more from in-app ads

- show adds from millions of Google advertisers in real time, or use AdMob's medication to earn form over 40 perminum networks through the admob platform to simplify your add operations and improve competition.

### Improve user experience

- native and video ads create a positive user experience as you monetize by matching the look and feel of your app.
- choose different ad templates, customize, and experiment with different layouts without having to republish your application.

### Scale fast

- monetize users quickly by showing ads to users in more than 200 markets
- Admob house ads is a free tool that enables you to cross-promote your apps to your userbase, across your family of apps.

### Access monetization reports

- produces its own monetization reports that you can use to make smarter decisions about product strategy.

## How does it work?

- AdMob helps you monetize your mobile app through in-app advertising.
- ads can be displayed in a number of formates and are seamlessly added to platform native UI components.
- create an AdMob account and activate one or more ad unit IDs- unique identifier for the places in your app where ads are displayed.
- uses the Google Mobile Ads SDK which helps app devs gain insights about their users and maximize ad revenue.

### Configure your app

1. in your app level `build.gradle` file: 

```
buildscript {
    repositories {
        google()
        mavenCentral()
    }
}

allprojects {
    repositories {
        google()
        mavenCentral()
    }
}
```

2. Add the dependencies to your modules app-level Gradle file: 

```
dependencies {
  implementation 'com.google.android.gms:play-services-ads:20.6.0'
}

```

3. Add your AdMob app ID (identified in the AdMob UI) to your app's AndroidManifest.xml file. Add a `<meta-data>` tag with `android:name="com.google.android.gms.ads.APPLICATION_ID"`

```
<manifest>
    <application>
        <!-- Sample AdMob app ID: ca-app-pub-3940256099942544~3347511713 -->
        <meta-data
            android:name="com.google.android.gms.ads.APPLICATION_ID"
            android:value="ca-app-pub-xxxxxxxxxxxxxxxx~yyyyyyyyyy"/>
    </application>
</manifest>
```

### Initialize the Google Mobile Ads SDK

- calling the `MobileAds.initialize()` will initialize the SDK and calls back a completion listener once this is complete.
- this needs to be done only once.
- ads may be preloaded by the SDK or mediation parnter SDKs upon calling the initializer.

```
import com.google.android.gms.ads.MobileAds;
import com.google.android.gms.ads.initialization.InitializationStatus;
import com.google.android.gms.ads.initialization.OnInitializationCompleteListener;

public class MainActivity extends AppCompatActivity {
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MobileAds.initialize(this, new OnInitializationCompleteListener() {
            @Override
            public void onInitializationComplete(InitializationStatus initializationStatus) {
            }
        });
    }
}
```

### Select an ad format

- AdMob offers a number of different ad formats.
  - Banner - rectangular ads that appear at the top or bottomm of device
  - Interstitial - full-screen ads that cover the interface of an app until closed by the user.
  - Native - customizable ads that match the look and feel of your app.
  - Rewarded - ads that reward users for watching short videos and interacting with playable ads and surveys.


### Sources

[Google AdMob](https://developers.google.com/admob)  
[Quick Start Guide](https://developers.google.com/admob/android/quick-start)