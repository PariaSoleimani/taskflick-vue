<template>
  <li
    class="flex cursor-pointer items-center gap-3 rounded-lg px-2 py-1 transition-all duration-200 hover:bg-zinc-200 active:scale-95"
  >
    <span :class="colors[color]" class="size-5 rounded-sm"></span>
    <span>{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['name', 'color', 'id'],
    inject: ['colors'],
  };
</script>
