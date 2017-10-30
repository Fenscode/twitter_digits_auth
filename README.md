## What is the use of “Twitter digits authentication”?

Email and password signup is a technology that has not been innovated on in decades.
Signup forms are cumbersome and repetitive. When users forget their credentials and fail
to sign in, you can lose customers.
So, that's why here twitter digits comes in picture. It use user's phone number to
authentication user and send One time password (OTP) code on that number for
authenticate genuine user for app. Twitter take phone number for authenticate user, fact
behind that, phone number is easly we remember.
Twitter digits provided their service for both Android and iOS.

## How to integrate and use Twitter digits in your App ?

###### 1. Add the Kit to Your app's build.gradle

```java
buildscript {
repositories {
maven { url 'https://maven.fabric.io/public' }
}

dependencies {
// The Fabric Gradle plugin uses an open ended version to react
// quickly to Android tooling updates
classpath 'io.fabric.tools:gradle:1.+'
}
}
```
###### Add following dependency to Your app's common build.gradle

```java
apply plugin: 'io.fabric'
repositories {
maven { url 'https://maven.fabric.io/public' }
}

dependencies {
...........
compile('com.digits.sdk.android:digits:2.0.1@aar') {
transitive = true;
}
}

```
###### Add Your API Key at “AndroidManifest.xml”
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
<application android:allowBackup="true" android:icon="@mipmap/ic_launcher"
android:label="@string/app_name" android:theme="@style/AppTheme" >
<activity android:name=".MainActivity" android:label="@string/app_name" >
<intent-filter>
<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>
<uses-permission android:name="android.permission.INTERNET" />
<meta-data android:name="io.fabric.ApiKey"
android:value="****a6e7c4913e66601a*********************" />
</application>
</manifest>
```

###### Tap on “Create Application” button, and create you twitter digits application. When you
made application, than your API key generated automatically.

###### Import packages in yor MainActivity.java
```java
import com.digits.sdk.android.Digits;
import com.twitter.sdk.android.core.TwitterAuthConfig;
import com.twitter.sdk.android.core.TwitterCore;import io.fabric.sdk.android.Fabric;
## Intialize your Twitter API KEY and Twitter Secret key on TwitterAuthConfig constuctor.
Both the key are available on Application dashboard.
## And after that build your your app with Fabric.
public class MainActivity extends ActionBarActivity
{
@Override protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
TwitterAuthConfig authConfig = new TwitterAuthConfig(TWITTER_KEY,TWITTER_SECRET);
Fabric.with(this, new TwitterCore(authConfig), new Digits.Builder().build());
setContentView(R.layout.activity_main);
}
........... .......... ..............
}
```
###### Rebuild your project:

Build your project and see everything going to work!

###### You can see, some demo Example on following link:
(https://fabric.io/kits/android/digits/features)

## Integrate your theme in your digits App:
###### - Customize Digits to use your own fonts and colors.
###### - Create a custom theme that can be assigned to the Digits authentication screens.

###### 1. Add your theme elements in themes.xml
```xml
<resources>
<style name="CustomDigitsTheme" parent="android:Theme.Light">
<item name="android:textColorPrimary">@android:color/black</item>
<item name="android:textColorSecondary">@android:color/darker_gray</item>
<item name="android:windowBackground">@android:color/darker_gray</item>
<item name="android:textColorLink">#ff398622</item>
<item name="dgts__accentColor">#ffacee</item>
</style>
</resource>
```

###### 2. Set the Digits theme in Mainactivity.java
To use this code you’ll need to already have a DigitsAuthButton in your app. Go through
the “Sign In with Phone Number” tutorial if you need one.

Adding a theme to DigitsAuthButton will affect the entire sign in flow. You can change
fonts, colors, and add your app’s logo.

###### Build your custom theme with Digits.Builder class.

## Example:
```java
Digits.Builder digitsBuilder = new Digits.Builder().withTheme(R.style.CustomDigitsTheme);
Fabric.with(this, new TwitterCore(authConfig), digitsBuilder.build());
```
Try it out!

Run the app. You should see that after tapping on the "Use my phone number" button,
your theme is applied to the Digits authentication screens.

## Screenshot:

###### Home:
<img src="https://github.com/Fenscode/twitter_digits_auth/blob/master/Screenshot/Screenshot_20161003-143929.png" width="180" height="300" />

###### Phone number authentication:
<img src="https://github.com/Fenscode/twitter_digits_auth/blob/master/Screenshot/Screenshot_20161003-143938.png" width="180" height="300" />

> ## Digits was shutdown on September 30, 2017. You can still migrate your users to Firebase Auth using the following guide.
> (https://docs.fabric.io/android/digits/android-migration.html)
