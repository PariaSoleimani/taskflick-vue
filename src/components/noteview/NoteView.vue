<template>
  <div class="flex h-full w-full flex-col text-zinc-800">
    <view-header>
      <template #heading>Sticky Notes</template>
      <template #badge>{{ noteCount }}</template>
    </view-header>
    <note-input :tags="tags"></note-input>

    <div
      class="mt-4 grow columns-1 space-y-3 overflow-y-auto sm:columns-2 md:gap-x-3 lg:columns-3 xl:columns-4 pr-2"
    >
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
  import NoteInput from './NoteInput.vue';
  import StickyNote from './StickyNote.vue';

  export default {
    components: {ViewHeader, StickyNote, NoteInput},
    props: ['notes', 'tags'],
    data() {
      return {
        openModal: false,
      };
    },
    computed: {
      noteCount() {
        return this.notes?.length ?? 0;
      },
    },
  };
</script>
