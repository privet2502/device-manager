<template>
  <div>
    <h2>Devices</h2>
    <button class="add-device" @click="addDevice">Add Device</button>
    <div v-for="(device, index) in devices" :key="device.id" class="device-container">
      <DeviceItem
        :device="device"
        @save="saveDevice(index, $event)"
        @delete="deleteDevice(index)"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import DeviceItem from './DeviceItem.vue';

const devices = ref([]);

const addDevice = () => {
  devices.value.push({ id: Date.now(), name: '', nodes: [], editing: true });
};

const saveDevice = (index, updatedDevice) => {
  devices.value[index] = updatedDevice;
};

const deleteDevice = (index) => {
  devices.value.splice(index, 1);
};
</script>
