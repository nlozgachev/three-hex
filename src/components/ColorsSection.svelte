<script lang="ts">
  import VirtualList from 'svelte-tiny-virtual-list';
  import ColorBox from './ColorBox.svelte';

  export let colors: string[];

  let gridHeight: number;
  let gridWidth: number;
  let rowColumns: number = 6;
  let itemHeight: number = 160 + 16;
  let itemWidth: number = 110 + 16;

  $: if (gridWidth > itemWidth) {
    rowColumns = Math.floor(gridWidth / itemWidth);
  }

  $: gridHeight = itemHeight * Math.ceil(colors.length / rowColumns);
</script>

<svelte:window />
<section class="section" id="colors">
  <div
    class="wrapper"
    bind:offsetHeight={gridHeight}
    bind:clientWidth={gridWidth}
  >
    <VirtualList
      width="100%"
      height={gridHeight}
      itemCount={Math.ceil(colors.length / rowColumns)}
      itemSize={itemHeight}
    >
      <div
        slot="item"
        let:index
        let:style
        class="row"
        style="--grid-columns: {rowColumns}; {style}"
      >
        {#each Array(rowColumns) as _, i}
          {#if colors[index * rowColumns + i]}
            <ColorBox hex={colors[index * rowColumns + i]} />
          {/if}
        {/each}
      </div>
    </VirtualList>
  </div>
</section>

<style lang="scss">
  :global(.virtual-list-wrapper) {
    overflow: hidden !important;
  }
  :global(.virtual-list-inner) {
    overflow: hidden !important;
  }

  .section {
    background: #444;
    padding: 4rem 0;
  }

  .wrapper {
    max-width: 800px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .row {
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(var(--grid-columns), minmax(0, 1fr));
  }
</style>
