<template>
  <div class="mx-auto flex h-screen max-w-7xl items-start gap-5 p-5">
    <side-bar @switch-component="switchComponent" :lists="lists" :tags="tags"></side-bar>
    <main class="h-full grow p-5">
      <component
        :is="activeComponent"
        :tasks="tasks"
        :tags="tags"
        :lists="lists"
        :notes="notes"
      ></component>
    </main>
  </div>
</template>

<script>
  import SideBar from './components/sidebar/SideBar.vue';
  import TaskView from './components/taskview/TaskView.vue';
  import NoteView from './components/noteview/NoteView.vue';

  export default {
    components: {SideBar, TaskView, NoteView},
    provide() {
      return {
        colors: this.colors,
        deleteTask: this.deleteTask,
        toggleCompleted: this.toggleCompleted,
        addTask: this.addTask,
        deleteNote: this.deleteNote,
      };
    },
    data() {
      return {
        activeComponent: 'task-view',
        colors: {
          sky: 'bg-sky-200',
          red: 'bg-red-200',
          green: 'bg-green-200',
          amber: 'bg-amber-200',
          gray: 'bg-gray-200',
          purple: 'bg-purple-200',
          rose: 'bg-rose-200',
          pink: 'bg-pink-200',
          lime: 'bg-lime-200',
          orange: 'bg-orange-200',
          indigo: 'bg-indigo-200',
          purple: 'bg-purple-200',
        },
        lists: [
          {
            id: 1,
            name: 'Personal',
            color: 'sky',
          },
          {
            id: 2,
            name: 'Work',
            color: 'pink',
          },
        ],
        tags: [
          {
            id: 1,
            name: 'urgent',
            color: 'amber',
          },
          {
            id: 2,
            name: 'important',
            color: 'green',
          },
          {
            id: 3,
            name: 'family',
            color: 'sky',
          },
          {
            id: 4,
            name: 'school',
            color: 'lime',
          },
          {
            id: 5,
            name: 'entertainment',
            color: 'indigo',
          },
        ],
        tasks: [
          {
            id: 1,
            title: 'Research content ideas',
            completed: false,
            tags: [1, 2, 3, 4, 5],
            lists: [1],
          },
          {
            id: 2,
            title: 'Create a database of guest authors',
            completed: false,
            tags: [3],
            lists: [1],
          },
          {
            id: 3,
            title: "Renew driver's license",
            completed: false,
            tags: [],
            lists: [2],
          },
          {
            id: 4,
            title: 'Consult accountant',
            completed: false,
            tags: [5],
            lists: [1, 2],
          },
          {
            id: 5,
            title: 'Print business card',
            completed: false,
            tags: [1],
            lists: [1, 2],
          },
        ],
        notes: [
          {
            id: 1,
            title: 'Hello',
            description: 'This is the first note',
            color: 'rose',
            tags: [1, 2],
          },
        ],
      };
    },
    computed: {},
    methods: {
      switchComponent(comp) {
        this.activeComponent = comp;
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      },
      toggleCompleted(id) {
        const selectedTask = this.tasks.find(task => task.id === id);
        selectedTask.completed = !selectedTask.completed;
      },
      addTask(title, tags, lists) {
        const newTask = {id: 10, title: title, tags: tags, lists: lists, completed: false};
        this.tasks.push(newTask);
      },
      deleteNote(id) {
        this.notes = this.notes.filter(note => note.id !== id);
      },
    },
    watch: {},
  };
</script>
