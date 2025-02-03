<template>
  <div>
    <h3 class="mb-2 text-xs font-bold uppercase md:text-sm">Tags</h3>
    <ul class="flex flex-wrap items-center gap-1.5">
      <tag-item
        v-for="tag in tags"
        :key="tag.id"
        :id="tag.id"
        :name="tag.name"
        :color="tag.color"
      ></tag-item>
      <button
        class="flex cursor-pointer items-center gap-1 rounded-lg px-1.5 py-1 text-sm transition-all duration-200 active:scale-95 active:bg-zinc-300"
        type="button"
        @click="openForm = !openForm"
      >
        <i class="ph ph-plus translate-y-[1px]"></i>
        <span>add tag</span>
      </button>
      <form
        v-if="openForm"
        class="flex items-center gap-1 rounded-xl px-2 py-1.5"
        @submit.prevent="addNewTag"
      >
        <input
          type="text"
          class="border-b border-b-zinc-300 pb-0.5 focus:outline-none"
          v-model="tagName"
          placeholder="add tag name"
        />
        <div class="relative shrink-0">
          <button
            @click="dropdownOpen = !dropdownOpen"
            type="button"
            class="cursor-pointer"
          >
            <span v-if="tagColor">
              <span class="inline-block size-5 rounded-md translate-y-1" :class="colors[tagColor]"></span>
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
                tagColor = key;
                dropdownOpen = false;
              "
              class="flex cursor-pointer flex-wrap items-center gap-0.5"
            >
              <span class="size-5 rounded-md" :class="value"></span>
            </li>
          </ul>
        </div>
      </form>
    </ul>
  </div>
</template>

<script>
  import TagItem from './TagItem.vue';

  export default {
    components: {TagItem},
    props: ['tags'],
    inject: ['colors', 'addTag'],
    data() {
      return {
        openForm: false,
        tagName: '',
        tagColor: null,
        dropdownOpen: false,
      };
    },
    methods: {
      addNewTag() {
        this.addTag(this.tagName, this.tagColor);
        this.tagName = '';
        this.tagColor = null;
        this.openForm = false;
      },
    },
  };
</script>
