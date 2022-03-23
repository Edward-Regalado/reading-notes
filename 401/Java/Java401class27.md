## Tasks and the back stack

- A task is a collection of activities that users interact with when trying to do something in your application.
- new activities are arranged in a stack -- the back stack -- in the order in which each activity is opened.
- when are user presses back, the new activity is finished and popped off the stack.


## Lifecycle of a task and its back stack

- device Home screen is the starting place for most tasks.
-when an app is launched that app's task comes to the foreground and if no task exist for the app (hasn't been used recently), then a new task is created and the main activity for that app opens are the root activity in the stack.
- when current activity starts another, the new activity is pushed on the top of the stack and takes focus.
- previous activity remains in the stack, but is stopped but the system retains the current state of its user interface.
- when a user hits the back button, the current activity is popped from the top of the stack (gets destroyed) and previous activity resumes.
- activities in the stack are never rearranged, only pushed and popped.
- Stacks operate on the last-in, first-out (LIFO) object structure.
- when the stack becomes empty in the current application, user will simply be returned to the home screen.

## Back press behavior for root launcher activities

- Root launcher activates are activities that declare an `Intent` filer with both `ACTION_MAIN` and `CATEGORY_LAUNCHER`.
- these activities act as entry points into your app form the app launcher and are used to start a task.
- Behavior of the back gesture at the root launcher activity differs depending on which version of android the device is running.
  - Andriod 11 and lower: finished the activity
  - Andriod 12 and higher: moves activity to the background

## Background and foreground tasks

- A task is a cohesive unit that can move to the background when a user begins a new task or goes to the Home screen.
- all activities within the app are stopped when the app is in the background, but the back stack remains intact.
- each app gets its own stack of activities.

## Multiple activity instance

- activities in the back stack are never rearranged, so new instances are created and pushed onto the stack rather than brining previous instances of the activity to the top.
- activates can be instantiated multiple times, even from other tasks.
- can modify this behavior if you do not want an activity to be instantiated more than once.

## Multi-window environments

- system manages tasks separately for each window and each window may have multiple tasks.

## Manage tasks

- android manages tasks and the back stack by placing all activities started in succession in the same task and in a LIFO.
- you can interrupt the normal behavior with attributes in the `<activity>` manifest element and with flags in the intent that you pass startActivity().

## Defining launch modes

- allows you to define how a new instanc eof an activity is associated with the current task.
- Using the `manifest` file: can specify how the activity should associate with tasks when it starts
- Using `Intent flags`: when you call `startActivity()`, you can include a flag in the Intent that declares how the new activity should associate with the current task.
- The `launchMode` attribute specifies an instruction on how the activity should be launched into a task and it has 4 different modes:
  - `standard`: Default. System creates a new instance of the activity in the task from which it started and routes the intent to it. Can be instantiated multiple times
  - `singleTop`: if an instance already exist at the top of the current task, the system routes the intent to that instacne through a call to its `onNewIntent()` method, rather than creating a new instance. Can be instantiated multiple times and each instance can belong to different tasks.
  - `singleTask`: system creates a new task and instantiates the activity at the root of the new stack. If an instance of the activity already exist in a separate task, the system routes the intent to that instance through a call to `onNewIntent()` method.
  - `singleInstance`: system doesn't launch any other activities into the task holding the instance. The activity is always single and only member if its task: any activities started by this one open in a separate task.

## Define lauch mode using Intent flags

- `FLAG_ACTIVITY_NEW_TASK`: start activity in a new task. If a task is already running, that task is brought to the foreground with its last state restored and receives the new intent in `onNewIntent()`
- `FLAG_ACTIVITY_SINGLE_TOP`: if the activity being started is the current activity (top of the back stack), then the existing instance receives a `call to onNewIntent()`, instead of creating a new instance.
- `FLAG_ACTIVITY_CLEAR_TOP`: if the activity being started is already running in the current task, all other activities on top of it are destroyed and this intent is delivered to the resume instance of the activity thought `onNewIntent()`

## Handle affinities

- An affinity indicates which task an activity prefers to belong to.
all activities from the same app have an affinity for each other by default and prefer to be in the same task.

## Clear the back stack

- when a user leaves a task for a long period of time, the system clears the task of all activities except the root activity.
only the root is restore when the user returns.

## Start a task

- set up an activity as the entry point for a task by giving it an intent filter with android.intent.action.MAIN
- an intent filter of this kind causes an icon and label for the activity to be displayed in the app launcher, giving the users a way to launch the activity and to return to the task it creates any time after it has been launched.

```
<activity ... >
    <intent-filter ... >
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
    ...
</activity>
```

## Save key-value data

- `SharedPreferences` saves the user's settings
if you have a small collection of key-values that you'd like to save, use the `SharedPreferences` APIs.
- A `SharedPreferences` object points to a file containing key-value pairs and provides simple methods to read and write them.

## Get a handle to shared preferences

- create a new shared preference file or access an existing one by calling one of these methods:
  - `getSharedPreferences()`: use this if you need multiple shared preference files identified by name.
  - `getPreferences()`: use this from an Activity if you need to use only one shared preference file for the activity.

```
Context context = getActivity();
SharedPreferences sharedPref = context.getSharedPreferences(
        getString(R.string.preference_file_key), Context.MODE_PRIVATE);

//  one shared preference file
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
```

- choose unique names when naming your shared preference files that is identifiable to your app.
- prefix the file name with your application ID `com.example.myapp.PREFERENCE_FILE_KEY`

## Write to shared preferences

- create a `SharedPreferences.Editor` by calling `edit()` on your SharedPreferences
- pass the keys and values you want to write with methods such as `putInt()`, `putString()`. Then call `apply()` or `commit()` to save.

```
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor editor = sharedPref.edit();
editor.putInt(getString(R.string.saved_high_score_key), newHighScore);
editor.apply();
```

## Read from shared preferences

- call methods such as `getInt()` and `getString()`, providing the key for the value you want

```
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
int defaultValue = getResources().getInteger(R.integer.saved_high_score_default_key);
int highScore = sharedPref.getInt(getString(R.string.saved_high_score_key), defaultValue);
```

## Sources

[Android for Developers](https://developer.android.com/guide/components/activities/tasks-and-back-stack)  

[Andriod for Developers](https://developer.android.com/training/data-storage/shared-preferences#java)
