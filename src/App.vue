<script>
import MemoList from "./components/MemoList.vue";
import ShowMemo from "./components/ShowMemo.vue";
import MemoForm from "./components/MemoForm.vue";

export default {
  components: {
    MemoList,
    ShowMemo,
    MemoForm,
  },
  data() {
    return {
      todoList: [],
      section: "None",
      selectedMemo: null,
    };
  },
  methods: {
    getTodoList() {
      return JSON.parse(localStorage.getItem("todoList")) || [];
    },
    store(memo) {
      this.todoList.push(memo);
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    update(memo) {
      this.todoList[this.selectedMemo.index] = memo;
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
      this.selectMemo(this.selectedMemo.index);
    },
    destroy() {
      this.todoList.splice(this.selectedMemo.index, 1);
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
      this.section = "None";
      this.selectedMemo = null;
    },
    selectMemo(index) {
      this.selectedMemo = this.todoList[index];
      this.selectedMemo.index = index;
      this.section = "ShowMemo";
    },
    create() {
      this.selectedMemo = null;
      this.section = "MemoForm";
    },
  },
  created() {
    this.todoList = this.getTodoList();
  },
};
</script>

<template>
  <main>
    <MemoList
      :todo-list="todoList"
      :selected-memo="selectedMemo"
      @selectMemo="selectMemo"
      @create="create"
    />
    <component
      :is="section"
      :todo-list="todoList"
      :selected-memo="selectedMemo"
      @edit="section = 'MemoForm'"
      @save="store"
      @update="update"
      @delete="destroy"
    />
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: row;
  width: 600px;
  height: 500px;
  margin: auto;
  padding: 10px;
  border-radius: 0.25rem;
  background-color: white;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
}
</style>
