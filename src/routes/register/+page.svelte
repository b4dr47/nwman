<script lang="ts">
  import { signUp } from '$lib/auth-client';
  import { goto } from '$app/navigation';
  import { InputField, Footer } from '$lib';
  let name = $state('');
  let email = $state('');
  let password = $state('');
  let error = $state('');
  let loading = $state(false);

  async function handleRegister() {
    loading = true;
    error = '';
    const { error: err } = await signUp.email({ name, email, password });
    if (err) {
      error = err.message ?? 'Registration failed';
    } else {
      goto('/dashboard');
    }
    loading = false;
  }
</script>

<div class="min-h-screen flex items-center justify-center bg-gray-900">
  <div class="w-full max-w-md bg-gray-800 rounded-2xl shadow-lg p-8 space-y-6">
    <h1 class="text-2xl font-bold text-gray-100">Create account</h1>

    {#if error}
      <p class="text-sm text-red-50 bg-red-500 px-4 py-2 rounded-lg">{error}</p>
    {/if}

    <div class="space-y-4">
      <InputField
        text="Name"
        bind:value={name}
        placeholder="Your name"
      ></InputField>
      <InputField
        text="Email"
        bind:value={email}
        type="email"
        placeholder="you@example.com"
      ></InputField>
      <InputField
        text="Password"
        type="password"
        bind:value={password}
      ></InputField>

      <button
        onclick={handleRegister}
        disabled={loading}
        class="w-full bg-blue-600 text-white py-2 rounded-lg font-medium hover:bg-blue-500 disabled:opacity-50 transition"
      >
        {loading ? 'Creating account…' : 'Create account'}
      </button>
    </div>
    
    <Footer
      text="Already have an account?"
      link="/login"
      action="Sign in"
    ></Footer>
  </div>
</div>
