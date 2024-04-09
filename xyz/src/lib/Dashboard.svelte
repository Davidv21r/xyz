<script>
  export let dashboard = []; // {name: string, value: string}[]
</script>

<div class="flex flex-col gap-4 md:flex-row md:items-stretch">
  {#each dashboard as { name, value }}
    <div class="flex-1 flex flex-col gap-0 border-stone-800 border bg-stone-900 p-4 rounded-xl min-w-44">
      <span class="text-xs font-semibold text-stone-500">{name}</span>
      <span class="text-lg font-semibold">{value}</span>
    </div>
  {/each}
</div>
