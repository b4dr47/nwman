<script lang="ts">
  import { signIn } from '$lib/auth-client';
  import { goto } from '$app/navigation';

  let email = $state('');
  let password = $state('');
  let error = $state('');
  let loading = $state(false);

  async function handleLogin() {
    loading = true;
    error = '';
    const { error: err } = await signIn.email({ email, password });
    if (err) {
      error = err.message ?? 'Login failed';
    } else {
      goto('/dashboard');
    }
    loading = false;
  }
</script>

<div class="min-h-screen flex items-center justify-center bg-gray-900">
  <div class="w-full max-w-md bg-gray-800 rounded-2xl shadow-lg p-8 space-y-6">
    <h1 class="text-2xl font-bold text-gray-100">Sign in</h1>

    {#if error}
      <p class="text-sm text-red-100 bg-red-500 px-4 py-2 rounded-lg">{error}</p>
    {/if}

    <div class="space-y-4">
      <div>
        <label class="block text-sm font-medium text-gray-100 mb-1">Email
        <input
          type="email"
          bind:value={email}
          class="w-full border border-gray-300 rounded-lg px-3 py-2 text-gray-200 focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="you@example.com"
        />
        </label>
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-100 mb-1">Password
        <input
          type="password"
          bind:value={password}
          class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        </label>
      </div>
      <button
        onclick={handleLogin}
        disabled={loading}
        class="w-full bg-blue-600 text-white py-2 rounded-lg font-medium hover:bg-blue-500 disabled:opacity-50 transition"
      >
        {loading ? 'Signing in…' : 'Sign in'}
      </button>
    </div>

    <p class="text-sm text-center text-gray-500">
      No account? <a href="/register" class="text-blue-500 hover:underline">Register</a>
    </p>
  </div>
</div>
