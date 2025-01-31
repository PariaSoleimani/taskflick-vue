<template>
  <div class="h-full w-full text-zinc-800">
    <view-header>
      <template #heading>Today</template>
      <template #badge>2</template>
    </view-header>
    <ul class="space-y-2">
      <task-item
        v-for="task in tasks"
        :key="task.id"
        :id="task.id"
        :title="task.title"
        :task-tags="task.tags"
        :completed="task.completed"
        :tags="tags"
      ></task-item>
    </ul>
  </div>
</template>

<script>
  import ViewHeader from '../ui/ViewHeader.vue';
  import TaskItem from './TaskItem.vue';

  export default {
    components: {
      ViewHeader,
      TaskItem,
    },
    props: ['tasks', 'tags'],
   
    // data() {
    //   return {
    //     title: null,
    //     tag: [],
    //   };
    // },
    methods: {
      // addNewTask() {
      //   this.$emit('add-task', {title: this.title, tag: this.tag});
      //   this.title = '';
      // },
      
    },
  };
</script>
