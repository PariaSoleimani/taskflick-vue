<template>
  <li
    class="item-center flex gap-1 rounded-full px-1.5 py-0.5 text-xs text-zinc-300 transition-all duration-200"
    :class="changeBgColor"
  >
    <button
      v-if="selected"
      class="translate-y-[1px] cursor-pointer"
      type="button"
      @click="unselectTag(id)"
    >
      <i class="ph-bold ph-x text-zinc-700"></i>
    </button>
    <span @click="selectTag(id)" class="cursor-pointer">{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['id', 'name', 'color', 'addTag', 'removeTag'],
    inject: ['colors'],
    data() {
      return {
        selected: false,
      };
    },
    methods: {
      selectTag(id) {
        this.selected = true;
        this.addTag(id);
      },
      unselectTag(id) {
        this.selected = false;
        this.removeTag(id);
      },
    },
    computed: {
      changeBgColor() {
        return this.selected
          ? [this.colors[this.color], 'text-zinc-700', 'border', 'border-transparent']
          : ['border', 'border-zinc-200'];
      },
    },
  };
</script>
