<script>
  import { onMount } from "svelte";

  let volName = "";
  let volPlace = "";
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
    <label for="volName">Name</label>
    <input
      type="text"
      id="name"
      name="Name"
      value={volName}
      on:input={setVolName} />

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
