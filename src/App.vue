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
      lastId: 1,
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
      this.updateLocalStorage();
      this.lastId++;
      localStorage.setItem("lastId", this.lastId);
    },
    update(memo) {
      const index = this.todoList.findIndex((todo) => todo.id === memo.id);
      this.todoList[index] = memo;
      this.updateLocalStorage();
      this.selectMemo(memo);
    },
    destroy() {
      const index = this.todoList.findIndex(
        (todo) => todo.id === this.selectedMemo.id
      );
      this.todoList.splice(index, 1);
      this.updateLocalStorage();
      this.section = "None";
      this.selectedMemo = null;
    },
    selectMemo(memo) {
      this.selectedMemo = memo;
      this.section = "ShowMemo";
    },
    create() {
      this.selectedMemo = null;
      this.section = "MemoForm";
    },
    getLastId() {
      return parseInt(localStorage.getItem("lastId")) || 1;
    },
    updateLocalStorage() {
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
  },
  created() {
    this.lastId = this.getLastId();
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
      :last-id="lastId"
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
