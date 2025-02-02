<template>
  <div class="h-full w-full text-zinc-800">
    <view-header>
      <template #heading>Sticky Notes</template>
      <template #badge>{{ noteCount }}</template>
    </view-header>
    <div class="columns-1 space-y-3 md:columns-2 md:gap-x-3 lg:columns-3 xl:columns-4">
      <sticky-note
        v-for="note in notes"
        :key="note.id"
        :id="note.id"
        :title="note.title"
        :description="note.description"
        :color="note.color"
        :tags="tags"
        :noteTags="note.tags"
      ></sticky-note>
    </div>
  </div>
</template>

<script>
  import ViewHeader from '../ui/ViewHeader.vue';
  import StickyNote from './StickyNote.vue';

  export default {
    components: {ViewHeader, StickyNote},
    props: ['notes', 'tags'],
    computed: {
      noteCount() {
        return this.notes?.length ?? 0;
      },
    },
  };
</script>
