<template>
  <div>
    <h3 class="mb-2 text-xs md:text-sm uppercase font-bold">Tags</h3>
    <ul class="flex flex-wrap gap-1.5 items-center">
      <tag-item v-for="tag in tags" :key="tag.id" :id="tag.id" :name="tag.name" :color="tag.color"></tag-item>
    </ul>
    <button class="mt-2 cursor-pointer text-zinc-500 duration-200 hover:text-zinc-700 flex items-center gap-1">
      <span class="text-2xl -translate-y-[1px]">+</span>
      <span>New Tag</span>
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
