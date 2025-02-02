<template>
  <li
    class="item-center flex gap-1 rounded-full border border-zinc-200 px-1.5 py-0.5 text-xs text-zinc-300 transition-all duration-200"
    :class="getBgColor"
  >
    <button
      v-if="selected"
      class="translate-y-[1px] cursor-pointer"
      type="button"
      @click="unselectList(id)"
    >
      <i class="ph ph-x text-zinc-600"></i>
    </button>
    <span @click="selectList(id)" class="cursor-pointer">{{ name }}</span>
  </li>
</template>

<script>
  export default {
    props: ['id', 'name', 'color'],
    emits: ['add-list', 'remove-list'],
    inject: ['colors'],
    data() {
      return {
        selected: false,
      };
    },
    methods: {
      selectList(id) {
        this.selected = true;
        this.$emit('add-list', id);
      },
      unselectList(id) {
        this.selected = false;
        this.$emit('remove-list', id);
      },
    },
    computed: {
      getBgColor() {
        return this.selected
          ? [this.colors[this.color], 'text-zinc-700', 'border-transparent']
          : [];
      },
    },
  };
</script>
