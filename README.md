# NativeScript Vue 3 GPS Location Example

This is a working example of how to implement GPS location tracking in a NativeScript Vue 3 application using the @nativescript/location package.

## Features

- Real-time GPS location tracking
- Display of:
  - Latitude
  - Longitude 
  - Altitude
  - Speed
  - Timestamp
- High accuracy location updates
- Proper cleanup of location watchers

## Key Components

- Uses `@nativescript/location` for geolocation services
- Implements location permission requests
- Continuous location watching with 10m update distance
- Location updates displayed in a GridLayout

## Implementation Details

The main functionality is implemented in `Home.vue` and includes:

- Location permission handling
- Watch location setup with high accuracy
- Automatic cleanup on component unmount
- Error handling for location services

## Full Tutorial

For a complete explanation of the implementation, visit:
https://newbiescripter.com/add-gps-functionality-to-app-with-nativescript-geolocation/
