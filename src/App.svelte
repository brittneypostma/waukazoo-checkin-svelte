<script>
  import Buttons from "./components/Buttons.svelte";
  import List from "./components/List.svelte";
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
    <List />
  </div>
</div>
