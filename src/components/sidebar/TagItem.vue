<template>
  <li
    class="cursor-pointer rounded-lg px-2 py-1 transition-all duration-200 active:scale-95"
    :class="colors[color]"
  >
    {{ name }}
  </li>
</template>

<script>
  export default {
    props: ['name', 'color', 'id'],
    inject: ['colors'],
  };
</script>
