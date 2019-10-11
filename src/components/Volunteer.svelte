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
  let checkIn = true;

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
    } else if (location.value.length < 1) {
      alert("Please input your location.");
      location.focus();
      return false;
    }
  };

  const checkOut = () => {
    checkIn = !checkIn;
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
</script>

<style>
  .form {
    align-self: center;
    background-color: white;
    margin: 0 auto;
    width: 50vw;
    border-radius: 10px;
    padding: 0 0.5em;
    max-height: 60vh;
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
    border: 2px solid #1e90ec;
    color: #1e90ec;
    cursor: pointer;
    font-size: 16px;
    line-height: 1;
    padding: 16px;
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
    box-shadow: 0 0 40px 40px #1e90ec inset, 0 14px 28px rgba(0, 0, 0, 0.25),
      0 10px 10px rgba(0, 0, 0, 0.22);
  }

  .date {
    margin: 0 0 -20px;
    padding: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .squaredTwo {
    display: flex;
    width: 28px;
    height: 28px;
    position: relative;
    margin: 0 auto;
    background: #fcfff4;
    background: linear-gradient(
      to bottom,
      #fcfff4 0%,
      #dfe5d7 40%,
      #b3bead 100%
    );
    box-shadow: inset 0px 1px 1px white, 0px 1px 3px rgba(0, 0, 0, 0.5);
  }
  .squaredTwo label {
    width: 20px;
    height: 20px;
    cursor: pointer;
    position: absolute;
    left: 4px;
    top: 4px;
    background: linear-gradient(to bottom, #222222 0%, #45484d 100%);
    box-shadow: inset 0px 1px 1px rgba(0, 0, 0, 0.5), 0px 1px 0px white;
  }
  .squaredTwo label:after {
    content: "";
    width: 9px;
    height: 5px;
    position: absolute;
    top: 4px;
    left: 4px;
    border: 3px solid #fcfff4;
    border-top: none;
    border-right: none;
    background: transparent;
    opacity: 0;
    -webkit-transform: rotate(-45deg);
    transform: rotate(-45deg);
  }
  .squaredTwo label:hover::after {
    opacity: 0.3;
  }
  .squaredTwo input[type="checkbox"] {
    visibility: hidden;
  }
  .squaredTwo input[type="checkbox"]:checked + label:after {
    opacity: 1;
  }

  .checkOut {
    width: 100%;
    position: relative;
    margin: 0;
  }

  .checkContainer {
    margin: 0 auto;
    display: grid;
    grid-template-columns: 250px 20px;
    align-items: center;
    color: red;
  }
</style>

<div class="form">

  <form name="submit-to-google-sheet" id="test-form">
    <div class="date">
      <h2>{today}</h2>
      <h2>Volunteer Check In</h2>
      <h2>{time}</h2>
    </div>
    <div class="checkContainer">
      <div>
        <h3 class="checkOut">Check Box To Check Out</h3>
      </div>
      <div class="squaredTwo">
        <input
          type="checkbox"
          value="None"
          id="squaredTwo"
          name="check"
          on:click={checkOut} />
        <label for="squaredTwo" />
      </div>
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
        required="true"
        placeholder="Guest Name"
        bind:value={guestVolName}
        className="guestName"
        name="Other"
        onInput={setGuestVolName} />
    {/if}

    {#if checkIn}
      <Input
        label="Location"
        type="text"
        id="place"
        name="Location"
        required="true"
        className="place"
        bind:value={volPlace}
        onInput={setVolPlace} />
    {/if}
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
