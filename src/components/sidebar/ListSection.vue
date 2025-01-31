<template>
  <div class="text-zinc-800">
    <h3 class="mb-2 font-serif text-lg">Lists</h3>
    <ul class="space-y-1">
      <list-item
        v-for="list in lists"
        :key="list.id"
        :name="list.name"
        :color="list.color"
      ></list-item>
    </ul>
    <button class="mt-3 cursor-pointer text-blue-400 duration-200 hover:text-blue-500">
      <span class="mr-1 text-xl">+</span>
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
