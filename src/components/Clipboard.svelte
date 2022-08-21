<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let text: string;

  async function copy() {
    await navigator.clipboard.writeText(text);
    dispatch('copy');
  }
</script>

<slot {copy} />
