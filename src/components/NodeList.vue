<template>
  <div class="node-list">
    <h3>Device Nodes</h3>
    <button class="add-device" @click="addNode">Add Node</button>
    <div v-for="(node, index) in nodes" :key="node.id" class="node-container">
      <NodeItem
        :node="node"
        @save="saveNode(index, $event)"
        @delete="deleteNode(index)"
      />
    </div>
  </div>
</template>

<script setup>
import NodeItem from './NodeItem.vue';

const props = defineProps({
  nodes: Array
});

const emit = defineEmits(['updateNodes']);

const addNode = () => {
  props.nodes.push({ id: Date.now(), name: '', editing: true });
  emit('updateNodes', [...props.nodes]);
};

const saveNode = (index, updatedNode) => {
  props.nodes[index] = updatedNode;
  emit('updateNodes', [...props.nodes]);
};

const deleteNode = (index) => {
  props.nodes.splice(index, 1);
  emit('updateNodes', [...props.nodes]);
};
</script>
