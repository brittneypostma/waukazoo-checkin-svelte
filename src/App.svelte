<script>
  import { get, set } from "idb-keyval";
  import Buttons from "./components/Buttons.svelte";
  import List from "./components/List.svelte";

  let list = [];
  get("list").then(arr => {
    if (arr !== undefined) list = arr;
  });
  console.log(list);

  const addName = () => {
    list = [
      ...list,
      {
        id: nextId,
        name: newName
      }
    ];

    set("list", list);
    nextId = nextId++;
    newName = "";
    console.log(list);
  };
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
    <Buttons handler={addName} />
  </div>
  <div class="list">
    <h2>People in the building</h2>
    {#each list as person}
      <List {person} />
    {/each}
  </div>
</div>
