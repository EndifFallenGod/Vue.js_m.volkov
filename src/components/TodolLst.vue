<template>
  <ul class="list-group">
    <li
      class="list-group-item"
      v-for="(item, i) in list"
      :key="i"
      @dblclick="removeItem(i)"
    >
      <button
        class="btn"
        v-bind:id="item.id"
        v-bind:class="{ 'btn-success': item.done, 'btn-secondary': !item.done }"
        v-on:click="item.done = !item.done"
      >
        {{ item.done ? "completed" : "in order" }}
      </button>
      {{ item.text }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    list: Array,
    removeTodo: {
      type: Function,
      required: true
    }
  },
  methods: {
    removeItem(index) {
      this.$emit('removeTodo', index)

    }
  },
};
</script>
