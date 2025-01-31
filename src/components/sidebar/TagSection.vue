<template>
  <div class="text-zinc-800">
    <h2 class="mb-2 font-serif text-lg">Tags</h2>
    <ul class="flex flex-wrap gap-2">
      <tag-item v-for="tag in tags" :key="tag.id" :name="tag.name" :color="tag.color"></tag-item>
    </ul>
    <button class="mt-3 cursor-pointer text-blue-400 duration-200 hover:text-blue-500">
      <span class="mr-1 text-xl">+</span>
      <span>Add Tag</span>
    </button>
  </div>
</template>

<script>
  import TagItem from './TagItem.vue';
  export default {
    components: {TagItem},
    props: ['tags'],
  };
</script>
