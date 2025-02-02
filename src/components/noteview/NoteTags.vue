<template>
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
</template>

<script>
  export default {
    props: ['noteTags', 'tags'],
    inject: ['colors'],
    computed: {
      mappedTags() {
        return this.noteTags.map(tagId => this.tags.find(tag => tag.id === tagId));
      },
    },
  };
</script>
