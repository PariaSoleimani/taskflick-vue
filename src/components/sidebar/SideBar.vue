<template>
  <aside
    class="absolute z-10 h-full w-64 shrink-0 rounded-tr-2xl rounded-bl-2xl bg-zinc-100 p-5 transition-transform duration-300 md:relative md:translate-x-0 md:rounded-2xl"
    :class="[openSidebar ? 'translate-x-0' : '-translate-x-full']"
  >
    <div
      class="absolute top-1/2 -right-3 h-72 w-4 -translate-y-1/2 cursor-pointer rounded-tr-2xl rounded-br-2xl bg-zinc-100 md:hidden"
      @click="showSidebar"
      @touchmove="showSidebar"
    ></div>
    <h1 class="mb-5 font-serif text-2xl md:text-3xl">NoteFlick</h1>
    <nav class="flex flex-col gap-5">
      <form
        class="flex w-full items-center gap-1 rounded-xl bg-zinc-50 px-2 py-1.5"
        @submit.prevent="submitForm"
      >
        <input
          type="text"
          placeholder="Search"
          class="w-full placeholder:text-sm placeholder:text-zinc-300 focus:outline-none md:text-lg md:placeholder:text-base"
          v-model="searchQuery"
        />
        <button class="group text-md cursor-pointer md:text-xl font-semibold" type="submit">
          <i
            class="ph ph-magnifying-glass text-zinc-400 transition-all duration-300"
            :class="{'text-zinc-800': searchQuery}"
          ></i>
        </button>
      </form>
      <ul class="space-y-2">
        <li
          class="flex cursor-pointer items-center gap-1.5 transition-all duration-200"
          @click="$emit('switch-component', 'TaskView')"
        >
          <i class="ph ph-calendar-check text-2xl"></i>
          <span>Tasks</span>
        </li>
        <li
          class="flex cursor-pointer items-center gap-1.5 transition-all duration-200"
          @click="$emit('switch-component', 'NoteView')"
        >
          <i class="ph ph-note text-2xl"></i>
          <span>Notes</span>
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
    emits: ['switch-component', 'show-sidebar', 'search-request'],
    data() {
      return {
        openSidebar: false,
        searchQuery: null,
      };
    },
    methods: {
      showSidebar() {
        this.openSidebar = !this.openSidebar;
        this.$emit('show-sidebar', this.openSidebar);
      },
      submitForm() {
        this.$emit('search-request', this.searchQuery);
        this.$emit('switch-component', 'SearchView');
      },
    },
  };
</script>
