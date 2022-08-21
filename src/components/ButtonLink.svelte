<script lang="ts">
  import { onMount, onDestroy, createEventDispatcher } from 'svelte';

  export let text: string;
  export let href: string;
  export let preventDefault = false;

  let button: HTMLAnchorElement;
  const dispatch = createEventDispatcher();

  const onClick = (event: MouseEvent) => {
    if (preventDefault) {
      event.preventDefault();
    }

    return dispatch('click', event);
  };

  onMount(() => {
    button.addEventListener('click', onClick);
  });

  onDestroy(() => {
    if (button) {
      button.removeEventListener('click', onClick);
    }
  });
</script>

<a bind:this={button} {href}>{text}</a>

<style lang="scss">
  a {
    border: 1px solid var(--link-border);
    padding: 1rem 2rem;
    border-radius: 10rem;
    font-size: 1rem;
    font-weight: 550;
    letter-spacing: -0.006rem;
    user-select: none;

    @media screen and (min-width: 768px) {
      font-size: 1.2rem;
    }
  }
</style>
