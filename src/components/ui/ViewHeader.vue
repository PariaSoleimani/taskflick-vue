<template>
  <header class="w-ful mb-5">
    <div class="flex w-fit items-center gap-1">
      <h1 class="font-serif text-4xl md:text-5xl">
        <slot name="heading"></slot>
      </h1>
      <span
        class="flex size-6 -translate-y-2 items-center justify-center rounded-full bg-zinc-300 text-sm text-white md:size-7 md:text-base"
      >
        <slot name="badge"></slot>
      </span>
    </div>
  </header>
</template>
