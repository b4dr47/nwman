<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
  import '../app.css';
	let { children } = $props();
</script>

<nav class="font-bold text-3xl bg-blend-darken bg-gray-900 text-gray-200 p-4">
  <a href='/'>Home</a>
  <a href='/login'>Login</a>
  <a href='/register'>Register</a>
</nav>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children()}
