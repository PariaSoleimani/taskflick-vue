<template>
  <div
    :class="colors[color]"
    class="group relative h-fit max-w-full md:max-w-96 min-w-52 break-inside-avoid rounded-lg p-4 text-zinc-800"
  >
    <button
      @click="deleteNote(id)"
      class="absolute top-4 right-4 hidden cursor-pointer text-zinc-600 group-hover:block"
    >
      <i class="ph-bold ph-x"></i>
    </button>
    <h4 class="mt-3 mb-2 text-xl font-semibold">{{ title }}</h4>
    <p class="text-base leading-6">{{ description }}</p>
    <note-tags :tags="tags" :noteTags="noteTags"></note-tags>
  </div>
</template>

<script>
  import NoteTags from './NoteTags.vue';

  export default {
    components: {NoteTags},
    props: ['id', 'title', 'description', 'color', 'tags', 'noteTags'],
    inject: ['deleteNote', 'colors'],
  };
</script>
