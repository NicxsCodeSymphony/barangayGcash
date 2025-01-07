<!-- AddResident.svelte -->
<script>
  export let isVisible = false;
  export let onClose;
  export let onAddResident;
</script>

{#if isVisible}
  <div class="fixed inset-0 bg-gray-500 bg-opacity-50 flex justify-center items-center z-50">
    <div class="bg-white p-6 rounded-lg shadow-lg">
      <h2 class="text-xl font-semibold">Add Resident</h2>
      <form on:submit|preventDefault={() => onAddResident()}>
        <div class="mb-4">
          <label for="name" class="block text-sm">Name</label>
          <input id="name" type="text" bind:value={name} class="mt-1 p-2 border border-gray-300 rounded w-full" required />
        </div>
        <div class="mb-4">
          <label for="age" class="block text-sm">Age</label>
          <input id="age" type="number" bind:value={age} class="mt-1 p-2 border border-gray-300 rounded w-full" required />
        </div>
        <div class="mb-4">
          <label for="email" class="block text-sm">Email</label>
          <input id="email" type="email" bind:value={email} class="mt-1 p-2 border border-gray-300 rounded w-full" required />
        </div>

        <div class="flex justify-between">
          <button type="button" on:click={onClose} class="px-4 py-2 bg-gray-500 text-white rounded">Cancel</button>
          <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded">Add</button>
        </div>
      </form>
    </div>
  </div>
{/if}