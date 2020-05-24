<template>
  <div class="flex flex-col w-full h-screen bg-white">
    <div class="bg-primaryBlue h-32">
      <div class="text-white pl-4 mt-8">
        <h1 class="font-bold text-3xl">Task App</h1>
      </div>
    </div>
    <div class="flex-1">
      <div class="bg-primaryBlue rounded-br-full">
        <h3 class="text-white pl-4 text-lg py-4">My task</h3>
      </div>
      <div class="">
        <ul class="flex ">
          <li class="-mb-px mr-1" v-for="tab in tabs" v-bind:key="tab.id">
            <a
              class="inline-block text-gray-500 rounded-t py-2 px-4"
              v-bind:class="{
                'text-primaryBlue': tab.active,
              }"
              v-on:click="tabChanged(tab.id)"
              >{{ tab.title }}</a
            >
          </li>
        </ul>
      </div>
      <TabContent :listOfTasks="getTabData()"></TabContent>
    </div>
    <div class="pb-4">
      <div class="text-gray-700 text-center ">
        <button
          class="bg-primaryBlue hover:bg-primaryBlue text-white text-3xl rounded-full w-16 h-16 hover:text-white py-2 px-4 border border-blue-500 hover:border-primaryBlue rounded"
          v-on:click="addTask()"
        >
          +
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import TabContent from '../components/TabContent.vue';
export default {
  name: 'Home',
  components: {
    TabContent,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      tabs: [
        {
          id: 0,
          title: 'Active',
          active: true,
        },
        {
          id: 1,
          title: 'Completed',
          active: false,
        },
      ],
      tasks: [
        {
          id: 1,
          title: 'First task',
          completed: false,
        },
        {
          id: 2,
          title: 'Second task',
          completed: true,
        },
        {
          id: 3,
          title: 'Third task',
          completed: false,
        },
      ],
    };
  },
  methods: {
    addTask() {
      console.log('added!!!');
    },
    tabChanged(index) {
      this.tabs.forEach((element) => (element.active = false));
      this.tabs[index].active = !this.tabs[index].active;
      this.$emit('tabChanged', this.getTabData(index));
    },
    getActive() {
      var parsedArray = JSON.parse(JSON.stringify(this.tasks));
      return parsedArray.filter((element) => !element.completed);
    },
    getCompleted() {
      var parsedArray = JSON.parse(JSON.stringify(this.tasks));
      return parsedArray.filter((element) => element.completed);
    },
    getTabData(index = 0) {
      return index === 0 ? this.getActive() : this.getCompleted();
    },
  },
};
</script>
<style scoped></style>
