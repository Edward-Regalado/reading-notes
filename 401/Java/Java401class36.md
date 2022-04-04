# Authentication

- Amplify Auth category provides an interface for authenticating a user.
- amplify CLI helps you to craet and configure the auth category with an authentication provider.

## Goal 

- setup and configure your application with Amplify Auth and go through a simple api to check the current auth session

## Configure Auth Category

- run `amplify add auth`
- Enter the following when prompted:

```
? Do you want to use the default authentication and security configuration?
    `Default configuration`
? How do you want users to be able to sign in?
    `Username`
? Do you want to configure advanced settings?
    `No, I am done.`

```

- run: `amplify push`
- once completed, `amplifyconfiguration.json` should be updated to reference provisioned backend auth resources.

## Install Amplify Libraries

- add the following dependency to your app's `build.gradle` along with others you added above in Prerequisites and click "Sync Now" when prompted:

```
dependencies {
    implementation 'com.amplifyframework:aws-auth-cognito:1.33.0'
}
```

## Initialize Amplify Auth

- add the Auth plugin before calling `Amplify.configure`

```
// Add this line, to include the Auth plugin.
Amplify.addPlugin(new AWSCognitoAuthPlugin());
Amplify.configure(getApplicationContext());
```

## Check the current auth session

- run the following code in your MainActivity's `onCreate` method.

```
Amplify.Auth.fetchAuthSession(
    result -> Log.i("AmplifyQuickstart", result.toString()),
    error -> Log.e("AmplifyQuickstart", error.toString())
);
```

# Sign in

- Auth category can be used to register a user, confirm attributes like email/phone, and sign in with optional multi-factor authentication.
- It's set up to use Amazon  Cognito User Pools which manages the users and their properties.

## Register a user

- default CLI flow requires a username, password and a valid email id as paramters to register a user.
- Invoke the following api to initiate a sign up flow.

```
AuthSignUpOptions options = AuthSignUpOptions.builder()
    .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
    .build();
Amplify.Auth.signUp("username", "Password123", options,
    result -> Log.i("AuthQuickStart", "Result: " + result.toString()),
    error -> Log.e("AuthQuickStart", "Sign up failed", error)
);

```

- next, confirm the user by sending a confirmation code to the email id provided during sign up.
- Enter confirmation code in the `confirmSignUp` call

```
Amplify.Auth.confirmSignUp(
    "username",
    "the code you received via email",
    result -> Log.i("AuthQuickstart", result.isSignUpComplete() ? "Confirm signUp succeeded" : "Confirm sign up not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

- once complete, you should see the following in your console `Confirm signUp succeeded`

## Sign in a user

- implement a UI to get the username and password from the user.
- after user enters their credentials you can start the sign in flow by calling the following method:
- once complete, you should see `Sign in succeeded` in your console

```
Amplify.Auth.signIn(
    "username",
    "password",
    result -> Log.i("AuthQuickstart", result.isSignInComplete() ? "Sign in succeeded" : "Sign in not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

## Multi-factor authentication

- some steps in setting up MFA can only be chosen during the initial setup of Auth so if you already added Auth via the CLI, run `amplify auth remove` and when that completes, `amplify push` to remove it.
- run: `amplify add auth` and setup Auth with the following options:
- once complete, run: `amplify push` to push changes to the cloud

```
? Do you want to use the default authentication and security configuration?
    `Manual configuration`
? Select the authentication/authorization services that you want to use:
    `User Sign-Up, Sign-In, connected with AWS IAM controls (Enables per-user Storage features for images or other content, Analytics, and more)`
? Please provide a friendly name for your resource that will be used to label this category in the project:
    `<default>`
? Please enter a name for your identity pool.
    `<default>`
? Allow unauthenticated logins? (Provides scoped down permissions that you can control via AWS IAM)
    `Yes`
? Do you want to enable 3rd party authentication providers in your identity pool?
    `No`
? Please provide a name for your user pool:
    `<default>`
Warning: you will not be able to edit these selections.
? How do you want users to be able to sign in?
    `Username`
? Do you want to add User Pool Groups?
    `No`
? Do you want to add an admin queries API?
    `No`
? Multifactor authentication (MFA) user login options:
    `ON (Required for all logins, can not be enabled later)`
? For user login, select the MFA types:
    `SMS Text Message`
? Please specify an SMS authentication message:
    `Your authentication code is {####}`
? Email based user registration/forgot password:
    `Enabled (Requires per-user email entry at registration)`
? Please specify an email verification subject:
    `Your verification code`
? Please specify an email verification message:
    `Your verification code is {####}`
? Do you want to override the default password policy for this User Pool?
    `No`
Warning: you will not be able to edit these selections.
? What attributes are required for signing up?
    `Email, Phone Number (This attribute is not supported by Facebook, Login With Amazon.)`
? Specify the app's refresh token expiration period (in days):
    `30`
? Do you want to specify the user attributes this app can read and write?
    `No`
? Do you want to enable any of the following capabilities?
    `NA`
? Do you want to use an OAuth flow?
    `No`
? Do you want to configure Lambda Triggers for Cognito?
    `No`
```

- in order to send SMS auth codes, you must request an origination number.
- If AWS account is in the SMS sandbox, you must also add a destination phone number by going to the Amazon Pinpoint Console, selecting SMS and voice in the nav pane, and selecting Add phone number in the Destination phone nums tab.
- To check if your AWS account is in the SMS sandbox, go to the SNS console, select the Text messaging tab from the navigation pane, and check the status under the Account information section.
- be sure to include both email and phone attributes when you sign up.

```
ArrayList<AuthUserAttribute> attributes = new ArrayList<>();
attributes.add(new AuthUserAttribute(AuthUserAttributeKey.email(), "my@email.com"));
attributes.add(new AuthUserAttribute(AuthUserAttributeKey.phoneNumber(), "+15551234567"));

Amplify.Auth.signUp(
    "username",
    "Password123",
    AuthSignUpOptions.builder().userAttributes(attributes).build(),
    result -> Log.i("AuthQuickstart", result.toString()),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

- confirm singup , sign in, and get back a nextStep in the sign in result of type `CONFIRM_SIGN_IN_WITH_SMS_MFA_CODE`.
- confirmation code will also be texted to the phone number provided above.
- pass the code you recieved to the confirmSignIn api:

```
Amplify.Auth.confirmSignIn(
    "confirmation code received via SMS",
    result -> Log.i("AuthQuickstart", result.toString()),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

# Sign in with web UI

- in terminal, nav to your project and run: `amplify update auth` and chose the following options:
- once compolete, run: `amplify push` to publish changes.

```
? Do you want to use the default authentication and security configuration? 
    `Default configuration with Social Provider (Federation)`
? How do you want users to be able to sign in? 
    `Username`
? Do you want to configure advanced settings? 
    `No, I am done.`
? What domain name prefix you want us to create for you? 
    `(default)`
? Enter your redirect signin URI: 
    `myapp://callback/`
? Do you want to add another redirect signin URI 
    `No`
? Enter your redirect signout URI: 
    `myapp://signout/`
? Do you want to add another redirect signout URI 
    `No`
? Select the social providers you want to configure for your user pool: 
    `<hit enter>`
```

## Update AndroidManifest.xml

- add the following activity and queries tag to your apps `AndroidManifest.xml` file, replacing `myapp` with your redirected URI prefix if necessary:

```
<queries>
  <intent>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="https" />
  </intent>
  <intent>
    <action android:name=
        "android.support.customtabs.action.CustomTabsService" />
  </intent>
</queries>
<application ...>
  ...
  <activity
      android:name="com.amplifyframework.auth.cognito.activities.HostedUIRedirectActivity"
      android:exported="true">
      <intent-filter>
          <action android:name="android.intent.action.VIEW" />
          <category android:name="android.intent.category.DEFAULT" />
          <category android:name="android.intent.category.BROWSABLE" />
          <data android:scheme="myapp" />
      </intent-filter>
  </activity>
  ...
</application>
```

- add redirect to an Activity  when the user signs in or out, add  an `<activity></activity>` block like the following inside your `<applicatoin>`:
- this will connect your URI `myapp://signout` to a redirect to the Activity name `LogoutActivity`

```
<activity android:name=".LogoutActivity" android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="myapp" android:host="signout" />
    </intent-filter>
</activity>

```

### Add Response Handler

- add the following result handler to whichever `Activity` you are call ing HostedUI from:

```
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if (requestCode == AWSCognitoAuthPlugin.WEB_UI_SIGN_IN_ACTIVITY_CODE) {
        Amplify.Auth.handleWebUISignInResponse(data);
    }
}
```
### Launch Web UI Sign In

- run this method in your `onCreate` method of MainActivity:

```
Amplify.Auth.signInWithWebUI(
    this,
    result -> Log.i("AuthQuickStart", result.toString()),
    error -> Log.e("AuthQuickStart", error.toString())
);
```

### Sources

[Amplify Docs](https://docs.amplify.aws/lib/auth/getting-started/)