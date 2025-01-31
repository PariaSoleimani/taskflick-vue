<template>
  <div class="mx-auto flex h-screen max-w-7xl items-start gap-3 p-5">
    <side-bar @switch-component="switchComponent"></side-bar>
  </div>
</template>

<script>
  import SideBar from './components/SideBar.vue';

  export default {
    components: {SideBar},
    data() {
      return {};
    },
    computed: {},
    methods: {},
    watch: {},
  };
</script>
