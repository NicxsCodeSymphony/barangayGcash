<script>
  import Sidebar from "../sidebar.svelte";
  import { onMount } from "svelte";
  import Add from "./add.svelte";

  const user = {
    photo: "https://via.placeholder.com/150",
    name: "Admin User",
  };

  const navigations = [
    { name: "Home", link: "/home", icon: "home" },
    { name: "Officials", link: "admin/officials", icon: "people" },
    { name: "History", link: "/admin/transaction", icon: "history" },
  ];

  let officials = [
    { id: 1, name: "John Doe", position: "Mayor", email: "johndoe@example.com" },
    { id: 2, name: "Jane Smith", position: "Councilor", email: "janesmith@example.com" },
    { id: 3, name: "Mark Johnson", position: "Treasurer", email: "markjohnson@example.com" },
    { id: 4, name: "Sara Lee", position: "Secretary", email: "saralee@example.com" },
  ];

  let showModal = false;

  function addOfficial(official) {
    officials = [...officials, { ...official, id: officials.length + 1 }];
  }

  function toggleModal() {
    showModal = !showModal;
  }

  function searchOfficial() {
    alert("Search functionality will be implemented.");
  }

  function downloadOfficialData(officialId) {
    alert(`Download data for official with ID: ${officialId}`);
  }

  function editOfficial(id) {
    alert(`Edit functionality for official with ID: ${id} will be implemented.`);
  }

  function deleteOfficial(id) {
    if (confirm(`Are you sure you want to delete the official with ID: ${id}?`)) {
      officials = officials.filter((official) => official.id !== id);
    }
  }

  // Initialize the chart when component is mounted
  onMount(() => {
    const ctx = document.getElementById("officialsChart").getContext("2d");
    new Chart(ctx, {
      type: "pie",
      data: {
        labels: ["Officials Registered"],
        datasets: [
          {
            data: [officials.length, 100 - officials.length],
            backgroundColor: ["#4CAF50", "#f0f0f0"],
            borderColor: ["#4CAF50", "#f0f0f0"],
            borderWidth: 1,
          },
        ],
      },
      options: {
        responsive: true,
        plugins: {
          legend: {
            display: false,
          },
        },
      },
    });
  });
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css"
  />
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    /* Prevent the whole page from scrolling */
    body,
    html {
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
  <Sidebar {user} {navigations} />

  <!-- Content -->
  <main class="flex-1 p-8 space-y-8 overflow-y-auto">
    <!-- Page Header -->
    <h1 class="text-3xl font-semibold text-gray-800">Officials Management</h1>

    <!-- Grid with Counter and Pie Chart in Row Layout -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <!-- Counter with Pie Chart -->
      <div class="bg-gradient-to-r from-blue-700 to-white text-white rounded-lg p-6 shadow flex flex-row items-center justify-between space-x-6">
        <!-- Counter -->
        <div class="flex flex-col justify-between">
          <h2 class="text-lg font-semibold">Total Officials</h2>
          <p class="text-5xl font-extrabold mt-4">{officials.length}</p>
          <p class="mt-2 text-sm opacity-90">All officials registered in the system</p>
        </div>

        <!-- Pie Chart (Placeholder) -->
        <div class="rounded-lg p-4 shadow flex justify-center items-center">
          <canvas id="officialsChart" class="w-36 h-36"></canvas>
        </div>
      </div>
    </div>

    <!-- Officials Table -->
    <div class="bg-white rounded-lg shadow-lg p-8">
      <div class="flex justify-between items-center mb-6">
       <button
  on:click={toggleModal}
  class="px-4 py-2 text-white bg-blue-600 rounded shadow hover:bg-blue-700 focus:ring focus:ring-blue-300 transition"
>
  Add Official
</button>
        <button
          on:click={searchOfficial}
          class="px-4 py-2 text-white bg-gray-600 rounded shadow hover:bg-gray-700 focus:ring focus:ring-gray-300 transition"
        >
          <i class="fas fa-search"></i> Search
        </button>
      </div>
      <div class="scrollable-table-container">
        <table class="min-w-full text-left border-collapse border border-gray-300">
          <thead>
            <tr class="bg-gray-200 text-gray-700">
              <th class="px-6 py-3 border-b">Official Name</th>
              <th class="px-6 py-3 border-b">Position</th>
              <th class="px-6 py-3 border-b">Email</th>
              <th class="px-6 py-3 border-b">Actions</th>
            </tr>
          </thead>
          <tbody>
            {#each officials as official (official.id)}
              <tr class="hover:bg-gray-50 transition-all">
                <td class="px-6 py-4 border-b">{official.name}</td>
                <td class="px-6 py-4 border-b">{official.position}</td>
                <td class="px-6 py-4 border-b">{official.email}</td>
                <td class="px-6 py-4 border-b space-x-4">
                  <button
                    on:click={() => editOfficial(official.id)}
                    class="text-yellow-500 hover:text-yellow-600"
                  >
                    <i class="fas fa-edit"></i>
                  </button> 
                  <button
                    on:click={() => deleteOfficial(official.id)}
                    class="text-red-500 hover:text-red-600"
                  >
                    <i class="fas fa-trash"></i>
                  </button>
                  <button
                    on:click={() => downloadOfficialData(official.id)}
                    class="text-green-500 hover:text-green-600"
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

  <!-- Add Official Modal -->
  <Add
    isVisible={showModal}
    onClose={toggleModal}
    onAddOfficial={addOfficial}
  />
</div>