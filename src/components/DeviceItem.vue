<template>
  <div class="device-item">
    <div v-if="isEditing" class="editing">
      <input v-model="editedDevice.name" placeholder="Device Name" />
      <div class="flex-row">
        <button class="save-button" @click="save">Save</button>
        <button class="delete-button" @click="deleteDevice">Delete</button>
      </div>
    </div>
    <div v-else>
      <span>{{ device.name }}</span>
      <div class="flex-row">
        <button class="edit-button" @click="edit">Edit</button>
        <button class="delete-button" @click="deleteDevice">Delete</button>
      </div>
    </div>
    <NodeList v-if="!isEditing" :nodes="device.nodes" @updateNodes="updateNodes"/>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import NodeList from './NodeList.vue';

const props = defineProps({
  device: Object
});

const emit = defineEmits(['save', 'delete']);

const editedDevice = ref({ ...props.device });
const isEditing = ref(props.device.editing);

const save = () => {
  isEditing.value = false;
  emit('save', { ...editedDevice.value, editing: false });
};

const edit = () => {
  isEditing.value = true;
};

const deleteDevice = () => {
  emit('delete');
};

const updateNodes = (newNodes) => {
  editedDevice.value.nodes = newNodes;
};

watch(props.device, (newDevice) => {
  editedDevice.value = { ...newDevice };
});
</script>
