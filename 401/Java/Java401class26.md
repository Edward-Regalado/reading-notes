# Application Fundamentals

- android apps can be written in Kotlin, Java and C++ languages.
- An android package, which is an archive file with an apk suffix, contains the contents of an Android app that are required at runtime and it is the file that Android-powered devices use to install the app.
- An Android App Bundle, which is an archive file with an aab suffix, contains the contents of an Android app project including some additional metadata that is not required at runtime.
  - Each Android app lives in its own security sandbox, protected by the following Android security features:
  - Android OS is a multi-user Linus system in which each app is a different user.
  - By default, the system assigns each app a unique Linus user ID(used only by the system and is unknown by the app). The system sets permissions for all the files in an app so that only the user ID assigned to that app can access them.
  - each process has its own VM, so an app's code runs in isolation from other apps.
  - By default, every app runs in its own Linus process. The Android system starts the process when any of the app's components that it requires to do its work and no more. Very secure env in which an app cannot access parts of the system for which it is not given permission.

## App Components

- essential building blocks of an Android app.
- each comp is an entry point through which the system or a user can enter your app.
- each type serves a distinct purpose and has a distinct lifecycle that defines how the component is created and destroyed.
- 4 different types of app components:
  - Activities
  - Services
  - Broadcast receivers
  - Content providers

### Activities

- an entry point for interacting with the user.
- represents a single screen with a user interface.
- An activity facilitates the following key interactions between system and app:
  - keeping track of what the user currently care about (what is on the screen) to ensure that the system keeps running the process that is hosting the activity
  - knowing that previously used processes contain things the user may return to (stopped activities)- more highly prioritize keeping those processes around
  - helping the app handling having its process killed so the user can return to activities with their previous state restored.
  - providing a way for apps to implement user flows between each other, and for the system to coordinate these flows.

### Services

- services is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.
- its a component that performs long-running operations or to perform work for remote processes.
- does not provide a user interface.
- plays music in the background while user is in a different app, or might fetch data over the network without blocking user interaction with an activity.
- another component can start the service and let it run or bind to it in order to interact with it.

### Started Services

- tells the system to keep them running until their work is completed- syncing data in the background or playing music after user leaves app.
- music playback (user directly aware of), apps tells the system it want to be foreground with a notification to tell the user about it; system tries really hard to keep this service running. - a regular background service is not something the user is directly aware as running, so the system has more freedom in managing its process (may get killed or restarted later if it needs RAM)

### Bound Services

- these services run because of some other app (or the system) has said that it wants to make use of the service.
- basically the service providing an API to another process (there's a dependency between service A and B)
- services are useful building blocks for all kinds of higher-level system concepts (notifications, live wallpapers, screen savers, input methods)

### Broadcast receivers

- component that enables the system to deliver events to the app outside of a regular user flow, allowing the app to respond to system-wide broadcast announcements.
- system can deliver broadcast even to apps that aren't currently running (schedule an alarm to post a notification )
- gateway to other components and is intended to do a very minimal amount of work.

### Content providers

- manages a shared set of app data that you can store in the file system, in a SQlite database, on the web, or in any other persistent storage location that your app can access.
- through the content provider, other apps can query or modify the data if the content provider allows it.
- it's an entry point into an app for publishing named data items, identified by a URI scheme.
- app can decide how it wants to map the data it contains to the URI namespace, handing out those URIs to other entities which can in turn use them to access the data.
- assign a URI doesn't require that the app remain running- URIs can persist after their owning apps have exited.
- URIs provide an important fine-grained security model. Uses a temporary URI permission grant to give apps access to a specific piece of data and nothing more.
- Useful for reading and writing data that is private to your app and not shared.
- Android apps don't have a single entry point(there's not main() function).
- b/c the system runs each app in a separate process with file permissions that restrict access to other apps, your app cannot directly activate a component from another app.

### Activating components

- activities, services and broadcast receivers components are activated by an asynchronous message called an intent.
- Intent bind individual comps to each other at runtime- they're like messengers that request an action from other components, whether the comp belongs to your app or another.
- intents are created with an Intent object, which defines a message to activate either a specific component or a specific type of component.
- For activities and service, an intent defines the action to perform (to view or send something) and may specify the URI of the data to act on.
- For broadcast receivers, the intent simply defines the announcement being broadcast (battery is low).
- content providers are not activated by intents- they are activated when targeted by a request from a ContentResolver.
- content resolvers handles all direct transactions with the content provider so that the component that's performing transactions with the provider doesn't need to and instead calls methods on the ContentResolver object.

#### Methods for activating each component

- activity: pass an Intent to `startActivity()` or `startActivityForResult()`
- broadcast: pass an Intent to methods such as `sendBroadcast()`, `sendOrderedBroadcast` or `sendStickyBroadCast()`
- content provider: perform a query by calling `query()` on a `ContentResolver`

### The manifest file

- primary task is to inform the system about the app's components.
- AndroidManifest.xml app must declare all of its components in this file and it must be at the root of the app project directory.
- identifies any user permissions the app requires, such as internet access or read-access to the user's contacts
- declares the min API level required by the app, based on which APIs the app uses.
- declares hardware and software features used or required by the app (camera, Bluetooth services).
- declares API libraries the app needs to be linked against.

### Declaring components

```
<?xml version="1.0" encoding="utf-8"?>
<manifest ... >
    <application android:icon="@drawable/app_icon.png" ... >
        <activity android:name="com.example.project.ExampleActivity"
                  android:label="@string/example_label" ... >
        </activity>
        ...
    </application>
</manifest>
```

- In the `<application>` element, android:icon attribute points to resources for an icon that identifies the app.
- In the `<activity>` element, android:name attribute specifies the full qualified class name of the Activity subclass and the android:label attribute specifies a string to use as the user-visible label for the activity.

- must declare all app comps using the following elements:

  - `<activity>`: for activies
  - `<service>`: for services
  - `<receiver>`: for broadcast receivers
  - `<provider>`: for content providers


### Declaring components capabilities

- When you declare an activity in your app's manifest, you can optionally include intent filters that declare the capabilities of the activity so it can respond to intents from other apps.
- declare an intent filter for your component by adding an `<intent-filter>` element as a child of the component's declaration element.

### Declaring app requirements

- To prevent your app from being installed on devices that lack features needed by your app, it's important that you clearly define a profile for the types of devices your app supports by declaring device and software requirements in your manifest file.
- used by external services such as GP in order to provide filtering for users when they search for apps for their device.

### App resources

- using app resources makes it easy to update various characteristics of your app without modifying code.
- providing sets of alternative resources enables you to optimize your app for a variety of device configs (screen sizes, languages).
- every resource defined in your project, SDK provides a unique integer ID.
- qualifier is a short string that you include in the name of your resource directories in order to define the device config for which those resources should be used.
- you can define two different layouts and apply the appropriate qualifier to each layout's directory name- system will auto apply the appropriate layout depending on the current device orientation.

### Sources

(Android for Developers)[https://developer.android.com/guide/components/fundamentals]