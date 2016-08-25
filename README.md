# android-wificonnect
An android library to effortlessly connect to available WiFi networks

## Supported Features

### Upcoming
- APIs that enables connection to any network (Open/WEP/WPA etc). There should be APIs that accept password in case network needs authentication.

### Version 0.1.0
- Initiate a scan for networks explicitly. If WiFi is turned off, it's turned on automatically and an attempt is made to connect to network.
- Scenarios specific to Android L (API Level 21-22) and Android Marshmallow (API Level 23) are handled. In case a user wants to connect to a network that doesn't provide internet connectivity (Captive Portal), `WifiConnectionManager.setBindingEnabled(true)` can be called that would ensure that the app uses the network (to which the device would connect to when `WifiConnectionManager.connectToAvailableSSID(String SSID, ConnectionStateListener listener)` is called) to route traffic irrespective of whether it provides internet connectivity.
- `WifiConnectionManager.connectToAvailableSSID(List<String> SSIDs, ConnectionStateListener listener)` accepts a list of SSIDs and can connect to an available network with strongest singal that has an SSID among SSIDs.
- Provide methods like `WifiConnectionManager.checkBoundNetworkConnectivity()` that enabled verifying and switching to using WiFi network to which app is bound currently for sending network traffic for whole device. It makes it as active network if network connectivity is available in case now Captive Portal login has been performed, otherwise it switches from using currently bound network.
- User can listen to `AdvancedConnectionState` that provides callback at different logical points in the process of connecting to a network.
- User receives a callback once either the connection has been successfully established `ConnectionStateListener.onConnectionEstablished()` or an error occurs `ConnectionStateListener.onConnectionError()`.

### Limitations as of Now
- As of now user can only connect to an Open Network (that doesn't need any authentication) using `connectToAvailableSSID()`

**Note:**
 1. Marshmallow dynamic permissions must be handled for the library to work as WiFi scanning starting from Android M needs ACCESS_COARSE_LOCATION permission.
 2. Location should be enabled to get WiFi scan results.