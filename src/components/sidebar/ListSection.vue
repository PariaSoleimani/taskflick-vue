<template>
  <div>
    <h3 class="mb-2 text-xs font-bold uppercase md:text-sm">Lists</h3>
    <ul class="space-y-2">
      <list-item
        v-for="list in lists"
        :key="list.id"
        :id="list.id"
        :name="list.name"
        :color="list.color"
      ></list-item>
      <button
        class="flex cursor-pointer items-center gap-1 rounded-lg px-1.5 py-1 text-sm transition-all duration-200 active:scale-95 active:bg-zinc-300"
        type="button"
        @click="openForm = !openForm"
      >
        <i class="ph ph-plus translate-y-[1px]"></i>
        <span>add list</span>
      </button>
    </ul>

    <form
      v-if="openForm"
      class="flex items-center gap-1 rounded-xl px-2 py-1.5"
      @submit.prevent="addNewList"
    >
      <input
        type="text"
        class="border-b border-b-zinc-300 pb-0.5 focus:outline-none"
        v-model="listName"
        placeholder="add list name"
      />
      <div class="relative shrink-0">
        <button @click="dropdownOpen = !dropdownOpen" type="button" class="cursor-pointer">
          <span v-if="listColor">
            <span
              class="inline-block size-5 translate-y-1 rounded-md"
              :class="colors[listColor]"
            ></span>
          </span>
          <span class="flex items-center justify-center" v-else>
            <i class="ph ph-palette text-xl"></i>
          </span>
        </button>
        <ul
          v-if="dropdownOpen"
          class="absolute top-8 right-0 flex w-36 flex-wrap items-center gap-1 rounded-md bg-zinc-100 p-1 shadow-sm"
        >
          <li
            v-for="(value, key) in colors"
            :key="key"
            @click="
              listColor = key;
              dropdownOpen = false;
            "
            class="flex cursor-pointer flex-wrap items-center gap-0.5"
          >
            <span class="size-5 rounded-md" :class="value"></span>
          </li>
        </ul>
      </div>
    </form>
  </div>
</template>

<script>
  import ListItem from './ListItem.vue';

  export default {
    props: ['lists'],
    components: {ListItem},
    inject: ['colors', 'addList'],
    data() {
      return {
        openForm: false,
        listName: '',
        listColor: null,
        dropdownOpen: false,
      };
    },
    methods: {
      addNewList() {
        this.addList(this.listName, this.listColor);
        this.listName = '';
        this.listColor = null;
        this.openForm = false;
      },
    },
  };
</script>
