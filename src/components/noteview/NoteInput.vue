<template>
  <form
    @submit.prevent="addNewNote"
    class="mb-3 w-full overflow-clip rounded-xl border border-zinc-200"
  >
    <div class="flex w-full flex-col items-start gap-2 px-3 pt-2" :class="applyColor">
      <div class="flex w-full items-start gap-2">
        <input
          class="w-full grow bg-transparent font-medium text-zinc-800 placeholder:text-zinc-400 focus:outline-none"
          type="text"
          placeholder="Add note title"
          v-model="title"
        />
        <button
          :disabled="!title"
          class="text-md group cursor-pointer text-xl font-semibold text-zinc-600 transition-all duration-200 disabled:text-zinc-300"
          type="submit"
          aria-label="Save note"
        >
          <i class="ph ph-check group-disabled:hidden"></i>
        </button>
      </div>
      <textarea
        v-model="description"
        class="w-full resize-none overflow-hidden bg-transparent text-sm text-zinc-700 placeholder:text-zinc-400 focus:outline-none"
        placeholder="Take your note!"
      ></textarea>
    </div>
    <div class="px-3 py-2" v-if="title">
      <ul v-show="title && tags" class="mt-2 flex flex-wrap items-center gap-1">
        <li><p class="mr-1 text-xs text-zinc-500">Tags:</p></li>
        <task-tag
          v-for="tag in tags"
          :key="tag.id"
          :name="tag.name"
          :color="tag.color"
          :id="tag.id"
          @add-tag="addTag"
          @remove-tag="removeTag"
        ></task-tag>
      </ul>
      <ul class="mt-3 flex items-center gap-1.5" v-show="title && colors">
        <li
          class="size-5 cursor-pointer rounded-md"
          v-for="(value, key) in colors"
          :key="key"
          :class="value"
          @click="selectColor(key)"
        ></li>
      </ul>
    </div>
  </form>
</template>

<script>
  import TaskTag from '../taskview/TaskTag.vue';

  export default {
    components: {TaskTag},
    props: ['tags'],
    inject: ['addNote', 'colors'],
    data() {
      return {
        title: '',
        description: '',
        color: null,
        noteTags: [],
      };
    },
    methods: {
      addTag(id) {
        this.noteTags.push(id);
      },
      removeTag(id) {
        const index = this.noteTags.indexOf(id);
        if (index !== -1) {
          this.noteTags.splice(index, 1);
        }
      },
      addNewNote() {
        if (!this.color) {
          this.addNote(this.title, this.description, 'gray', this.noteTags);
        } else {
          this.addNote(this.title, this.description, this.color, this.noteTags);
        }

        this.title = '';
        this.description = '';
        this.color = null;
        this.noteTags = [];
      },
      selectColor(key) {
        this.color = key;
      },
    },
    computed: {
      applyColor() {
        return this.colors[this.color];
      },
    },
  };
</script>
