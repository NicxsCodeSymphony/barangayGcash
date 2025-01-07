<script>
  import { fade, scale } from "svelte/transition";

  let user = {
    name: "Juan Dela Cruz",
    barangay: "Barangay Example",
  };

  let documentTypes = ["Barangay Clearance", "Residency Certificate", "Business Permit"];
  let selectedDocument = "";
  let purpose = "";
  let requests = [
    { id: 1, type: "Barangay Clearance", status: "Pending" },
    { id: 2, type: "Residency Certificate", status: "Approved" },
  ];

  const submitRequest = () => {
    if (selectedDocument && purpose) {
      requests = [
        ...requests,
        { id: requests.length + 1, type: selectedDocument, status: "Pending" },
      ];
      selectedDocument = "";
      purpose = "";
      alert("Request submitted successfully!");
    } else {
      alert("Please fill in all fields.");
    }
  };
</script>

<div class="bg-gray-100 min-h-screen p-4 sm:p-6">
  <!-- Page Container -->
  <div in:fade>
    <!-- Header -->
    <div
      class="bg-white shadow rounded-lg p-4 sm:p-6 mb-6 transition-transform transform hover:scale-105 duration-300 ease-out"
    >
      <h1 class="text-lg sm:text-2xl font-bold text-gray-800">
        Welcome, {user.name}
      </h1>
      <p class="text-sm sm:text-base text-gray-600">
        Barangay: {user.barangay}
      </p>
    </div>

    <!-- Request Form -->
    <div
      class="bg-white shadow rounded-lg p-4 sm:p-6 mb-6 transition-transform transform hover:scale-105 duration-300 ease-out"
    >
      <h2 class="text-lg sm:text-xl font-semibold text-gray-800 mb-4">
        Request a Document
      </h2>
      <form
        class="grid grid-cols-1 sm:grid-cols-2 gap-4"
        on:submit|preventDefault={submitRequest}
        in:scale
      >
        <div>
          <label class="block text-gray-700 font-medium mb-2">
            Document Type
          </label>
          <select
            bind:value={selectedDocument}
            class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 transition-all duration-200 ease-in-out hover:ring-blue-400"
          >
            <option value="" disabled selected>Select a document</option>
            {#each documentTypes as doc}
              <option value={doc}>{doc}</option>
            {/each}
          </select>
        </div>
        <div>
          <label class="block text-gray-700 font-medium mb-2">Purpose</label>
          <input
            type="text"
            bind:value={purpose}
            placeholder="e.g., Job Application"
            class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 transition-all duration-200 ease-in-out hover:ring-blue-400"
          />
        </div>
        <button
          type="submit"
          class="col-span-1 sm:col-span-2 bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded-lg shadow-lg transform transition-transform duration-300 hover:scale-105"
        >
          Submit Request
        </button>
      </form>
    </div>

    <!-- Request History -->
    <div class="bg-white shadow rounded-lg p-4 sm:p-6" in:fade>
      <h2 class="text-lg sm:text-xl font-semibold text-gray-800 mb-4">
        Request History
      </h2>
      <div class="overflow-x-auto">
        <table
  class="w-full border-collapse border border-gray-200 text-sm sm:text-base"
  in:fade
>
  <thead>
    <tr class="bg-gray-100">
      <th class="border border-gray-200 px-4 py-2 text-left text-gray-700">
        #
      </th>
      <th class="border border-gray-200 px-4 py-2 text-left text-gray-700">
        Document
      </th>
      <th class="border border-gray-200 px-4 py-2 text-left text-gray-700">
        Status
      </th>
    </tr>
  </thead>
  <tbody>
    {#each requests as request}
      <tr
        class="hover:bg-blue-50 transition-colors duration-200"
        in:fade
        out:fade
      >
        <td class="border border-gray-200 px-4 py-2">{request.id}</td>
        <td class="border border-gray-200 px-4 py-2">{request.type}</td>
        <td
          class="border border-gray-200 px-4 py-2 font-semibold"
          class:!text-green-500={request.status === "Approved"}
          class:!text-yellow-500={request.status === "Pending"}
          class:!text-red-500={request.status === "Rejected"}
        >
          {request.status}
        </td>
      </tr>
    {/each}
  </tbody>
</table>
      </div>
    </div>
  </div>
</div>