<template>
  <header class="mb-5 w-full text-zinc-800">
    <div class="flex w-fit items-center gap-2">
      <h1 class="flex items-center gap-2 font-serif text-5xl">
        <slot name="heading"></slot>
      </h1>
      <span class="size-8 text-lg -translate-y-2 flex items-center justify-center bg-zinc-400 text-white rounded-full"><slot name="badge"></slot></span>
    </div>
  </header>
</template>
