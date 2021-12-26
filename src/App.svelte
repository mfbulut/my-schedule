<script>
  import Clock from "./Clock.svelte";
  import Timetable from "./Timetable.svelte";
</script>

<main>
  <h1>9/A School Schedule</h1>
  <Clock />
  <Timetable />
</main>

<style>
  :global(body) {
    background-color: #eeeeee;
  }

  main {
    text-align: center;
  }

  h1 {
    color: #000000;
    text-transform: uppercase;
    font-family: Arial, sans-serif;
    font-size: 3em;
    font-weight: 100;
    padding-bottom: 0px;
  }

  @media only screen and (max-width: 600px) {
    h1 {
      font-size: 1.6em;
    }
  }
</style>
