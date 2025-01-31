<template>
  <div class="h-full w-full text-zinc-800">
    <view-header>
      <template #heading>Today</template>
      <template #badge>{{ todayTasksNum }}</template>
    </view-header>
    <ul>
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
  import TaskInput from './TaskInput.vue';
  import TaskItem from './TaskItem.vue';

  export default {
    components: {
      ViewHeader,
      TaskItem,
      TaskInput,
    },
    props: ['tasks', 'tags'],
    computed: {
      todayTasksNum() {
        return this.tasks.filter(task => !task.completed).length;
      },
    },
    methods: {
    },
  };
</script>
