<script>
  import { onMount } from "svelte";

  import Visitor from "./Visitor.svelte";
  import Volunteer from "./Volunteer.svelte";

  let formName;

  onMount(() => {
    let visBtn = document.getElementById("visBtn");
    let volBtn = document.getElementById("volBtn");

    visBtn.addEventListener("click", () => {
      return (formName = "Visitor");
    });
    volBtn.addEventListener("click", () => {
      return (formName = "Volunteer");
    });
  });
</script>

<style>
  .leftScreen {
    display: grid;
    align-content: space-around;
    background-color: rgb(106, 106, 248);
  }
</style>

<div class="leftScreen">
  <div class="left">
    <div>
      <button id="visBtn">Visitor</button>
    </div>
    <div>
      <button id="volBtn">Volunteer</button>
    </div>
  </div>

  <div class="right">
    {#if formName === 'Visitor'}
      <Visitor />
    {:else if formName === 'Volunteer'}
      <Volunteer />
    {/if}
  </div>
</div>
