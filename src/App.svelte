<script>
  import Volunteer from "./components/Volunteer.svelte";
</script>

<style>
  .body {
    display: grid;
    overflow: none;
    height: 100%;
    grid-template-rows: 200px 1fr;
  }

  header {
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
    width: 200px;
    height: 200px;
  }

  main {
    background-color: #111;
    display: grid;
    text-align: center;
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

    <img src="./logo.png" alt="logo" class="logo" />

  </header>
  <main>
    <Volunteer />
  </main>
</div>
