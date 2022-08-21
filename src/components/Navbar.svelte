<script lang="ts">
  import ButtonLink from './ButtonLink.svelte';

  const scrollIntoView = ({ detail: { target } }: CustomEvent) => {
    const el = document.querySelector(target.getAttribute('href'));
    if (!el) return;
    el.scrollIntoView({
      behavior: 'smooth',
    });
  };
</script>

<nav class="nav">
  <div class="logo">
    three
    <br />
    hex
  </div>
  <div>
    <ButtonLink
      text={'Colors'}
      href="#colors"
      on:click={scrollIntoView}
      preventDefault
    />
  </div>
</nav>

<style lang="scss">
  .nav {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem;

    @media screen and (min-width: 768px) {
      padding: 4rem;
    }

    .logo {
      user-select: none;
      cursor: pointer;
      font-weight: 550;
      font-size: 1rem;
      margin: 0;
      line-height: 1;
      border: 1px solid var(--link-border);
      aspect-ratio: 1/1;
      padding: 0.8rem;
      display: grid;
      place-items: center;
      @media screen and (min-width: 768px) {
        font-size: 1.2rem;
      }
    }
  }
</style>
