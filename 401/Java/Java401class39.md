# Android Location

- using Google play services locatoin APIs, apps can request the last known location of the user's device.
- `fused location provider` is one of the location APIs in GP services- it manages the underlying location tech and provides a simple API so that you can specify requirements at a high level such as accuracy or low power and optimizes the device's use of battery power.

## Create location services client

- in your activity's `onCreate()` method, create an instance of the Fused Location Provider Client

```
private FusedLocationProviderClient fusedLocationClient;

// ..

@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...

    fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
}
```

## Get the last known location

- use the `getLastLocation()` method to retrieve the device's location.
- the precise location returned is determined by the permission setting you put in the app manifest.
- the following code snippet illustrates the request and handling of the response:

```
fusedLocationClient.getLastLocation()
        .addOnSuccessListener(this, new OnSuccessListener<Location>() {
            @Override
            public void onSuccess(Location location) {
                // Got last known location. In some rare situations this can be null.
                if (location != null) {
                    // Logic to handle location object
                }
            }
        });
```

- `getLastLocation()` returns a `Task` that you can use to get a `Location` object with the latitude and longitude coordinates of a geographic location.
- location object may be null in the following situation:
  - Location is turned off in the devices settings- disabling location also clears the cache.
  - device never recorded its location - device is new or has been restored to factory settings.
  - Google Play services on the device has restarted, and there is no active Fused Location Provider client that has requested location after the services restarted.

  ## Choose the best location estimate

- `FusedLocationProviderClient` provides several methods to retrieve device location information:
  - `getLastLocation()` - gets a location estimate more quickly and minimizes battery usage that can be attributed to your app but location might be out of date if no other clients have actively used location recently.
  - `getCurrentLocation()` - get a newer, more accurate location more consistently. Can cause active location computation to occur on the device.
- this is the recommended way to get a fresh location, whenever possible as its safe than alternatives like starting and managing location updates yourself using `requestLocationUpdates()`- this can consume lasrge amounts of power if location isn't available or if the request isn't stopped correctly after getting a new location.

## Change location settings

- if your app needs to request location or receive permission updates, the device needs to enable the appropriate system settings such as GPS or Wi-Fi scanning.
- instead of enabling service such as the device's GPS, your app specifies the required level of accuracy/power consumption and desired update interval- the device will automatically make the appropriate change to system settings

## Configure location services

- connect your app using the `Settings Client` in order to use the GP services and fused location provider.
- apps that use location services must request location permissions, depending on the use cases of those features.

## Set up a location request

- create a `LocationRequest` to store parameters for requests to the fused location provider. These params determine the level of accuracy for requests.
- `setInterval()` sets the rate in milliseconds at which your app prefers to recieve location updates.
- `setFastestInterval()` - sets the fastest rate in milliseconds at which your app can handle location updates.

## Priority

- `setPriority()` - this method sets the priority of the request and gives Google play services location services a hint about  which location sources to use.
  - `PRIORITY_BALANCED_POWER_ACCURACY` - Use this setting to request location precision to within a city block, which is an accuracy of approximately 100 meters. This is considered a coarse level of accuracy, and is likely to consume less power. With this setting, the location services are likely to use WiFi and cell tower positioning. Note, however, that the choice of location provider depends on many other factors, such as which sources are available.
  - `PRIORITY_HIGH_ACCURACY` - Use this setting to request the most precise location possible. With this setting, the location services are more likely to use GPS to determine the location.
  - `PRIORITY_LOW_POWER` - Use this setting to request city-level precision, which is an accuracy of approximately 10 kilometers. This is considered a coarse level of accuracy, and is likely to consume less power.
  - `PRIORITY_NO_POWER` - Use this setting if you need negligible impact on power consumption, but want to receive location updates when available. With this setting, your app does not trigger any location updates, but receives locations triggered by other apps.

```
protected void createLocationRequest() {
    LocationRequest locationRequest = LocationRequest.create();
    locationRequest.setInterval(10000);
    locationRequest.setFastestInterval(5000);
    locationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
}
```

## Get current location settings

- to get the current location, create a `LocationSettingsRequest.Builder` and add one or more location requests

```
LocationSettingsRequest.Builder builder = new LocationSettingsRequest.Builder()
     .addLocationRequest(locationRequest);
LocationSettingsRequest.Builder builder = new LocationSettingsRequest.Builder();

// ...

SettingsClient client = LocationServices.getSettingsClient(this);
Task<LocationSettingsResponse> task = client.checkLocationSettings(builder.build());

```

## Prompt the user to chagne location settings

- add an `OnFailureListener` to the `Task` object to validate the location settings, then check if the `Exception` object passed to the `onFailure()` method is an instance of the `ResolvableApiException` class, which indicates that the settings must be changed.

```
task.addOnSuccessListener(this, new OnSuccessListener<LocationSettingsResponse>() {
    @Override
    public void onSuccess(LocationSettingsResponse locationSettingsResponse) {
        // All location settings are satisfied. The client can initialize
        // location requests here.
        // ...
    }
});

task.addOnFailureListener(this, new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception e) {
        if (e instanceof ResolvableApiException) {
            // Location settings are not satisfied, but this can be fixed
            // by showing the user a dialog.
            try {
                // Show the dialog by calling startResolutionForResult(),
                // and check the result in onActivityResult().
                ResolvableApiException resolvable = (ResolvableApiException) e;
                resolvable.startResolutionForResult(MainActivity.this,
                        REQUEST_CHECK_SETTINGS);
            } catch (IntentSender.SendIntentException sendEx) {
                // Ignore the error.
            }
        }
    }
});
```

### Sources

[Android for Developers](https://developer.android.com/training/location/retrieve-current)