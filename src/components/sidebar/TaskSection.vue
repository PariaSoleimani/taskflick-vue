<template>
  <div class="text-zinc-800">
    <h3 class="mb-2 font-serif text-lg">Tasks</h3>
    <ul class="space-y-1">
      <li
        class="flex w-full cursor-pointer items-center gap-3 rounded-md px-2 py-1 transition-all duration-200 hover:bg-zinc-200"
        @click="switchComponent('TaskView')"
      >
        <i class="ph ph-calendar-check text-lg"></i>
        <span>Today</span>
      </li>
      <li
        class="flex cursor-pointer items-center gap-3 rounded-md px-2 py-1 transition-all duration-200 hover:bg-zinc-200"
        @click="switchComponent('NoteView')"
      >
        <i class="ph ph-note text-lg"></i>
        <span>Sticky Wall</span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    emits: ['switch-component'],
    methods: {
      switchComponent(comp) {
        this.$emit('switch-component', comp);
      },
    },
  };
</script>
