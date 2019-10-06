<script>
  let visName = "";
  let visPlace = "";
  const setVisName = e => (visName = e.target.value);
  const setVisPlace = e => (visPlace = e.target.value);
</script>

<style>
  .form {
    display: grid;
    align-items: center;
    justify-content: center;
    grid-gap: 10px;
  }
</style>

<div class="form">
  <h2>Visitor</h2>
  <label for="visName">Visitor Name</label>
  <input type="text" id="visName" value={visName} on:input={setVisName} />
  <label for="visPlace">Location</label>
  <input type="text" id="visPlace" value={visPlace} on:input={setVisPlace} />
  <button>Add</button>
</div>
