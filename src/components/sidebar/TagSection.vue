<template>
  <div class="text-zinc-800">
    <h3 class="mb-3 text-lg">Tags</h3>
    <ul class="flex flex-wrap gap-2">
      <tag-item v-for="tag in tags" :key="tag.id" :id="tag.id" :name="tag.name" :color="tag.color"></tag-item>
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
