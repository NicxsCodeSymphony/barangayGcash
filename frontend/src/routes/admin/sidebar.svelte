<script>
  export let user = {
    name: "John Doe",
    photo: "https://via.placeholder.com/150", // Replace with actual photo URL
  };
</script>

<div class="w-64 bg-gray-900 h-screen flex flex-col text-white">
  <!-- User Profile -->
  <div class="flex flex-col items-center bg-gray-800 p-6 shadow-md">
    <img
      src={user.photo}
      alt="User Photo"
      class="w-24 h-24 rounded-full border-4 border-indigo-500 mb-4 hover:scale-110 transition-transform duration-500"
    />
    <h2 class="text-lg font-bold">{user.name}</h2>
  </div>

  <!-- Navigation Links -->
  <nav class="flex-1 mt-6 space-y-2 px-4">
    <a
      href="/admin"
      class="block px-4 py-2 rounded-lg hover:bg-indigo-500 transition-colors duration-300"
    >
      Dashboard
    </a>
    <a
      href="/admin/officials"
      class="block px-4 py-2 rounded-lg hover:bg-indigo-500 transition-colors duration-300"
    >
      Officials
    </a>
    <a
      href="/admin/residents"
      class="block px-4 py-2 rounded-lg hover:bg-indigo-500 transition-colors duration-300"
    >
      Residents
    </a>
    <a
      href="/admin/transaction"
      class="block px-4 py-2 rounded-lg hover:bg-indigo-500 transition-colors duration-300"
    >
      Transactions
    </a>
  </nav>

  <!-- Logout Button -->
  <div class="px-4 pb-6">
    <a
      href="#logout"
      class="block w-full text-center bg-red-500 text-white py-2 rounded-lg hover:bg-red-600 transition-all duration-300 shadow-lg"
    >
      Log Out
    </a>
  </div>
</div>