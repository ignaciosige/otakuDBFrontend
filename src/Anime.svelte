<script>
  export let anime = {};

  /* let splitDate = anime.fechaSalida.split("T");
  let date      = splitDate[0].split("-");
  let fecha     = date[2] + '/' + date[1] + '/' + date[0]; */

    let fecha       = new Date(anime.fechaSalida);
    let fechaSalida = ("0" + fecha.getDate()).slice(-2) + '/' + ("0" + (fecha.getMonth() + 1)).slice(-2) + '/' + fecha.getFullYear();
 
 </script>

<style>
  .title {
    font-weight: bold;
  }
  .card {
    background-color: #fdebc9;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    border-radius: 5px;
    transition: 0.3s;
    padding: 10px;
    margin: 10px;
  }

  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.4);
  }

  input {
    background-color: inherit;
    padding: 10px;
    font-size: 14px;
    color: black;
    border: 0;
    outline: none;
    margin-left: 5px;
    margin-bottom: 4px;
  }

  input[type="number"] {
    text-align: right;
    width: 150px;
  } 
  input:focus {
    background-color: wheat;
  }

  input:required:invalid,
  input:focus:invalid {
    background-color: lightpink;
  }
</style>

<div class="card" on:click>
  <input bind:value={anime.nombre} placeholder="Nombre" class="title" />
  <input type="text" bind:value={fechaSalida} placeholder="Fecha de Salida" class="title" />
  <input type="number" bind:value={anime.numeroEpisodios} placeholder="Nº Episodios" />
  <slot />
</div>
