<script>
  import { fade } from 'svelte/transition';
  import { quintOut } from 'svelte/easing';
  import { tweened } from 'svelte/motion';

  let logoScale = tweened(0.5, { duration: 1200, easing: quintOut });
  let formOpacity = tweened(0, { duration: 800, easing: quintOut });

  // Trigger animations on mount
  $: logoScale.set(1);
  $: formOpacity.set(1);
</script>

<main class="min-h-screen flex flex-col justify-center items-center bg-gradient-to-br from-gray-800 to-purple-900 text-white">
  <!-- Animated Logo -->
  <div
    class="flex items-center justify-center mb-10"
    in:fade={{ duration: 800 }}
    style="transform: scale({$logoScale});"
  >
    <svg
      class="w-20 h-20 text-indigo-500 animate-pulse"
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      viewBox="0 0 24 24"
      stroke-width="2"
      stroke="currentColor"
    >
      <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4" />
    </svg>
  </div>

  <!-- Login Form -->
  <form
    class="w-full max-w-md bg-gray-900 bg-opacity-75 rounded-lg p-8 shadow-lg transition-all duration-700 hover:shadow-2xl transform hover:scale-105"
    style="opacity: {$formOpacity};"
    in:fade={{ duration: 1000 }}
  >
    <h2 class="text-2xl font-bold mb-6 text-center">Welcome Back!</h2>

    <!-- Email Field -->
    <div class="mb-4 relative group">
      <input
        type="email"
        id="email"
        class="peer w-full p-4 bg-gray-800 text-gray-200 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:outline-none placeholder-transparent"
        placeholder="Email Address"
        required
      />
      <label
        for="email"
        class="absolute left-4 top-4 text-gray-400 text-sm transition-all duration-300 peer-placeholder-shown:top-4 peer-placeholder-shown:text-gray-500 peer-focus:top-0 peer-focus:text-indigo-400 peer-focus:text-xs"
      >
        Email Address
      </label>
    </div>

    <!-- Password Field -->
    <div class="mb-6 relative group">
      <input
        type="password"
        id="password"
        class="peer w-full p-4 bg-gray-800 text-gray-200 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:outline-none placeholder-transparent"
        placeholder="Password"
        required
      />
      <label
        for="password"
        class="absolute left-4 top-4 text-gray-400 text-sm transition-all duration-300 peer-placeholder-shown:top-4 peer-placeholder-shown:text-gray-500 peer-focus:top-0 peer-focus:text-indigo-400 peer-focus:text-xs"
      >
        Password
      </label>
    </div>

    <!-- Submit Button -->
    <button
      type="submit"
      class="w-full bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-3 rounded-lg shadow-md transition-transform transform hover:scale-105"
    >
      Login
    </button>
  </form>

  <!-- Footer -->
  <p class="mt-6 text-sm text-gray-300">
    Don’t have an account?
    <a href="/register" class="text-indigo-400 hover:underline">Sign up</a>
  </p>
</main>