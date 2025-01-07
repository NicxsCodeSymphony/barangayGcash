<script>
  import Sidebar from "../sidebar.svelte";
  import { onMount } from "svelte";

  const user = {
    photo: "https://via.placeholder.com/150",
    name: "Admin User",
  };

  const navigations = [
    { name: "Home", link: "/home", icon: "home" },
    { name: "Officials", link: "admin/officials", icon: "people" },
    { name: "Residents", link: "admin/residents", icon: "person" },
    { name: "History", link: "/admin/transaction", icon: "history" },
  ];

  let transactions = [
    { id: 1, date: "2024-12-01T00:00:00Z", amount: 500, status: "Pending" },
    { id: 2, date: "2024-12-02T00:00:00Z", amount: 200, status: "Pending" },
    { id: 3, date: "2024-12-03T00:00:00Z", amount: 150, status: "Pending" },
    { id: 4, date: "2024-12-04T00:00:00Z", amount: 350, status: "Pending" },
    { id: 5, date: "2024-12-05T00:00:00Z", amount: 450, status: "Pending" },
  ];

  function markAsPaid(id) {
    // Update the status of the transaction to "Paid"
    transactions = transactions.map((transaction) =>
      transaction.id === id ? { ...transaction, status: "Paid" } : transaction
    );
  }

  function searchTransaction() {
    alert("Search functionality will be implemented.");
  }

  function downloadTransactionData(transactionId) {
    alert(`Download data for transaction with ID: ${transactionId}`);
  }

  // Format the date
  function formatDate(date) {
    const options = { year: 'numeric', month: 'long', day: 'numeric' };
    return new Date(date).toLocaleDateString('en-US', options);
  }
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css"
  />
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    /* Prevent the whole page from scrolling */
    body, html {
      overflow: hidden;
      height: 100%;
    }

    /* Scrollable table */
    .scrollable-table-container {
      max-height: 400px; /* Set a fixed height for the table container */
      overflow-y: auto;
    }
  </style>
</svelte:head>

<div class="flex h-screen bg-gray-100">
  <!-- Sidebar -->
  <Sidebar {user}  />

  <!-- Content -->
  <main class="flex-1 p-8 space-y-8 overflow-y-auto">
    <!-- Page Header -->
    <h1 class="text-3xl font-semibold text-gray-800">Transaction History</h1>

    <!-- Transactions Table -->
    <div class="bg-white rounded-lg shadow-lg p-8">
      <div class="flex justify-between items-center mb-6">
        <button
          on:click={searchTransaction}
          class="px-4 py-2 text-white bg-gray-600 rounded shadow hover:bg-gray-700 focus:ring focus:ring-gray-300 transition"
        >
          <i class="fas fa-search"></i> Search
        </button>
      </div>
      <div class="scrollable-table-container">
        <table class="min-w-full text-left border-collapse border border-gray-300">
          <thead>
            <tr class="bg-gray-200 text-gray-700">
              <th class="px-6 py-3 border-b">Transaction ID</th>
              <th class="px-6 py-3 border-b">Date</th>
              <th class="px-6 py-3 border-b">Amount</th>
              <th class="px-6 py-3 border-b">Status</th>
              <th class="px-6 py-3 border-b">Actions</th>
            </tr>
          </thead>
          <tbody>
            {#each transactions as transaction (transaction.id)}
              <tr class="hover:bg-gray-50 transition-all">
                <td class="px-6 py-4 border-b">{transaction.id}</td>
                <td class="px-6 py-4 border-b">{formatDate(transaction.date)}</td>
                <td class="px-6 py-4 border-b">{transaction.amount}</td>
                <td class="px-6 py-4 border-b">
                  <span class={`px-3 py-1 rounded-full text-white ${transaction.status === "Paid" ? "bg-green-500" : "bg-yellow-500"}`}>
                    {transaction.status}
                  </span>
                </td>
                <td class="px-6 py-4 border-b space-x-4">
                  {#if transaction.status === "Pending"}
                    <button
                      on:click={() => markAsPaid(transaction.id)}
                      class="text-green-500 hover:text-green-600"
                    >
                      Mark as Paid
                    </button>
                  {/if}
                  <button
                    on:click={() => downloadTransactionData(transaction.id)}
                    class="text-blue-500 hover:text-blue-600"
                  >
                    <i class="fas fa-download"></i>
                  </button>
                </td>
              </tr>
            {/each}
          </tbody>
        </table>
      </div>
    </div>
  </main>
</div>