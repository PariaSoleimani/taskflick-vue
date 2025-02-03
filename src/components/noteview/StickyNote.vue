<template>
  <div
    :class="colors[color]"
    class="group relative h-fit max-w-full break-inside-avoid rounded-xl p-3 md:max-w-96"
  >
    <button
      @click="deleteNote(id)"
      class="absolute top-4 right-4 hidden cursor-pointer group-hover:block"
    >
      <i class="ph-bold ph-x"></i>
    </button>
    <h4 class="mb-2 text-lg font-semibold">{{ title }}</h4>
    <p class="text-sm">{{ description }}</p>
    <ul class="mt-3 flex flex-wrap items-center gap-1" v-if="noteTags.length">
      <li
        class="rounded-full px-1.5 py-0.5 text-xs text-zinc-700"
        v-for="tag in mappedTags"
        :key="tag.id"
        :class="colors[tag.color]"
      >
        {{ tag.name }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: ['id', 'title', 'description', 'color', 'tags', 'noteTags'],
    inject: ['deleteNote', 'colors'],
    computed: {
      mappedTags() {
        return this.noteTags.map(tagId => this.tags.find(tag => tag.id === tagId));
      },
    },
  };
</script>
