<template>
  <form
    @submit.prevent="addNewTask"
    class="mb-3 w-full rounded-xl border border-zinc-200 px-3 py-2"
  >
    <div class="flex items-center gap-2">
      <input
        class="w-full bg-transparent font-medium text-zinc-800 placeholder:text-zinc-400 focus:outline-none"
        type="text"
        placeholder="Add New Task"
        v-model="title"
      />
      <button
        :disabled="!title"
        class="text-md group cursor-pointer text-xl font-semibold text-zinc-600 transition-all duration-200 disabled:text-zinc-300"
        type="submit"
      >
        <i class="ph ph-check group-disabled:hidden"></i>
      </button>
    </div>

    <ul v-show="title && allTags" class="mt-2 flex flex-wrap items-center gap-1">
      <li><p class="mr-1 text-xs text-zinc-500">Tags:</p></li>
      <task-tag
        v-for="tag in allTags"
        :key="tag.id"
        :name="tag.name"
        :color="tag.color"
        :id="tag.id"
        @add-tag="addTag"
        @remove-tag="removeTag"
      ></task-tag>
    </ul>

    <ul v-show="title && allLists" class="mt-2 flex flex-wrap items-center gap-1">
      <li><p class="mr-1 text-xs text-zinc-500">Lists:</p></li>
      <task-list
        v-for="list in allLists"
        :key="list.id"
        :name="list.name"
        :color="list.color"
        :id="list.id"
        @add-list="addList"
        @remove-list="removeList"
      ></task-list>
    </ul>
  </form>
</template>

<script>
  import TaskList from './TaskList.vue';
  import TaskTag from './TaskTag.vue';

  export default {
    components: {TaskTag, TaskList},
    props: ['allTags', 'allLists'],
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
