<template>
  <li
    class="flex cursor-pointer items-center gap-1.5 active:scale-95 duration-200"
  >
    <span :class="colors[color]" class="size-4 md:size-5 rounded-sm"></span>
    <span class="text-sm">{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['name', 'color', 'id'],
    inject: ['colors'],
  };
</script>
