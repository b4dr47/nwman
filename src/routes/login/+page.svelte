<script lang="ts">
  import { signIn } from '$lib/auth-client';
  import { goto } from '$app/navigation';
  import { InputField, Footer } from '$lib';

  let email = $state('');
  let password = $state('');
  let error = $state('');
  let loading = $state(false);

  async function Login() {
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

      <InputField
        text="Email"
        type="email"
        bind:value={email}
        placeholder="you@exmample.com"
      ></InputField>
      <InputField
        text="password"
        type="password"
        bind:value={password}
      ></InputField>
      <button
        onclick={Login}
        disabled={loading}
        class="w-full bg-blue-600 text-white py-2 rounded-lg font-medium hover:bg-blue-500 disabled:opacity-50 transition"
      >
        {loading ? 'Signing in…' : 'Sign in'}
      </button>
    </div>
    <Footer
      text="No account?"
      link="/register"
      action="Register"
    ></Footer>
  </div>
</div>
