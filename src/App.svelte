<script>
  import Volunteer from "./components/Volunteer.svelte";
</script>

<style>
  .body {
    display: grid;
    overflow: none;
    height: 100%;
    grid-template-rows: 200px 1fr;
    font-family: "Montserrat", sans-serif;
  }

  header {
    height: 200px;
    color: #111;
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-content: space-between;
    align-items: center;
    align-content: center;
    padding: 0 1em;
  }

  .logo {
    justify-self: flex-end;
    width: 200px;
    height: 200px;
  }

  main {
    background-color: #111;
    display: grid;
    text-align: center;
    align-content: center;
  }

  p {
    color: white;
    font-size: 1.1em;
  }
</style>

<div class="body">
  <header class="header">
    <div class="school">
      <h1>
        Waukazoo Elementary
        <br />
        <span>Visitor Check In</span>
      </h1>
    </div>

    <img src="./logo.png" alt="logo" class="logo" />
  </header>
  <main>

    <p>
      If you are not volunteering, please use the book to sign in.
      <br />
      (ie. visiting for lunch, dropping off something, picking up)
    </p>
    <Volunteer />
  </main>
</div>
