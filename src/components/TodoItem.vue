<script>
export default {
  props: {
    todo: {
      type: String,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      isEditing: false
    };
  },
  methods: {
    save() {
      this.$emit('update', this.index, this.todo);
      this.isEditing = false;
    }
  }
};
</script>

<template>
  <div v-if="!isEditing" class="item">
    <p>{{ todo }}</p>
    <div>
      <button @click="isEditing = true">Edit</button> |
      <button @click="$emit('destroy', index)">Delete</button>
    </div>
  </div>
  <div v-else>
    <input v-model="todo" type="text" placeholder="Type something..." />
    <button @click="save()">Save</button>
  </div>
</template>

<style scoped>
.item {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 5px;
}
</style>
