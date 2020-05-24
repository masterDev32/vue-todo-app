<template>
  <div v-on:tabChanged="tabChanged($event)">
    <div v-for="task in tasks" v-bind:key="task.id" class="">
      <div class="shadow-md h-12 mx-4 my-2 border-gray-100">
        <p
          class="text-gray-600 rounded-t py-2 px-4"
          v-bind:class="{
            'text-primaryBlue': task.completed,
          }"
        >
          {{ task.title }}
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'TabContent',
  props: {
    listOfTasks: { default: [] },
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    tabChanged(newValue) {
      this.tasks = newValue;
    },
  },
  mounted() {
    this.tasks = this.listOfTasks;
  },
  created() {
    this.$parent.$on('tabChanged', this.tabChanged);
  },
};
</script>
