<template>
  <section class="flex h-full flex-col gap-3">
    <view-header>
      <template #heading>Results</template>
      <template #badge>{{ resultsCount }}</template>
    </view-header>
    <div
      class="flex h-full w-full items-center justify-center"
      v-if="filteredNotes.length === 0 && filteredTasks.length === 0"
    >
      <img class="max-w-72 brightness-105 contrast-90 grayscale" src="/no-results.png" alt="" />
    </div>
    <div class="space-y-3 overflow-y-auto">
      <div v-if="filteredTasks.length !== 0">
        <h3 class="mb-2 text-xl font-semibold md:text-2xl">Tasks</h3>
        <ul>
          <task-item
            v-for="task in filteredTasks"
            :key="task.id"
            :id="task.id"
            :title="task.title"
            :completed="task.completed"
            :taskTags="task.tags"
            :taskLists="task.lists"
            :tags="tags"
            :lists="lists"
          ></task-item>
        </ul>
      </div>
      <div v-if="filteredNotes.length !== 0">
        <h3 class="mb-2 text-xl font-semibold md:text-2xl">Notes</h3>
        <ul class="columns-1 space-y-3 sm:columns-2 md:gap-x-3 lg:columns-3 xl:columns-4">
          <sticky-note
            v-for="note in filteredNotes"
            :key="note.id"
            :id="note.id"
            :title="note.title"
            :description="note.description"
            :color="note.color"
            :note-tags="note.tags"
            :tags="tags"
          ></sticky-note>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
  import StickyNote from '../noteview/StickyNote.vue';
  import TaskItem from '../taskview/TaskItem.vue';
  import ViewHeader from '../ui/ViewHeader.vue';

  export default {
    components: {ViewHeader, TaskItem, StickyNote},
    props: ['notes', 'tasks', 'tags', 'lists', 'searchQuery'],
    computed: {
      resultsCount() {
        const count = this.filteredNotes?.length + this.filteredTasks?.length ?? 0;
        return count;
      },
      filteredTasks() {
        return this.tasks?.filter(task =>
          task.title.toLowerCase().includes(this.searchQuery.toLowerCase()),
        );
      },
      filteredNotes() {
        return this.notes?.filter(
          note =>
            note.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
            note.description.toLowerCase().includes(this.searchQuery.toLowerCase()),
        );
      },
    },
  };
</script>
