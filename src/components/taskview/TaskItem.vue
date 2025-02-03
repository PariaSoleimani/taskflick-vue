<template>
  <li
    class="group flex flex-col gap-2 border-b border-zinc-200 p-3 transition-all duration-200 hover:bg-zinc-100"
  >
    <div class="flex items-center justify-between">
      <label class="flex w-full items-center gap-2">
        <input
          type="checkbox"
          @change="toggleCompleted(id)"
          class="size-3 accent-zinc-500 md:size-4"
        />
        <p :class="{'line-through opacity-50': completed}" class="md:text-lg">
          {{ title }}
        </p>
      </label>
      <button
        class="hidden cursor-pointer items-center justify-center text-zinc-700 group-hover:flex"
        @click="deleteTask(id)"
      >
        <i class="ph-bold ph-x"></i>
      </button>
    </div>
    <div class="flex items-center gap-1.5">
      <ul
        class="flex flex-wrap gap-1.5"
        v-if="mappedTags.length"
        :class="{'opacity-50': completed}"
      >
        <li
          class="rounded-full px-1.5 py-0.5 text-xs"
          v-for="tag in mappedTags"
          :key="tag.id"
          :class="colors[tag.color]"
        >
          {{ tag.name }}
        </li>
      </ul>
      <div
        v-if="mappedLists.length > 0 && mappedTags.length > 0"
        class="h-4 w-[1px] bg-zinc-200"
      ></div>
      <ul class="flex flex-wrap gap-2" v-if="mappedLists.length" :class="{'opacity-50': completed}">
        <li class="flex items-center gap-1 text-xs" v-for="list in mappedLists" :key="list.id">
          <span class="size-4 rounded-md" :class="colors[list.color]"></span>
          <span>{{ list.name }}</span>
        </li>
      </ul>
    </div>
  </li>
</template>

<script>
  export default {
    props: ['id', 'title', 'taskTags', 'taskLists', 'tags', 'completed', 'lists'],
    inject: ['deleteTask', 'colors', 'toggleCompleted'],
    computed: {
      mappedTags() {
        if (!this.taskTags || !this.tags) return [];
        return this.taskTags
          .map(tagId => this.tags.find(tag => tag.id === tagId))
          .filter(tag => tag);
      },
      mappedLists() {
        if (!this.taskLists || !this.lists) return [];
        return this.taskLists
          .map(listId => this.lists.find(list => list.id === listId))
          .filter(list => list);
      },
    },
  };
</script>
