<template>
  <div class="flex h-full flex-col text-zinc-800">
    <view-header>
      <template #heading>Tasks</template>
      <template #badge>{{ tasksCount }}</template>
    </view-header>
    <task-input :all-tags="tags" :all-lists="lists"></task-input>
    <div class="overflow-y-scroll pr-3">
      <ul>
        <task-item
          v-for="task in tasks"
          :key="task.id"
          :id="task.id"
          :title="task.title"
          :tags="task.tags"
          :lists="task.lists"
          :completed="task.completed"
          :all-tags="tags"
          :all-lists="lists"
        ></task-item>
      </ul>
    </div>
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
      tasksCount() {
        return this.tasks.filter(task => !task.completed).length;
      },
    },
  };
</script>
