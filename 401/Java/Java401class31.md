# Espresso

- example of espresso test:

```
@Test
public void greeterSaysHello() {
    onView(withId(R.id.name_field)).perform(typeText("Steve"));
    onView(withId(R.id.greet_button)).perform(click());
    onView(withText("Hello Steve!")).check(matches(isDisplayed()));
}
```

- Espresso tests state expectation, interaction, and assertions clearly without the distraction of boilerplate content, custom infrastructure, or messy implementation details getting in the way.

## Target audience

- targeted at devs who believe that automated testing is an integral part of the development lifecycle.

## Synchronization capabilities

- each time your test invokes `onView()`, Espresso waits to perform the corresponding UI aciton or assertion until the following synchronization conditions are met:
  - message queue is empty
  - no instances of `AsyncTask` currently executing a task
  - all developer-defined `idling resources` are idel.

## Packages

- espresso- core - contains core and basic `View` matchers, actions, and assertions.
- espresso-web - resoureces for `Webview` support.
- espresso-idling-resource - mechanism for synchronization with background jobs.
- espresso-contrib - external contributions that contain `DatePicker`, `RecyclerView` and `Drawer` actions, accessibility checks, and `CountingIdlingResources`
- espresso-intents - extension to validate the stub intents for hermetic testing.
- espresso-remote - location of espresso's multi-purpose functionality/

# Create UI test with Espresso Test Recorder

- lets you create UI test for your app without writing any test code.
- can reord interactions with a device and add assertions to verify UI elements in particular snapshots of your app.
- takes saved recording and auto-generates a corresponding UI test that you can run to test your application.
- based on the `Espresso Testing framwork`, an API in AndroidX.
- by stating expectations, interactions and assertions without directly accessing the underlying app's activites and views, this structure prevents flakiness and optimizes test run speed.
- turn off animations on your test device to repvetn unexpected results.

## Record an Espresso test

- consist of two primary componenets: UI interactions and assertions on View elements.
- UI interactions include tap and type actions that a person my use to interact iwth your app.
- Assertions verify the existence or contents of visual elements on the screen.

## Record UI interactions

1. Click `Run > Record Espresso Test`
2. In the `Select Deployment Target` window, choose device on which you want to record the test. Click Ok.
3. Espresso Test Recorder triggers a build of your project, and the app must install and launch before ETR allows you to interact with it. The `Record Your Test` window appears after the app launches and reads "No events recorded yet." Interact with your device to start logging events.

## Add assertions to verify UI elements

- assertions verify the existence or conents of a View element through 3 main types:
  - text is: checks text content of the selected View element.
  - exist: checks if the View element is present in the current View hierarchy visible on the screen.
  - does not exist: check that the View element is not present in the current View hierarchy.

- To add an assertion to your test:
  1. Click `Add Assertion`. A screen capture dialog appears while Espresso gets the UI heiarchy and other information about the currrent app state.
  2. A layout of the current screen appear in a panel on the right of the `Record Your Test` window. Select a View element and create an assertion by clicking on an element in the screenshot or use th efirst drop-down menu in the `Edit assertion` box at the bottom of the window.
  3. Select assertion you want to use form the second drop-down menu in the `Edit assertion` box. Espresso popluatles the menu with valid assertions for trhe selected View element.
  4. Click `Save and Add Anoter` to create another assertion or click `Save Assertion` to close the assertion panels.

## Save a recording

- use the following steps to save your recording and generate the Espresso test:
  1. click `Complete Recording` and choose a test class name for your test.
  2. Espresso Test Recorder give your test a unique name within its package based on the name of the launched activity. Use the `Test class name` text field if you wan to change the suggested name. Click save.
  3. file automatically opens after ETR generates it, and Android Studio shows the test class as selected in the Project window of the IDE>

### Sources

[Android for Developers](https://developer.android.com/training/testing/espresso)  
[Android for Developers](https://developer.android.com/studio/test/other-testing-tools/espresso-test-recorder)  