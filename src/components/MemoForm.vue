<script>
export default {
  props: {
    selectedMemo: {
      type: Object,
      required: false,
    },
  },
  data() {
    return {
      title: "",
      content: "",
    };
  },
  methods: {
    save() {
      if (this.title) {
        this.$emit("save", { title: this.title, content: this.content });
        this.title = "";
        this.content = "";
      }
    },
    update() {
      if (this.title) {
        this.$emit("update", { title: this.title, content: this.content });
      }
    },
  },
  mounted() {
    if (this.selectedMemo) {
      this.title = this.selectedMemo.title;
      this.content = this.selectedMemo.content;
    }
  },
};
</script>

<template>
  <div class="section">
    <div class="header" v-text="selectedMemo ? 'Edit Memo' : 'Create Memo'"></div>
    <div class="fill-height">
      <div>
        <label>title</label>
        <input v-model="title" type="text" />
      </div>
      <div class="fill-height">
        <label>content</label>
        <textarea v-model="content" rows="18"></textarea>
      </div>
    </div>
    <div class="action">
      <button v-if="selectedMemo" class="fill-width" @click="update">
        Update
      </button>
      <button v-else class="fill-width" @click="save">Save</button>
    </div>
  </div>
</template>
