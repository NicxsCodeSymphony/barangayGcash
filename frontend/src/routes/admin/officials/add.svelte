<!-- Add.svelte -->
<script>
  export let isVisible = false;
  export let onClose = () => {};
  export let onAddOfficial = (official) => {};

  let name = "";
  let position = "";
  let email = "";

  const handleAddOfficial = () => {
    const newOfficial = { id: Date.now(), name, position, email };
    onAddOfficial(newOfficial);
    clearForm();
    onClose();
  };

  const clearForm = () => {
    name = "";
    position = "";
    email = "";
  };
</script>

<style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.3s ease, visibility 0.3s ease;
  }

  .modal-overlay.open {
    opacity: 1;
    visibility: visible;
  }

  .modal-content {
    background: white;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 400px;
  }

  .modal-header {
    font-size: 1.25rem;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  .input {
    width: 100%;
    padding: 0.75rem;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 8px;
  }

  .modal-footer {
    display: flex;
    justify-content: flex-end;
  }

  .btn {
    padding: 0.75rem 1.5rem;
    margin-left: 0.5rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }

  .btn-primary {
    background-color: #4CAF50;
    color: white;
  }

  .btn-secondary {
    background-color: #f44336;
    color: white;
  }
</style>

<div class={`modal-overlay ${isVisible ? 'open' : ''}`} on:click={onClose}>
  <div class="modal-content" on:click|stopPropagation>
    <div class="modal-header">Add New Official</div>
    <form on:submit|preventDefault={handleAddOfficial}>
      <input
        class="input"
        type="text"
        placeholder="Name"
        bind:value={name}
        required
      />
      <input
        class="input"
        type="text"
        placeholder="Position"
        bind:value={position}
        required
      />
      <input
        class="input"
        type="email"
        placeholder="Email"
        bind:value={email}
        required
      />
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" on:click={onClose}>Cancel</button>
        <button type="submit" class="btn btn-primary">Add Official</button>
      </div>
    </form>
  </div>
</div>