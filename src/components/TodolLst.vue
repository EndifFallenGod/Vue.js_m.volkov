<template>
  <ul class="list-group">
    <li class="list-group-item" v-for="(item, i) in list" :key="i">
      <button
        class="btn m-2"
        v-bind:id="item.id"
        v-bind:class="{ 'btn-success': item.done, 'btn-secondary': !item.done }"
        v-on:click="item.done = !item.done"
      >
        {{ item.done ? "completed" : "in order" }}
      </button>
      <input type="text" :value="item.text" ref="val" />
      <button class="btn btn-primary m-2" @click="changeEdit(item.id, i)">
        Change
      </button>
      <button class="btn btn-danger" @click="removeItem(i)">Delete</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      editValue: "1231234",
    };
  },
  props: {
    list: Array,
    removeTodo: {
      type: Function,
    },
    changeEditing: {
      type: Function,
    },
  },
  methods: {
    removeItem(index) {
      this.$emit("removeTodo", index);
    },
    changeEdit(id, index) {
      console.log(this.$refs.val[index].value);
      this.$emit("changeEditing", { id, text: this.$refs.val[index].value });
    },
    editItem(text) {
      this.$emit("editTask", text);
    },
  },
};
</script>
