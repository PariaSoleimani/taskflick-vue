<template>
  <li class="group flex flex-col p-3 transition-all duration-200 hover:bg-zinc-100 border-b border-zinc-200">
    <div class="flex items-center justify-between">
      <label class="flex w-full items-center gap-2">
        <input type="checkbox" @change="toggleCompleted(id)" class="size-4 accent-zinc-500" />
        <p :class="{'line-through opacity-50': completed}" class="text-lg font-light">
          {{ title }}
        </p>
      </label>
      <button
        class="text mt-1 ml-auto hidden cursor-pointer items-center justify-center text-sm text-zinc-500 group-hover:flex"
        @click="deleteTask(id)"
      >
        <i class="ph-bold ph-x text-lg"></i>
      </button>
    </div>
    <div class="mt-2 w-full" v-if="mappedTags.length" :class="{'opacity-50': completed}">
      <ul class="flex flex-wrap gap-1.5">
        <li
          class="rounded px-2 py-1 text-xs"
          v-for="tag in mappedTags"
          :key="tag.id"
          :class="colors[tag.color]"
        >
          {{ tag.name }}
        </li>
      </ul>
    </div>
    <div class="mt-3 w-full" v-if="mappedLists.length" :class="{'opacity-50': completed}">
      <ul class="flex flex-wrap gap-3">
        <li
          class="flex items-center gap-1 rounded text-xs"
          v-for="list in mappedLists"
          :key="list.id"
        >
          <span class="block size-4 rounded-sm" :class="colors[list.color]"></span>
          <span>{{ list.name }}</span>
        </li>
      </ul>
    </div>
  </li>
</template>

<script>
  export default {
    props: ['id', 'title', 'tags', 'lists', 'allTags', 'completed', 'allLists'],
    inject: ['deleteTask', 'colors', 'toggleCompleted'],
    computed: {
      mappedTags() {
        if (!this.tags || !this.allTags) return [];
        return this.tags
          .map(tagId => this.allTags.find(tag => tag.id === tagId))
          .filter(tag => tag);
      },
      mappedLists() {
        if (!this.lists || !this.allLists) return [];
        return this.lists
          .map(listId => this.allLists.find(list => list.id === listId))
          .filter(list => list);
      },
    },
  };
</script>
