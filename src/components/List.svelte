<script>
  export let name;
  export let location;
  export let isCompleted;
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
  <h2>{name}</h2>
  <p>{location}</p>
  <p>{time}</p>
</div>
