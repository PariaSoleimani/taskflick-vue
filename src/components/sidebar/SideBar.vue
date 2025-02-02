<template>
  <aside
    class="absolute z-10 h-full w-64 shrink-0 rounded-tr-2xl rounded-bl-2xl bg-zinc-100 p-5 transition-transform duration-300 md:relative md:translate-x-0 md:rounded-2xl"
    :class="[openSidebar ? 'translate-x-0' : '-translate-x-full']"
  >
    <div class="absolute w-3 h-56 rounded-tr-2xl rounded-br-2xl bg-zinc-100 top-1/2 -translate-y-1/2 -right-3 cursor-pointer md:hidden" @click="showSidebar" @touchmove="showSidebar">

    </div>
    <h1 class="mb-5 text-3xl">NoteFlick</h1>
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

      <ul class="space-y-1">
        <li
          class="flex w-full cursor-pointer items-center gap-3 rounded-md px-2 py-1 transition-all duration-200 hover:bg-zinc-200"
          @click="$emit('switch-component', 'TaskView')"
        >
          <i class="ph ph-calendar-check text-2xl"></i>
          <span>Tasks</span>
        </li>
        <li
          class="flex cursor-pointer items-center gap-3 rounded-md px-2 py-1 transition-all duration-200 hover:bg-zinc-200"
          @click="$emit('switch-component', 'NoteView')"
        >
          <i class="ph ph-note text-2xl"></i>
          <span>Sticky Notes</span>
        </li>
      </ul>
      <list-section :lists="lists"></list-section>
      <tag-section :tags="tags"></tag-section>
    </nav>
  </aside>
</template>

<script>
  import ListSection from './ListSection.vue';
  import TagSection from './TagSection.vue';

  export default {
    components: {ListSection, TagSection},
    props: ['lists', 'tags'],
    emits: ['switch-component', 'show-sidebar'],
    data() {
      return {
        openSidebar: false,
      };
    },
    methods: {
      showSidebar() {
        this.openSidebar = !this.openSidebar;
        this.$emit('show-sidebar', this.openSidebar);
      },
    },
  };
</script>
