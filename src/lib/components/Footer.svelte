<script lang="ts">
  let { text, action, link = $bindable() } = $props();
</script>

<p class="text-sm text-center text-gray-500">
  {text} <a href={link} class="text-blue-500 hover:underline">{action}</a>
</p>
