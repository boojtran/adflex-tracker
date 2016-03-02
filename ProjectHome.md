# Before you Begin #

---

Before implementing the SDK, make sure you have the following:

[AdFlexTracker for Android V1](http://sdk.adflex.vn/dev/libAdFlexTracker1.2.jar) (with libAdFlexTracker1.2.jar included in your project's /libs directory and build path)

# Getting Started #

---

## There are two steps to getting started with the AdFlexTracker Library: ##
1. <u>Update AndroidManifest.xml</u>

Update your AndroidManifest.xml file by adding the following permissions:

```

<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

Add a new BroadcastReceiver

```

<receiver android:name="vn.adflex.tracking.android.InstallationReceiver"  android:exported="true">
<intent-filter>
<action android:name="com.android.vending.INSTALL_REFERRER" />


Unknown end tag for &lt;/intent-filter&gt;





Unknown end tag for &lt;/receiver&gt;


```

Note: An Android app cannot have multiple receivers which have the same intent-filtered action. If you want have more than one INSTALL\_REFFERER receiver, you must make the proxy receiver like this

```

<receiver android:name="com.example.app.TrackingReceiver" android:exported="true">
<intent-filter>
<action android:name="com.android.vending.INSTALL_REFERRER" />


Unknown end tag for &lt;/intent-filter&gt;




Unknown end tag for &lt;/receiver&gt;


```

In TrackingReceiver.java (Only for Google Play)
```


public class TrackingReceiver extends BroadcastReceiver {
@Override
public void onReceive(Context context, Intent intent) {

// call AdFlex tracker
vn.adflex.tracking.android.InstallationReceiver adf= new vn.adflex.tracking.android.InstallationReceiver();
adf.onReceive(context, intent);

// call AdMob tracker
com.google.ads.InstallReceiver ir = new com.google.ads.InstallReceiver();
ir.onReceive(context, intent);

// call Analytics tracker
com.google.android.apps.analytics.AnalyticsReceiver ar = new com.google.android.apps.analytics.AnalyticsReceiver();
ar.onReceive(context, intent);
}
}
```

2. <u>Adding AdFlexTracker methods</u>

Add the track method to the onStart() method of your Launcher Activity as in the following example:

```

package vn.adflex.tracking.demo;
import android.app.Activity;
import android.os.Bundle;
import vn.adflex.tracking.android.AdFlexTracker;


public class MainActivity extends Activity {

@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
}

@Override
protected void onStart() {
super.onStart();
// Add this method, only for Dedicated GooglePlay account, does not require with apk or general GooglePlay account campaigns.
AdFlexTracker.getInstance(this).setApId("provided by AdFlex");
AdFlexTracker.getInstance(this).track(); // Add this method.
}

}
```
