<template>
  <form
    @submit.prevent="addNewTask"
    class="mb-5 w-full rounded-xl border border-zinc-200 px-3 py-2"
  >
    <div class="flex items-center gap-2">
      <input
        class="w-full bg-transparent placeholder:text-sm placeholder:text-zinc-300 focus:outline-none md:text-lg md:placeholder:text-base"
        type="text"
        placeholder="Add New Task"
        v-model="title"
      />
      <button class="text-md cursor-pointer text-xl font-semibold" type="submit">
        <i class="ph ph-check" :class="{hidden: !title}"></i>
      </button>
    </div>
    <ul v-if="title && tags" class="mt-2 flex flex-wrap items-center gap-1">
      <li><p class="mr-1 text-xs text-zinc-600 md:text-sm">Tags:</p></li>
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
    <ul v-if="title && lists" class="mt-2 flex flex-wrap items-center gap-1">
      <li><p class="mr-1 text-xs text-zinc-600 md:text-sm">Lists:</p></li>
      <task-list
        v-for="list in lists"
        :key="list.id"
        :name="list.name"
        :color="list.color"
        :id="list.id"
        :add-list="addList"
        :remove-list="removeList"
      ></task-list>
    </ul>
  </form>
</template>

<script>
  import TaskList from './TaskList.vue';
  import TaskTag from './TaskTag.vue';

  export default {
    components: {TaskTag, TaskList},
    props: ['tags', 'lists'],
    inject: ['addTask'],
    data() {
      return {
        title: null,
        taskTags: [],
        taskLists: [],
      };
    },
    methods: {
      addNewTask() {
        this.addTask(this.title, this.taskTags, this.taskLists);
        this.title = null;
        this.taskTags = [];
        this.taskList = [];
        console.log(this.taskTags);
        console.log(this.taskLists);
      },
      addTag(id) {
        this.taskTags.push(id);
      },
      removeTag(id) {
        const index = this.taskTags.indexOf(id);
        if (index !== -1) {
          this.taskTags.splice(index, 1);
        }
      },
      addList(id) {
        this.taskLists.push(id);
      },
      removeList(id) {
        const index = this.taskLists.indexOf(id);
        if (index !== -1) {
          this.taskLists.splice(index, 1);
        }
      },
    },
  };
</script>
