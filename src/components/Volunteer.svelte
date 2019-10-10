<script>
  import { onMount } from "svelte";

  import Input from "./Input.svelte";

  const date = new Date();
  const dd = date.getDate();
  const mm = date.getMonth() + 1;
  const yy = date.getFullYear();
  const today = `${mm}/${dd}/${yy}`;
  const time = date.toLocaleTimeString([], {
    hour: "2-digit",
    minute: "2-digit"
  });

  let volName = "";
  let volPlace = "";
  let guestVolName = "";

  const setVolName = e => (volName = e.target.value);
  const setVolPlace = e => (volPlace = e.target.value);
  const setGuestVolName = e => (guestVolName = e.target.value);

  const handleSubmit = () => {
    const selName = document.getElementById("volunteersList");
    const guestInput = document.getElementById("guest");
    const location = document.getElementById("place");
    if (selName.selectedIndex < 1) {
      alert("Please select your name.");
      selName.focus();
      return false;
    } else if (guestInput.innerText === "") {
      alert("Please select your name.");
      guestName.focus();
      return false;
    } else if (location.value.length < 1) {
      alert("Please input your location.");
      location.focus();
      return false;
    }
  };

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
    align-self: center;
    background-color: white;
    margin: 0 auto;
    width: 50vw;
    border-radius: 10px;
    padding: 0 0.5em;
  }
  #test-form {
    display: grid;
    align-items: center;
    justify-content: center;
    grid-gap: 10px;
  }
  #postForm {
    width: 100%;
  }

  button {
    background-color: transparent;
    border: 2px solid #e74c3c;
    color: #e74c3c;
    cursor: pointer;
    font-size: 1rem;
    line-height: 1;
    padding: 1.2em 2.8em;
    text-decoration: none;
    text-align: center;
    text-transform: uppercase;
    font-weight: 700;
    transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
  }

  button:hover,
  :focus {
    color: #fff;
    outline: 0;
    box-shadow: 0 0 40px 40px #e74c3c inset, 0 14px 28px rgba(0, 0, 0, 0.25),
      0 10px 10px rgba(0, 0, 0, 0.22);
  }

  .date {
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>

<div class="form">

  <form name="submit-to-google-sheet" id="test-form">
    <div class="date">
      <h2>{today}</h2>
      <h2>Volunteer Check In</h2>
      <h2>{time}</h2>
    </div>

    <Input
      label="Volunteer Name"
      id="volunteersList"
      type="text"
      name="Name"
      placeholder="&#x1F50D; Search Names..."
      required="true"
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
      required="true"
      className="place"
      bind:value={volPlace}
      onInput={setVolPlace} />
    <br />
    <button
      form="test-form"
      type="submit"
      id="postForm"
      on:click={handleSubmit}>
      Submit
    </button>

    <p style="color: red;">
      **If the visitor is not in the system, use the Guest Visitor name and a
      new input box will come up for the guests name.
    </p>
  </form>

</div>
