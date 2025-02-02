<template>
  <div class="h-full w-full text-zinc-800">
    <view-header>
      <template #heading>Today</template>
      <template #badge>{{ todayTasksCount }}</template>
    </view-header>
    <task-input :tags="tags" :lists="lists"></task-input>
    <ul>
      <task-item
        v-for="task in tasks"
        :key="task.id"
        :id="task.id"
        :title="task.title"
        :task-tags="task.tags"
        :task-lists="task.lists"
        :completed="task.completed"
        :tags="tags"
        :lists="lists"
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
    props: ['tasks', 'tags', 'lists'],
    computed: {
      todayTasksCount() {
        return this.tasks.filter(task => !task.completed).length;
      },
    },
  };
</script>
