<template>
  <div class="mx-auto flex h-screen max-w-7xl items-start gap-3 p-5">
    <side-bar @switch-component="switchComponent" :lists="lists" :tags="tags"></side-bar>
  </div>
</template>

<script>
  import SideBar from './components/SideBar.vue';

  export default {
    components: {SideBar},
    provide() {
      return {
        colors: this.colors,
      };
    },
    data() {
      return {
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
            id: 0,
            name: 'urgent',
            color: 'amber',
          },
          {
            id: 1,
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
      };
    },
    computed: {},
    methods: {},
    watch: {},
  };
</script>
