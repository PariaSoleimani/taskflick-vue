<template>
  <li class="group flex flex-col rounded-sm p-3 transition-all duration-200 hover:bg-zinc-200">
    <div class="flex items-center justify-between">
      <label class="flex w-full items-center gap-2">
        <input
          type="checkbox"
          @change="toggleCompleted(id)"
          class="size-4 accent-zinc-500"
        />
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
    <div class="mt-2 w-full" v-if="taskTags.length" :class="{'opacity-50': completed}">
      <ul class="flex flex-wrap gap-1">
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
  </li>
</template>

<script>
  export default {
    props: ['id', 'title', 'taskTags', 'tags', 'completed'],
    inject: ['deleteTask', 'colors', 'toggleCompleted'],
    computed: {
      mappedTags() {
        return this.taskTags.map(tagId => this.tags.find(tag => tag.id === tagId));
      },
    },
  };
</script>
