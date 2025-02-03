<template>
  <li
    class="item-center flex gap-1 rounded-full px-1.5 py-0.5 text-xs text-zinc-300 transition-all duration-200"
    :class="changeBgColor"
  >
    <button
      v-if="selected"
      class="translate-y-[1px] cursor-pointer"
      type="button"
      @click="unselectList(id)"
    >
      <i class="ph-bold ph-x text-zinc-700"></i>
    </button>
    <span @click="selectList(id)" class="cursor-pointer">{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['id', 'name', 'color', 'addList', 'removeList'],
    inject: ['colors'],
    data() {
      return {
        selected: false,
      };
    },
    methods: {
      selectList(id) {
        this.selected = true;
        this.addList(id);
      },
      unselectList(id) {
        this.selected = false;
        this.removeList(id);
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
