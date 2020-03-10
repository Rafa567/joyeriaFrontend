<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";
  import Buscar                  from "./Buscar.svelte";
  import Catalogo                from "./Catalogo.svelte";
  import Boton                   from "./Boton.svelte";
  const URL = getContext("URL");
  let busqueda = "";
  let catalogo = {};
  onMount(async () => {
    const response = await fetch(URL.catalogos);
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

<h1>CATALOGOS</h1>
<Buscar bind:busqueda />

<div class="container">
  <Catalogo bind:catalogo>
    <div style="text-align: right">
      <Boton documento={catalogo} tipo="insertar" coleccion="catalogos" />
    </div>
  </Catalogo>
</div>

<div class="container">
  {#each datos as catalogo}
    <Catalogo {catalogo}>
      <div style="text-align: right">
        <Boton documento={catalogo} tipo="modificar" coleccion="catalogos" />
        <Boton documento={catalogo} tipo="eliminar"  coleccion="catalogos" />
      </div>
    </Catalogo>
  {/each}
</div>