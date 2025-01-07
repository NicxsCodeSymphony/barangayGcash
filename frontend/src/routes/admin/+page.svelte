<script>
  import Sidebar from "./sidebar.svelte";

  // Data for the dashboard
  const user = {
    photo: "https://via.placeholder.com/150",
    name: "Admin User",
  };

  const navigations = [
    { name: "Home", link: "/home", icon: "home" },
    { name: "Officials", link: "/admin/officials", icon: "people" },
    { name: "Residents", link: "admin/residents", icon: "person" },
    { name: "Transactions", link: "/transactions", icon: "attach_money" },
    { name: "History", link: "/history", icon: "history" },
  ];

  const stats = [
    { title: "Total Officials", value: 42, bgColor: "bg-gradient-to-r from-blue-600 to-blue-400", icon: "group" },
    { title: "Total Residents", value: 856, bgColor: "bg-gradient-to-r from-green-600 to-green-400", icon: "home" },
    { title: "Total Transactions", value: 1342, bgColor: "bg-gradient-to-r from-purple-600 to-purple-400", icon: "receipt" },
    { title: "Total Earnings", value: "$12,345", bgColor: "bg-gradient-to-r from-yellow-600 to-yellow-400", icon: "monetization_on" },
  ];

  const chartUrl = "https://www.chartjs.org/docs/latest/getting-started/";

  const tableData = [
    { id: 1, name: "John Doe", role: "Resident", status: "Active" },
    { id: 2, name: "Jane Smith", role: "Official", status: "Inactive" },
    { id: 3, name: "Alice Johnson", role: "Resident", status: "Active" },
    { id: 4, name: "Bob Brown", role: "Official", status: "Active" },
  ];
</script>

<div class="flex h-screen bg-gray-50">
  <!-- Sidebar -->
  <Sidebar {user} {navigations} />

  <!-- Content Area -->
  <main class="flex-1 p-8 space-y-8 overflow-y-auto">
    <!-- Dashboard Title -->
    <div class="flex justify-between items-center">
      <h1 class="text-4xl font-semibold text-gray-800">Admin Dashboard</h1>
      <div class="text-gray-500">Last Updated: 5 mins ago</div>
    </div>

    <!-- Statistics Cards -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
      {#each stats as stat}
        <div
          class={`relative p-8 rounded-xl shadow-xl transform transition-all hover:scale-105 ${stat.bgColor} text-white flex flex-col items-center justify-center`}
        >
          <div class="absolute top-0 right-0 p-2 text-3xl bg-opacity-70 rounded-full bg-white text-gray-800">
            <i class="material-icons">{stat.icon}</i>
          </div>
          <p class="text-xl font-medium">{stat.title}</p>
          <p class="text-4xl font-bold mt-4">{stat.value}</p>
          <div class="absolute bottom-0 left-0 w-full h-1 bg-white opacity-25"></div>
        </div>
      {/each}
    </div>

    <!-- Chart Section -->
    <div class="bg-white rounded-2xl shadow-2xl p-8">
      <h2 class="text-2xl font-semibold text-gray-800 mb-4">Activity Overview</h2>
      <div class="flex justify-between items-center mb-6">
        <p class="text-lg text-gray-600">Interactive chart that can be updated in real time.</p>
        <a href={chartUrl} class="text-blue-500 underline hover:text-blue-700">Learn more</a>
      </div>
      <div class="w-full h-80 bg-gray-200 rounded-lg flex items-center justify-center relative border-2 border-dashed">
        <span class="text-gray-500">[Insert Chart Here]</span>
      </div>
    </div>

    <!-- Recent Activities Table -->
    <div class="bg-white rounded-2xl shadow-xl p-8">
      <h2 class="text-2xl font-semibold text-gray-800 mb-6">Recent Activities</h2>
      <div class="overflow-x-auto">
        <table class="min-w-full table-auto text-left border-collapse border border-gray-300">
          <thead>
            <tr class="bg-gray-100 text-gray-700">
              <th class="px-6 py-3 border-b">ID</th>
              <th class="px-6 py-3 border-b">Name</th>
              <th class="px-6 py-3 border-b">Role</th>
              <th class="px-6 py-3 border-b">Status</th>
            </tr>
          </thead>
          <tbody>
            {#each tableData as row (row.id)}
              <tr class="hover:bg-gray-50 transition-all">
                <td class="px-6 py-4 border-b">{row.id}</td>
                <td class="px-6 py-4 border-b">{row.name}</td>
                <td class="px-6 py-4 border-b">{row.role}</td>
                <td
                  class={`px-6 py-4 border-b font-semibold ${
                    row.status === "Active" ? "text-green-600" : "text-red-600"
                  }`}
                >
                  <span
                    class={`inline-block px-3 py-1 rounded-full ${
                      row.status === "Active" ? "bg-green-100 text-green-600" : "bg-red-100 text-red-600"
                    }`}
                  >
                    {row.status}
                  </span>
                </td>
              </tr>
            {/each}
          </tbody>
        </table>
      </div>
    </div>
  </main>
</div>