<template>
  <li class="rounded px-2 py-1" :class="getBgColor">
    <span>{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['name', 'color'],
    inject: ['colors'],
    computed: {
      getBgColor() {
        return this.colors[this.color];
      },
    },
  };
</script>
