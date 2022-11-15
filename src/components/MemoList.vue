<script>
export default {
  props: {
    todoList: {
      type: Array,
      required: true,
    },
    selectedMemo: {
      type: Object,
    },
  },
  computed: {
    currentMemo() {
      return this.selectedMemo || { id: -1 };
    },
  },
};
</script>

<template>
  <div class="section">
    <div class="fill-height">
      <div class="header">Memo List</div>
      <div class="memo-list">
        <div
          v-for="todo in todoList"
          :key="todo.id"
          @click="$emit('selectMemo', todo)"
        >
          <p
            class="memo-title"
            :class="{ selected: this.currentMemo.id === todo.id }"
          >
            {{ todo.title }}
          </p>
        </div>
      </div>
    </div>
    <div class="action">
      <button class="fill-width" @click="$emit('create')">New Memo</button>
    </div>
  </div>
</template>

<style scoped>
.memo-list {
  padding-right: 30px;
}

.memo-title {
  color: blue;
  cursor: pointer;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.selected {
  color: black;
  cursor: default;
}
</style>
