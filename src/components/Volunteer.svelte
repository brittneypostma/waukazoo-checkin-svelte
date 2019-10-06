<script>
  import { onMount } from "svelte";

  import Input from "./Input.svelte";

  let volName = "";
  let volPlace = "";
  let guestVolName = "";
  const setVolName = e => (volName = e.target.value);
  const setVolPlace = e => (volPlace = e.target.value);

  onMount(() => {
    const scriptURL =
      "https://script.google.com/macros/s/AKfycbzrKqVJEidj98LDaebjqwQX4Ti5tjvWcx52oLBrQwKqDH29_uo/exec";
    const form = document.forms["submit-to-google-sheet"];
    form.addEventListener("submit", e => {
      e.preventDefault();

      fetch(scriptURL, {
        method: "POST",
        body: new FormData(form)
      });
      document.getElementById("test-form").reset();
    });
  });
</script>

<style>
  .form {
    display: grid;
    align-items: center;
    justify-content: center;
    grid-gap: 10px;
  }
  #postForm {
    width: 100%;
  }
</style>

<div class="form">
  <h2>Volunteer</h2>
  <form name="submit-to-google-sheet" id="test-form">
    <Input
      label="Volunteer Name"
      id="volunteersList"
      type="select"
      required
      bind:value={volName}
      onInput={setVolName} />

    {#if volName === 'Guest Visitor'}
      <label for="guest">Guest Name</label>
      <input
        id="guest"
        type="text"
        placeholder="Guest Name"
        bind:value={guestVolName}
        class="guest-name"
        name="Other" />
    {/if}
    <label for="volPlace">Location</label>
    <input
      type="text"
      id="place"
      name="Location"
      value={volPlace}
      on:input={setVolPlace} />
    <br />
    <button form="test-form" type="submit" class="submit btn-in" id="postForm">
      Submit
    </button>
  </form>
</div>
