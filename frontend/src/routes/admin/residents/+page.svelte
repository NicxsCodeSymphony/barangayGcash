<script>
  import { onMount } from 'svelte';
  import Sidebar from '../sidebar.svelte';

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

  let residents = [
    { id: 1, name: "Carlos Mendoza", age: 45, email: "carlosmendoza@example.com" },
    { id: 2, name: "Maria Santos", age: 32, email: "mariasantos@example.com" },
    { id: 3, name: "James Lopez", age: 28, email: "jameslopez@example.com" },
    { id: 4, name: "Anna Reyes", age: 39, email: "annareyes@example.com" },
  ];

  let ageGroups = { "18-30": 0, "31-40": 0, "41-50": 0 };
  residents.forEach((resident) => {
    if (resident.age <= 30) ageGroups["18-30"]++;
    else if (resident.age <= 40) ageGroups["31-40"]++;
    else ageGroups["41-50"]++;
  });

  let showModal = false;
  let newResident = { name: '', age: '', email: '' };

  function addResident() {
    if (newResident.name && newResident.age && newResident.email) {
      const resident = {
        id: Date.now(), // Unique ID based on timestamp
        name: newResident.name,
        age: newResident.age,
        email: newResident.email,
      };
      residents = [...residents, resident];
      newResident = { name: '', age: '', email: '' }; // Reset form
      showModal = false;
    } else {
      alert('Please fill out all fields');
    }
  }

  function openModal() {
    showModal = true;
  }

  function closeModal() {
    showModal = false;
  }

  // Call createPieChart on mount
  onMount(() => {
    createPieChart();
  });

  function createPieChart() {
    const ctx = document.getElementById("ageChart").getContext("2d");
    new Chart(ctx, {
      type: "pie",
      data: {
        labels: Object.keys(ageGroups),
        datasets: [
          {
            data: Object.values(ageGroups),
            backgroundColor: ["#4caf50", "#2196f3", "#ff9800"],
            borderColor: ["#ffffff"],
            borderWidth: 1,
          },
        ],
      },
      options: {
        responsive: true,
        plugins: {
          legend: {
            position: "top",
          },
        },
      },
    });
  }
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css"
  />
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body, html {
      overflow: hidden;
      height: 100%;
    }

    .scrollable-table-container {
      max-height: 400px;
      overflow-y: auto;
    }

    .modal-overlay {
      position: fixed;
      inset: 0;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .modal {
      background-color: white;
      padding: 20px;
      border-radius: 8px;
      width: 400px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
  </style>
</svelte:head>

<div class="flex h-screen bg-gray-100">
  <Sidebar {user} {navigations} />

  <main class="flex-1 p-8 space-y-8 overflow-y-auto">
    <h1 class="text-3xl font-semibold text-gray-800">Residents Management</h1>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <div class="bg-gradient-to-r from-green-700 to-white text-white rounded-lg p-6 shadow flex flex-row items-center justify-between space-x-6">
        <div class="flex flex-col justify-between">
          <h2 class="text-lg font-semibold">Total Residents</h2>
          <p class="text-5xl font-extrabold mt-4">{residents.length}</p>
          <p class="mt-2 text-sm opacity-90">All residents registered in the system</p>
        </div>

        <div class="rounded-lg p-4 shadow flex justify-center items-center">
          <canvas id="ageChart" class="w-36 h-36"></canvas>
        </div>
      </div>
    </div>

    <div class="bg-white rounded-lg shadow-lg p-8">
      <div class="flex justify-between items-center mb-6">
        <button
          on:click={openModal}
          class="px-4 py-2 text-white bg-blue-600 rounded shadow hover:bg-blue-700 focus:ring focus:ring-blue-300 transition"
        >
          Add Resident
        </button>
        <button
          on:click={() => alert("Search functionality will be implemented.")}
          class="px-4 py-2 text-white bg-gray-600 rounded shadow hover:bg-gray-700 focus:ring focus:ring-gray-300 transition"
        >
          <i class="fas fa-search"></i> Search
        </button>
      </div>

      <div class="scrollable-table-container">
        <table class="min-w-full text-left border-collapse border border-gray-300">
          <thead>
            <tr class="bg-gray-200 text-gray-700">
              <th class="px-6 py-3 border-b">Resident Name</th>
              <th class="px-6 py-3 border-b">Age</th>
              <th class="px-6 py-3 border-b">Email</th>
              <th class="px-6 py-3 border-b">Actions</th>
            </tr>
          </thead>
          <tbody>
            {#each residents as resident (resident.id)}
              <tr class="hover:bg-gray-50 transition-all">
                <td class="px-6 py-4 border-b">{resident.name}</td>
                <td class="px-6 py-4 border-b">{resident.age}</td>
                <td class="px-6 py-4 border-b">{resident.email}</td>
                <td class="px-6 py-4 border-b space-x-4">
                  <button class="text-yellow-500 hover:text-yellow-600">
                    <i class="fas fa-edit"></i>
                  </button>
                  <button class="text-red-500 hover:text-red-600">
                    <i class="fas fa-trash"></i>
                  </button>
                  <button class="text-green-500 hover:text-green-600">
                    <i class="fas fa-download"></i>
                  </button>
                </td>
              </tr>
            {/each}
          </tbody>
        </table>
      </div>
    </div>

    <!-- Modal for adding resident -->
    {#if showModal}
      <div class="modal-overlay" on:click={closeModal}>
        <div class="modal" on:click|stopPropagation>
          <h2 class="text-2xl font-semibold mb-4">Add New Resident</h2>
          <div>
            <label class="block text-sm font-medium text-gray-700">Resident Name</label>
            <input
              type="text"
              bind:value={newResident.name}
              placeholder="Enter name"
              class="w-full p-2 mt-2 border border-gray-300 rounded-lg"
            />
          </div>
          <div class="mt-4">
            <label class="block text-sm font-medium text-gray-700">Age</label>
            <input
              type="number"
              bind:value={newResident.age}
              placeholder="Enter age"
              class="w-full p-2 mt-2 border border-gray-300 rounded-lg"
            />
          </div>
          <div class="mt-4">
            <label class="block text-sm font-medium text-gray-700">Email</label>
            <input
              type="email"
              bind:value={newResident.email}
              placeholder="Enter email"
              class="w-full p-2 mt-2 border border-gray-300 rounded-lg"
            />
          </div>

          <div class="mt-6 flex justify-end space-x-4">
            <button
              on:click={closeModal}
class="px-4 py-2 bg-gray-400 text-white rounded-lg hover:bg-gray-500"
            >
              Cancel
            </button>
            <button
              on:click={addResident}
              class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700"
            >
              Add Resident
            </button>
          </div>
        </div>
      </div>
    {/if}
  </main>


  <h1>This yeah</h1>
  
</div>
              

