<script lang="ts" setup>
import {
  ref,
  onMounted,
  onUnmounted,
} from 'nativescript-vue';
import * as Geolocation from '@nativescript/geolocation';
import { CoreTypes } from '@nativescript/core';

const location = ref<Geolocation.Location | null>(null);
const watchId = ref<number | null>(null);

function startLocationUpdates() {
  console.log('Starting location updates');

  Geolocation.enableLocationRequest()
    .then(() => {
      Geolocation.watchLocation(
        (result) => {
          location.value = result;
        },
        (error) => {
          console.error('Error watching location:', error);
        },
        {
          desiredAccuracy: CoreTypes.Accuracy.high,
          updateDistance: 10,
        }
      )
      .then((id) => {
        watchId.value = id;
      });
    })
    .catch((error) => {
      console.error('Error enabling location request:', error);
    });
}

const onLoaded = () => {
  console.log('mounted');
  startLocationUpdates();
};

onUnmounted(() => {
  console.log('unmounted');
  if (watchId.value) {
    Geolocation.clearWatch(watchId.value);
  }
});
</script>

<template>
  <Frame>
    <Page @loaded="onLoaded">
      <ActionBar>
        <Label text="Home" class="font-bold text-lg" />
      </ActionBar>

      <GridLayout rows="*, auto, auto, *" class="px-4">
        <Label
          row="1"
          textWrap="true"
          class="text-xl align-middle text-left text-gray-500"
          :text="location ? 
              'Lat: ' + location.latitude + '\n' +
              'Long: ' + location.longitude + '\n' +
              'Alt: ' + location.altitude + '\n' +
              'Speed: ' + location.speed + '\n' +
              'Timestamp: ' + location.timestamp
              : 'No location'"
        />
      </GridLayout>
    </Page>
  </Frame>
</template>

<style>
/* .info {
    font-size: 20;
  } */
</style>
