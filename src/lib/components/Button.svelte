<button
  onclick={handleRegister}
  disabled={loading}
  class="w-full bg-blue-600 text-white py-2 rounded-lg font-medium hover:bg-blue-500 disabled:opacity-50 transition"
>
  {loading ? 'Creating account…' : 'Create account'}
</button>

