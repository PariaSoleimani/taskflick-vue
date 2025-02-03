<template>
  <form
    @submit.prevent="addNewNote"
    class="mb-5 w-full rounded-xl border border-zinc-200 px-3 py-2"
  >
    <div class="flex flex-col gap-2">
      <div class="flex items-center gap-2">
        <input
          class="w-full bg-transparent placeholder:text-sm placeholder:text-zinc-300 focus:outline-none md:text-lg md:placeholder:text-base"
          type="text"
          placeholder="Add Note Title"
          v-model="title"
        />
        <button class="text-md cursor-pointer text-xl font-semibold" type="submit">
          <i class="ph ph-check" :class="{hidden: !(title || description)}"></i>
        </button>
      </div>
      <textarea
        ref="textArea"
        v-model="description"
        class="w-full resize-none overflow-hidden bg-transparent text-xs text-zinc-700 placeholder:text-sm placeholder:text-zinc-300 focus:outline-none md:text-sm md:placeholder:text-base"
        placeholder="Take your note!"
        @input="autoResize"
        rows="2"
      ></textarea>
      <div v-if="title || description">
        <ul v-if="(title || description) && tags" class="flex flex-wrap items-center gap-1">
          <li><span class="mr-1 text-xs text-zinc-600 md:text-sm">Tags:</span></li>
          <task-tag
            v-for="tag in tags"
            :key="tag.id"
            :id="tag.id"
            :name="tag.name"
            :color="tag.color"
            :add-tag="addTag"
            :remove-tag="removeTag"
          ></task-tag>
        </ul>
        <ul class="mt-3 flex items-center gap-1.5" v-if="(title || description) && colors">
          <li v-for="(value, key) in colors" :key="key">
            <input
              type="radio"
              v-model="color"
              :value="key"
              class="size-5 cursor-pointer appearance-none rounded-md"
              :class="[value, color === key ? 'outline-1 outline-zinc-400' : '']"
              @click="toggleSelection(key)"
            />
          </li>
        </ul>
      </div>
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
        selectedColor: false,
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
        if (this.title || this.description) {
          this.addNote(this.title, this.description, this.color, this.noteTags);
        }
        this.title = '';
        this.description = '';
        this.color = null;
        this.noteTags = [];
      },
      toggleSelection(key) {
        this.color = this.color === key ? null : key;
      },
      autoResize() {
        const textarea = this.$refs.textArea;
        textarea.style.height = `${textarea.scrollHeight}px`;
      },
    },
  };
</script>
