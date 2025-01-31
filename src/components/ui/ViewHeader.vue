<template>
  <header class="mb-5 w-full">
    <div class="flex w-fit items-center gap-2">
      <h1 class="flex items-center gap-2 font-serif text-5xl">
        <slot name="heading"></slot>
      </h1>
      <span><slot name="badge"></slot></span>
    </div>
  </header>
</template>
