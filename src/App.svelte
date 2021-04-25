<script>
  import PageMenu from "./menus/PageMenu.svelte";
  import HomePage from "./pages/HomePage.svelte";
  import GardenPage from "./pages/GardenPage.svelte";
  import AboutPage from "./pages/AboutPage.svelte";

  let selectedPage = "home";
</script>

<section id="page">
  <PageMenu bind:selectedPage />
  <main>
    {#if selectedPage == "home"}
      <HomePage />
    {:else if selectedPage == "gardens"}
      <GardenPage />
    {:else if selectedPage == "about"}
      <AboutPage />
    {:else}
      <HomePage />
    {/if}
  </main>
</section>

<style lang="scss">
  #page {
    position: relative;
  }
  main {
    padding: 1em;
  }
</style>
