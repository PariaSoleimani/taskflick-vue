<template>
  <aside class="h-full w-64 rounded-lg bg-zinc-100 p-5">
    <h1 class="mb-5 font-serif text-3xl">NoteFlick</h1>
    <nav class="flex flex-col gap-5">
      <form class="flex w-full items-center gap-1 rounded-lg bg-zinc-200 px-1.5 py-1">
        <input
          type="text"
          placeholder="Search"
          class="w-full text-zinc-800 placeholder:text-zinc-400 focus:outline-none"
        />
        <button class="flex cursor-pointer items-center justify-center" type="submit">
          <i class="ph ph-magnifying-glass text-lg text-zinc-400"></i>
        </button>
      </form>
      <task-section @switch-component="$emit('switch-component', comp)"></task-section>
    </nav>
  </aside>
</template>

<script>
  import TaskSection from './TaskSection.vue';
  export default {
    components: {TaskSection},
    emits: ['switch-component'],
  };
</script>
