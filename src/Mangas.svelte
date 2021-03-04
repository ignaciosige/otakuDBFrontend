<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Manga                from "./Manga.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let manga = {};

  onMount(async () => {
    const response = await fetch(URL.mangas);
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

<h1>MANGAS</h1>
<Buscar bind:busqueda />

<div class="container">
  <Manga bind:manga>
    <div style="text-align: right">
      <Boton documento={manga} tipo="insertar" coleccion="mangas" />
    </div>
  </Manga>
</div>

<div class="container">
  {#each datos as manga}
    <Manga {manga}>
      <div style="text-align: right">
        <Boton documento={manga} tipo="modificar" coleccion="mangas" />
        <Boton documento={manga} tipo="eliminar"  coleccion="mangas" />
      </div>
    </Manga>
  {/each}
</div>
