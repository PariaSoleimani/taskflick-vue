<template>
  <div class="flex h-full flex-col text-zinc-800">
    <view-header>
      <template #heading>Results</template>
      <template #badge>{{ resultsCount }}</template>
    </view-header>
    <div class="w-full grow flex justify-center items-center" v-if="filteredNotes.length === 0 && filteredTasks.length === 0"><p>No results!</p></div>
    <div v-else>
      <h3 class="mb-4 text-2xl">Tasks</h3>
      <ul>
        <task-item
          v-for="task in filteredTasks"
          :key="task.id"
          :id="task.id"
          :title="task.title"
          :completed="task.completed"
          :tags="task.tags"
          :lists="task.lists"
          :all-tags="tags"
          :all-lists="lists"
          @click="$emit('switch-component', 'TaskView')"
        ></task-item>
      </ul>
    </div>
    <div v-else>
      <h3 class="my-4 text-2xl">Notes</h3>
      <ul>
        <sticky-note
          v-for="note in filteredNotes"
          :key="note.id"
          :id="note.id"
          :title="note.title"
          :description="note.description"
          :color="note.color"
          :note-tags="note.tags"
          :tags="tags"
          @click="$emit('switch-component', 'NoteView')"
        ></sticky-note>
      </ul>
    </div>
  </div>
</template>

<script>
  import StickyNote from '../noteview/StickyNote.vue';
  import TaskItem from '../taskview/TaskItem.vue';
  import ViewHeader from '../ui/ViewHeader.vue';

  export default {
    components: {ViewHeader, TaskItem, StickyNote},
    props: ['filteredNotes', 'filteredTasks', 'tags', 'lists'],
    emits: ['switch-component'],
    data() {
      return {};
    },
    computed: {
      resultsCount() {
        const count = this.filteredNotes?.length + this.filteredTasks?.length ?? 0;
        return count;
      },
    },
  };
</script>
