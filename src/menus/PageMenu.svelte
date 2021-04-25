<script>
  import { routes } from "../routes";
  import PageMenuElement from "./PageMenuElement.svelte";

  export let selectedPage;
</script>

<nav>
  <ul>
    {#each routes as route}
      <li>
        <PageMenuElement {...route} bind:selectedPage />
      </li>
    {/each}
  </ul>
</nav>

<style lang="scss">
  nav {
    position: fixed;
    width: 100vw;
    z-index: 100;
    bottom: 0px;
    border-top: thin solid black;

    @media only screen and (min-width: 768px) {
      /* for desktop */
      position: sticky;
      top: 0;
      border-top: none;
      border-bottom: thin solid black;
    }

    ul {
      list-style: none;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      padding: 0;
      margin: 0;

      li {
        &:not(:first-of-type) {
          border-left: thin solid black;
        }
      }
    }
  }
</style>
