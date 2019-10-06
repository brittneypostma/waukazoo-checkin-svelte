<script>
  import { onMount } from "svelte";

  import Input from "./Input.svelte";

  export let volHandler;

  let volName = "";
  let volPlace = "";
  let guestVolName = "";
  const setVolName = e => (volName = e.target.value);
  const setVolPlace = e => (volPlace = e.target.value);
  const setGuestVolName = e => (guestVolName = e.target.value);

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

  const addName = e => {
    if (e.key === "Enter") {
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
    }
  };
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
      name="Name"
      required
      bind:value={volName}
      className="volName"
      onInput={setVolName} />

    {#if volName === 'Guest Visitor'}
      <Input
        label="Guest Name"
        id="guest"
        type="text"
        placeholder="Guest Name"
        bind:value={guestVolName}
        className="guestName"
        name="Other"
        onInput={setGuestVolName} />
    {/if}

    <Input
      label="Location"
      type="text"
      id="place"
      name="Location"
      className="place"
      bind:value={volPlace}
      onInput={setVolPlace} />
    <br />
    <button
      form="test-form"
      type="submit"
      class="submit"
      id="postForm"
      on:click={volHandler}>
      Submit
    </button>
  </form>
</div>
