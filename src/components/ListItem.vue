<template>
  <li
    class="flex cursor-pointer items-center gap-3 rounded-md px-2 py-1 transition-all duration-200 hover:bg-zinc-200"
  >
    <div :class="colors[color]" class="size-5 rounded-sm"></div>
    <span>{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['name', 'color'],
    inject: ['colors'],
  };
</script>
