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
      return this.selectedMemo || { index: -1 };
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
          v-for="(todo, index) in todoList"
          :key="index"
          @click="$emit('selectMemo', index)"
        >
          <p
            class="memo-title"
            :class="{ selected: this.currentMemo.index === index }"
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
