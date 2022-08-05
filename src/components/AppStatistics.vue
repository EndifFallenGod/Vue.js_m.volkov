<template>
  <div class="statistics-wrapper">
    <div class="statistics-wrapper__item">
      Completed tasks {{ completedTasks }}
    </div>
    <div class="statistics-wrapper__item">All tasks {{ allTasks }}</div>
    <div class="statistics-wrapper__item">
      Percent complete tasklist {{ percent }} %
    </div>
  </div>
</template>

<script>
export default {
  name: "AppStatistics",
  props: {
    items: Array,
  },
  computed: {
    allTasks() {
      return this.items.length;
    },
    completedTasks() {
      let completed = 0;
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].done == true) {
          completed++;
        }
      }
      return completed;
    },
    percent() {
      return Math.ceil((this.completedTasks / this.allTasks) * 100);
    },
  },
};
</script>
