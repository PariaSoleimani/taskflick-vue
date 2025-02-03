<template>
  <section class="flex h-full flex-col">
    <view-header>
      <template #heading>Tasks</template>
      <template #badge>{{ tasksCount }}</template>
    </view-header>
    <task-input :tags="tags" :lists="lists"></task-input>
    <div class="overflow-y-auto pr-3 grow">
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
  </section>
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
