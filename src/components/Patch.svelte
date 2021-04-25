<script>
  import { plants } from "../plants";

  let svgElement;
  let popoutElement;
  let popoutPlant = null;
  function openDetails(evt) {
    let g = evt.target.parentElement;
    let globalPlantBounds = g.getBoundingClientRect();
    let globalSvgBounds = svgElement.getBoundingClientRect();
    let top = globalPlantBounds.bottom - globalSvgBounds.y;
    let left =
      (globalPlantBounds.left + globalPlantBounds.right) / 2 -
      globalSvgBounds.x;
    console.log(globalSvgBounds, globalPlantBounds);
    popoutElement.style.top = `${top}px`;
    popoutElement.querySelector(".plantLocator").style.left = `${left}px`;

    let plantName = g.parentElement.dataset.plant;
    let plant = plants.find((plant) => plant.name === plantName);

    popoutPlant = plant;
    setTimeout(() =>
      popoutElement.scrollIntoView({ block: "end", behavior: "smooth" })
    );
  }
  function closeDetails() {
    popoutPlant = null;
  }
</script>

<section class="patch">
  <svg
    viewBox="0 0 100 300"
    on:click|capture={closeDetails}
    bind:this={svgElement}
  >
    {#each plants as plant}
      <g data-plant={plant.name}>
        {#each plant.locations as location}
          <g
            class="plant"
            transform="translate({location.x} {location.y})"
            on:click={openDetails}
          >
            <circle r={location.r} cx={0} cy={0} />
            <text>{plant.name}</text>
          </g>
        {/each}
      </g>
    {/each}
  </svg>
  <aside
    class="popout"
    class:open={popoutPlant !== null}
    bind:this={popoutElement}
  >
    <div class="plantLocator" />
    {#if popoutPlant}
      <h1>{popoutPlant.name}</h1>
    {/if}
  </aside>
</section>

<style lang="scss">
  .patch {
    position: relative;

    .popout {
      display: none;
      position: absolute;
      z-index: 1;
      border: thin solid black;
      background-color: white;
      width: 100%;
      padding: 1em;

      .plantLocator {
        position: absolute;
        top: calc(-1em - 3px);
        transform: translate(-0.5em, 0);
        width: 0;
        height: 0;
        border-left: calc(0.5em + 1px) solid transparent;
        border-right: calc(0.5em + 1px) solid transparent;
        border-bottom: calc(1em + 2px) solid black;

        &:after {
          position: absolute;
          content: "";
          width: 0;
          height: 0;
          top: 2px;
          left: -0.5em;
          border-left: 0.5em solid transparent;
          border-right: 0.5em solid transparent;
          border-bottom: calc(1em + 1px) solid white;
        }
      }

      &.open {
        display: block;
      }
    }

    svg {
      border: 8pt solid #412117;
      background-color: #6e492b;
      stroke-width: 0.1pt;

      .plant {
        circle {
          stroke: black;
          fill: green;
        }
        text {
          font-size: 2pt;
          text-anchor: middle;
          alignment-baseline: middle;
        }

        &.highlighted {
          stroke: red;
        }
      }
    }
  }
</style>
