<template>
  <div class="node-item">
    <div v-if="isEditing" class="editing">
      <input v-model="editedNode.name" placeholder="Node Name" />
      <div class="flex-row">
        <button class="save-button" @click="save">Save</button>
        <button class="delete-button" @click="deleteNode">Delete</button>
      </div>
    </div>
    <div v-else>
      <span>{{ node.name }}</span>
      <div class="flex-row">
        <button class="edit-button" @click="edit">Edit</button>
        <button class="delete-button" @click="deleteNode">Delete</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  node: Object
});

const emit = defineEmits(['save', 'delete']);

const editedNode = ref({ ...props.node });
const isEditing = ref(props.node.editing);

const save = () => {
  isEditing.value = false;
  emit('save', { ...editedNode.value, editing: false });
};

const edit = () => {
  isEditing.value = true;
};

const deleteNode = () => {
  emit('delete');
};
</script>
