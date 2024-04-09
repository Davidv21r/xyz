<script>
  const footer = [{ name: "Github", link: "https://github.com/Davidv21r/xyz" }];
</script>

<footer class="flex justify-center p-6">
  {#each footer as { name, link }}
    <a
      class="hover:bg-stone-900/30 text-stone-400 hover:text-stone-100 transition-all px-4 py-2 rounded-full"
      href={link}>{name}</a
    >
  {/each}
</footer>
