# Allowing Other Apps to Start Your Activity

- when an application can perform an action that might be useful from another app, your app should be prepared to respond to action requests by specifying the appropriate intent filter in your activity.
- To allow other apps to start your activity, you need to add an `<intent-filter></intent-filter>` element i nyour manifest file for the corresponding `<activity>` element.
- the OS identifies your intent filters and adds the information to an internal catalog of intents supported by all installed apps.
- when an app calls `startActivity()` or `startActivityForResult()`, with an implicit intent, the system finds which activity can repsond.

## Add an Intent Filter

- be specific as possible in terms of the type of action and data the activity accepts.

### Action

- A string naming the action to perform. Usually on of the platform-defined values such as `ACTION_SEND` or `ACTION_VIEW`.
- Specify this in your intent filter with the `<action>` element. Value that you specify in this element must be the full string name for the action, instead of the API constant.

### Data

- A description of the data associated with the intent.
- specify this in your intent filter with the `<data>` element. Using one or more attributes in this element, you can specify just the MIME type, just a URI prefix, URI schema or a combination of these and others that indicate the data type accepted.

### Category

- provides an additional way to characterize the activity handling the intent, usually related to the user gesture or location from which it's started.
- All implicit intents are defined with `CATEGORY_DEFAULT` by default.
- specify this in your intent filter with the `<category>` element.
Each incoming intent specifies only one action and one data type, but it's OK to declare multiple instances of the `<action>`, `<category>`, and `<data>` elements in each `<intent-filter>`.

```
<activity android:name="ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
        <data android:mimeType="image/*"/>
    </intent-filter>
</activity>
```

- create separate intent filters to specify which actions are acceptable when paired with which data type.

```
<activity android:name="ShareActivity">
    <!-- filter for sending text; accepts SENDTO action with sms URI schemes -->
    <intent-filter>
        <action android:name="android.intent.action.SENDTO"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:scheme="sms" />
        <data android:scheme="smsto" />
    </intent-filter>
    <!-- filter for sending text or images; accepts SEND action and text or image data -->
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="image/*"/>
        <data android:mimeType="text/plain"/>
    </intent-filter>
</activity>

```

### Handle the Intent in your Activity

- To decide what action to take in your activity, read the `Intent` that was used to start it.
- As activity starts, call `getIntent()` to retrieve the `Intent` that started the activity.
- can do this at any time during the lifecycle of the activity, but you should try to do so during early callback such as `onCreate()` or `onStart()`

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    setContentView(R.layout.main);

    // Get the intent that started this activity
    Intent intent = getIntent();
    Uri data = intent.getData();

    // Figure out what to do based on the intent type
    if (intent.getType().indexOf("image/") != -1) {
        // Handle intents with image data ...
    } else if (intent.getType().equals("text/plain")) {
        // Handle intents with text ...
    }
}
```

### Return a Result

- call `setResult()` to specify the result code and result `Intent`.
- when operation is done and the user should return to the original activity, call `finish()` to close your activity.
- must always specify the result code with the result, which is usually `RESULT_OK` OR `RESULT_CANCELED`

```
// Create intent to deliver some kind of result data
Intent result = new Intent("com.example.RESULT_ACTION", Uri.parse("content://result_uri"));
setResult(Activity.RESULT_OK, result);
finish();
```

### Sources

[Android for Developers](https://developer.android.com/training/basics/intents/filters)