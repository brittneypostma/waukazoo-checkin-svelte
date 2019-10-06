<script>
  import { namesData as data } from "../data.js";
  import Person from "./Person.svelte";
  export let listName;
  export let listPlace;
  const date = new Date();
  const n = date.toDateString();
  const time = date.toLocaleTimeString([], {
    hour: "2-digit",
    minute: "2-digit"
  });
</script>

<style>
  div {
    margin: 1rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  }
</style>

<div>
  <h2>{listName}</h2>
  <h3>{listPlace}</h3>
  <p>{time}</p>
</div>
