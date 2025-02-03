<template>
  <div>
    <h3 class="mb-2 text-xs md:text-sm uppercase font-bold">Lists</h3>
    <ul class="space-y-2">
      <list-item
        v-for="list in lists"
        :key="list.id"
        :id="list.id"
        :name="list.name"
        :color="list.color"
      ></list-item>
    </ul>
    <button class="mt-2 cursor-pointer text-zinc-500 duration-200 hover:text-zinc-700 flex items-center gap-1">
      <span class="text-2xl -translate-y-[1px]">+</span>
      <span>New List</span>
    </button>
  </div>
</template>

<script>
  import ListItem from './ListItem.vue';

  export default {
    props: ['lists'],
    components: {ListItem},
  };
</script>
