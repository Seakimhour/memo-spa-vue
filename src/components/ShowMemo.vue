<script>
export default {
  props: {
    todoList: {
      type: Array,
      required: true,
    },
    selectedMemo: {
      type: Object,
      required: true,
    },
  },
};
</script>

<template>
  <div class="section">
    <div class="header">Show Memo</div>
    <div class="fill-height">
      <div>
        <label>title</label>
        <p class="memo-property">{{ selectedMemo.title }}</p>
      </div>
      <div class="fill-height">
        <label>content</label>
        <p class="memo-property fill-height">{{ selectedMemo.content }}</p>
      </div>
    </div>
    <div class="action">
      <button class="fill-width" @click="$emit('edit')">Edit</button>
      <button @click="$emit('delete')">Delete</button>
    </div>
  </div>
</template>

<style scoped>
.memo-property {
  background-color: aliceblue;
  padding: 10px;
  border-radius: 10px;
}
</style>
