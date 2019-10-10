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

    <Volunteer />
  </main>
</div>
