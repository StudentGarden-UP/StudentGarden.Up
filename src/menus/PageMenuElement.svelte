<script>
  export let title;
  export let pageId;
  export let selectedPage;
</script>

<a
  href="#{pageId}"
  class:selected={selectedPage === pageId}
  on:click|preventDefault={() => {
    selectedPage = pageId;
  }}>{title}</a
>

<style lang="scss">
  a {
    display: block;
    padding: 1em;
    background-color: rgb(62, 145, 62);
    text-align: center;
    font-weight: 600;
    letter-spacing: 0.1em;
    color: white;
    text-decoration: none;

    &.selected {
      background-color: rgb(34, 75, 34);
      cursor: default;
    }
  }
</style>
