<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Catalogos  from "./Catalogos.svelte";
  import Clientes   from "./Clientes.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/catalogos" component={Catalogos} />
  <Route path="/clientes" component={Clientes} />
</main>
© 2020 GitHub, Inc.