<script>
  import { namesData as data } from "../data.js";
  let visName = "";
  let visPlace = "";
  let guestVisName = "";
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
  <label for="volunteersList">Visitor Name</label>

  <select
    required
    name="Name"
    id="volunteersList"
    bind:value={visName}
    on:input={setVisName}>

    <option selected>Search for Your Name</option>
    {#each data as name}
      <option>{name.firstname} {name.lastname}</option>
    {/each}
  </select>
  {#if visName === 'Guest Visitor'}
    <label for="guest">Guest Name</label>
    <input
      id="guest"
      type="text"
      placeholder="Guest Name"
      bind:value={guestVisName}
      class="guest-name"
      name="Other" />
  {/if}
  <label for="visPlace">Location</label>
  <input
    type="text"
    id="visPlace"
    bind:value={visPlace}
    on:input={setVisPlace} />
  <button>Add</button>
</div>
