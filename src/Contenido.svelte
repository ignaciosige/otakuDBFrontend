<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Mangas  from "./Mangas.svelte";
  import Animes   from "./Animes.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/mangas" component={Mangas} />
  <Route path="/animes" component={Animes} />
</main>
