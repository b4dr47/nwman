<script lang="ts">
  let { text, type, placeholder, value = $bindable() } = $props();
</script>

<div>
  <label class="block text-sm font-medium text-gray-100 mb-1">{text}
    <input
      type={type}
      bind:value
      class="w-full border border-gray-300 rounded-lg px-3 py-2 text-gray-200 focus:outline-none focus:ring-2 focus:ring-blue-500"
      placeholder={placeholder}
    />
  </label>
</div>
