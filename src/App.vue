<template>
  <div class="mx-auto flex h-dvh max-w-7xl items-start gap-5 p-5 font-sans">
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
        addNote: this.addNote,
      };
    },
    data() {
      return {
        activeComponent: 'TaskView',
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
        },
        lists: [
          {
            id: 1,
            name: 'Personal',
            color: 'amber',
          },
          {
            id: 2,
            name: 'Work',
            color: 'purple',
          },
        ],
        tags: [
          {
            id: 1,
            name: 'Urgent',
            color: 'rose',
          },
          {
            id: 2,
            name: 'Important',
            color: 'green',
          },
          {
            id: 3,
            name: 'Unfinished',
            color: 'lime',
          },
        ],
        tasks: [
          {
            id: 1,
            title: 'Research content ideas',
            completed: false,
            tags: [1, 2, 3],
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
            tags: [2],
            lists: [2],
          },
          {
            id: 4,
            title: 'Consult accountant',
            completed: false,
            tags: [1],
            lists: [1, 2],
          },
          {
            id: 5,
            title: 'Print business card',
            completed: false,
            tags: [1],
            lists: [1, 3],
          },
        ],
        notes: [
          {
            id: 1,
            title: 'Hello',
            description: 'This is the first note',
            color: 'sky',
            tags: [1, 2],
          },
          {
            id: 2,
            title: 'Adding new notes',
            description:
              'To add new notes, press the plus button on the bottom right corner of the page!',
            color: 'indigo',
            tags: [2],
          },
          // {
          //   id: 3,
          //   title: 'Adding new notes',
          //   description: 'To add new notes, press the plus button on the bottom right corner of the page!',
          //   color: 'indigo',
          //   tags: [2],
          // },
          // {
          //   id: 4,
          //   title: 'Adding new notes',
          //   description: 'To add new notes, press the plus button on the bottom right corner of the page!',
          //   color: 'indigo',
          //   tags: [2],
          // },
        ],
      };
    },
    computed: {},
    methods: {
      switchComponent(comp) {
        this.activeComponent = comp;
      },
      deleteTask(id) {
        const index = this.tasks.findIndex(task => task.id === id);
        if (index !== -1) this.tasks.splice(index, 1);
      },
      toggleCompleted(id) {
        const task = this.tasks.find(task => task.id === id);
        if (task) task.completed = !task.completed;
      },
      addTask(title, tags, lists) {
        const newTask = {id: 10, title, tags, lists, completed: false};
        this.tasks.push(newTask);
      },
      deleteNote(id) {
        const index = this.notes.findIndex(note => note.id === id);
        if (index !== -1) this.notes.splice(index, 1);
      },
      addNote(title, description, color, tags) {
        const newNote = {id: 10, title, description, color, tags};
        this.notes.push(newNote);
      },
    },
  };
</script>
