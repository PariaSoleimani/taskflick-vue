<template>
  <aside class="flex h-full w-64 flex-col gap-5 rounded-lg bg-zinc-100 p-5">
    <h1 class="font-serif text-3xl">NoteFlick</h1>
    <nav>
      <form class="flex w-full items-center gap-1 rounded-lg bg-zinc-200 px-1.5 py-1">
        <input
          type="text"
          placeholder="Search"
          class="w-full text-zinc-800 placeholder:text-zinc-400 focus:outline-none"
        />
        <button class="flex cursor-pointer items-center justify-center" type="submit">
          <i class="ph ph-magnifying-glass text-lg text-zinc-400"></i>
        </button>
      </form>
    </nav>
  </aside>
</template>

<script></script>
