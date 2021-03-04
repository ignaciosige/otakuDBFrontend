<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Anime                 from "./Anime.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let anime = {};

  onMount(async () => {
    const response = await fetch(URL.animes);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>ANIMES</h1>
<Buscar bind:busqueda />

<div class="container">
  <Anime bind:anime>
    <div style="text-align: right">
      <Boton documento={anime} tipo="insertar" coleccion="animes" />
    </div>
  </Anime>
</div>

<div class="container">
  {#each datos as anime}
    <Anime {anime}>
      <div style="text-align: right">
        <Boton documento={anime} tipo="modificar" coleccion="animes" />
        <Boton documento={anime} tipo="eliminar" coleccion="animes" />
      </div>
    </Anime>
  {/each}
</div>