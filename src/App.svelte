<script>
  import { list } from "./useLocalStorage.js";
  import Buttons from "./components/Buttons.svelte";
  import List from "./components/List.svelte";

  let list_value;

  const unsubscribe = list.subscribe(value => {
    list_value = value;
  });

  console.log(list_value);
</script>

<style>
  .container {
    display: grid;
    grid-template-columns: 10fr 1fr;
    height: 100%;
    text-align: center;
  }
  .left-container {
    display: grid;
    align-items: space-around;
    background-color: rgb(106, 106, 248);
  }
  .list {
    width: 400px;
  }
</style>

<div class="container">
  <div class="left-container">
    <Buttons />
  </div>
  <div class="list">
    <h2>People in the building</h2>
    {#each list_value as person}
      <List {person} />
    {/each}
  </div>
</div>
