# Alan SDK for Android

[Alan Platform](https://alan.app/) • [Alan Studio](https://studio.alan.app/register) • [Docs](https://alan.app/docs/intro.html) • [FAQ](https://alan.app/docs/additional/faq.html) •
[Blog](https://alan.app/blog/) • [Twitter](https://twitter.com/alanvoiceai)

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/alan-ai/alan-sdk-android)](https://github.com/alan-ai/alan-sdk-android/releases)

Create a voice script for your application in [Alan Studio](https://studio.alan.app/register) and then add it to your app.

### SDK installation
Config **module-level** build.gradle file.

### Option 1. Add it as a Maven dependency
```java
def AlanMavenRepo = "https://mymavenrepo.com/repo/fSCXIHAoBMWBdlZGqq6n/"

repositories {
	...
	//Add the following line to the repositories section
    maven { url AlanMavenRepo }
}

...

dependencies {
	...
	//Adding the Alan SDK dependency
    implementation "app.alan:sdk:3.0.7"
}
```

### Option 2. Download aar package and include it manually

Download sdk from releases section [here](https://github.com/alan-ai/alan-android-sdk/releases/download/v3.0.7/AlanSDK_3.0.7.aar)
Put in your <project>/app/libs folder (create one if needed) then modify your build.gradle file

```java
repositories {
		...
		//Add the following line to the repositories section
	    flatDir {
	        dirs 'libs'
	    }
}

dependencies {
	...
	//Alan SDK dependency
 	implementation (name: 'AlanSdk-3.0.7', ext: 'aar')
}
```

## Add the Alan Button to your layout

__activity_main.xml:__

```xml
 <com.alan.alansdk.button.AlanButton
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       android:id="@+id/alanBtn"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"/>
```

## Connect to your Project in Alan Studio

__MainActivity.java:__

```java

private AlanButton alanButton;

protected void onCreate(Bundle savedInstanceState) {
	...
	alanButton = findViewById(R.id.alanBtn);
	alanButton.initSDK("<YOUR_PROJECT_ID_HERE>");
}
```

## Init methods overloads
Most of the time you will need only last overload. 
authJson is used when you need to pass additional params to the script init. It should be a json parseable string

```java
public boolean initSDK(String server, String projectId, String dialogId, String authJson)

public boolean initSDK(String server, String projectId, String dialogId)

public boolean initSDK(String projectId, String dialogId)

public boolean initSDK(String projectId)

```
*Default server is Alan.SERVER Constant.*
*Here projectId == Alan Studio key*

## Handling Alan callbacks

*Handling all possible callbacks*

```java
class YourCallback implements AlanCallback {

@Override
/**
* Alan sdk server connection state changed
**/
public void onConnectStateChanged(@NonNull ConnectionState connectState) {}

@Override
/**
* Alan voice state changed
**/
public void onDialogStateChanged(@NonNull DialogState dialogState) {}

@Override
/**
* Alan recognized an intent
**/
public void onRecognizedEvent(EventRecognised eventRecognised) {}

@Override
/**
* Alan recognized speech. It is essentially speech2text callback
**/
public void onTextEvent(EventText eventText) {}

@Override
/**
* Some other event coming.
* Most of the time it would be your own script-defined events
**/
public void onUnknownEvent(String event, String payload) {}

@Override
/**
* Some error happens
**/
public void onError(String error) {}

@Override
/**
* Callback from the script method calling via sdk.call(method, params)
**/  
public void onMethodCallResponse(String method, String body, String errors) {}

}
```

*For handling only particular callback one can extends **BasicSdkListener***

```java
class YourSimpleCallback extends BasicSdkListener {

//Override smth if needed

}
```

## Logging

One can set extended logging with static method of the Alan object:

`Alan.enableLogging(true);`

## Sample: 
See our example of Alan Integration [here](https://github.com/alan-ai/alan-sdk-android/tree/master/examples/AlanSampleApp)

### Other platforms:
* [Native iOS](https://github.com/alan-ai/alan-sdk-ios)
* [Web](https://github.com/alan-ai/alan-sdk-web)
* [Cordova](https://github.com/alan-ai/alan-sdk-cordova)
* [ReactNative](https://github.com/alan-ai/alan-sdk-reactnative)
* [Flutter](https://pub.dev/packages/alan_voice)

## Have questions?
If you have any questions or if something is missing in the documentation, please [contact us](mailto:support@alan.app), or tweet us [@alanvoiceai](https://twitter.com/alanvoiceai). We love hearing from you!).
