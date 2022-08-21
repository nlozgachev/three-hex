<script lang="ts">
  import Clipboard from './Clipboard.svelte';
  import { writable } from 'svelte/store';
  import { draw, fade } from 'svelte/transition';

  export let hex: string | undefined;

  let copyIconState = writable(false);
  let hexValue = hex ? '#'.concat(hex) : '';
  let isCopied = false;

  copyIconState.subscribe((value) => {
    isCopied = value;
  });

  const animationDuration = 600;
</script>

<Clipboard
  text={hexValue}
  let:copy
  on:copy={() => {
    copyIconState.set(true);
    setTimeout(() => {
      copyIconState.set(false);
    }, animationDuration * 2);
  }}
>
  <article class="color-wrapper" on:click={copy}>
    <div class="color-square" style:--hex={hexValue}>
      {#if isCopied}
        <svg
          viewBox="0 0 30 30"
          xmlns="http://www.w3.org/2000/svg"
          fill="#fff"
          stroke="currentColor"
          stroke-width="1"
          class="copy-icon circle"
          transition:fade={{ duration: animationDuration }}
        >
          <circle cx="15" cy="15" r="12" />
        </svg>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="1"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="copy-icon checkmark"
          transition:fade={{ duration: animationDuration }}
        >
          <polyline
            in:draw={{ duration: animationDuration }}
            points="20 6 9 17 4 12"
          />
        </svg>
      {/if}
    </div>
    <div class="color-hex">{hexValue}</div>
  </article>
</Clipboard>

<style lang="scss">
  .color-wrapper {
    background: #fff;
    padding: 0.2rem 0.2rem 0 0.2rem;
    display: grid;
    grid-template-rows: 1fr auto;
    cursor: pointer;
    margin-bottom: 1rem;
  }

  .color-square {
    background: var(--hex);
    position: relative;
    display: flex;
  }

  .color-hex {
    font-weight: 500;
    font-size: 1rem;
    letter-spacing: 0.02;
    padding: 1rem 0.5rem;
    text-transform: uppercase;
  }

  .copy-icon {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    margin: auto;
  }

  .checkmark {
    width: 40px;
    top: 6px;
    left: 2px;
  }

  .circle {
    width: 56px;
    fill: var(--background);
  }
</style>
