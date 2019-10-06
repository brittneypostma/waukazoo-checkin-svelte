<script>
  import { onMount } from "svelte";
  import { get, set } from "idb-keyval";

  import Input from "./Input.svelte";

  let visName = "";
  let visPlace = "";
  let guestVisName = "";

  const setVisName = e => (visName = e.target.value);
  const setVisPlace = e => (visPlace = e.target.value);
  const setGuestVisName = e => (guestVisName = e.target.value);

  onMount(() => {
    const visForm = document.forms["visitor-form"];
    visForm.addEventListener("submit", e => {
      e.preventDefault();

      document.getElementById("visitorForm").reset();
    });
  });

  let newName = "";
  let nextId = 1;

  export let visHandler;
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
  <form name="visitor-form" id="visitorForm">
    <Input
      label="Visitor Name"
      type="select"
      required
      name="Name"
      id="visName"
      bind:value={visName}
      className="visName"
      onInput={setVisName} />

    {#if visName === 'Guest Visitor'}
      <Input
        label="Guest Name"
        id="guest"
        type="text"
        placeholder="Guest Name"
        bind:value={guestVisName}
        className="guestName"
        name="Other"
        onInput={setGuestVisName} />
    {/if}
    <Input
      label="Location"
      type="text"
      id="visPlace"
      name="Location"
      className="visPlace"
      bind:value={visPlace}
      onInput={setVisPlace} />
    <button
      form="visitor-form"
      type="submit"
      class="visitor-form"
      id="visitorForm"
      on:click={visHandler}>
      Add
    </button>
  </form>
</div>
