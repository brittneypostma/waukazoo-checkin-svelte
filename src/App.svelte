<script>
  import Volunteer from "./components/Volunteer.svelte";
</script>

<style>
  .body {
    display: grid;
    overflow: none;
    height: 100%;
    grid-template-rows: 1fr 1fr;
  }

  header {
    width: 100%;
    color: #111;
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-content: space-between;
    padding: 0 1em;
  }

  .school {
    font-size: 2rem;
  }

  .logo {
    justify-self: flex-end;
  }

  main {
    background-color: #111;
  }
</style>

<div class="body">
  <header class="header">
    <div class="school">
      <h2>
        Waukazoo Elementary
        <br />
        <span>Visitor Check In</span>
      </h2>
    </div>
    <div class="logo">
      <img src="./logo.png" alt="logo" style=" height: 200px; width: 200px;" />
    </div>
  </header>
  <main>
    <Volunteer />
  </main>
</div>
