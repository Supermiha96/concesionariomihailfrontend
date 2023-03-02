<script>
    import { getContext, setContext } from "svelte";
    import { onMount } from "svelte";
    import Cliente from "./cliente.svelte";
    import Boton from "./BotonCliente.svelte";
    import Buscar from "./buscar.svelte";
    import { data } from "./store";
    let clienteInsertar = {}
    let datosFiltrados = [];
    let patron = "";
    const URL = getContext("URL");

    let getClientes = async () => {
        const response = await fetch(URL.clientes);
        $data = await response.json();
    };
    

    onMount(getClientes);
    $: datosFiltrados = $data.filter((cliente) =>
        RegExp(patron, "i").test(cliente.nombre)
    );
</script>

<h1>Clientes</h1>
<Buscar bind:busqueda={patron} />
<hr />

<Cliente bind:cliente = {clienteInsertar}>
<Boton documento = {clienteInsertar}/>
</Cliente>
<br /><br />
<ul>
    {#each datosFiltrados as cliente}
        <Cliente bind:cliente = {cliente} >
        <br />
        
        <Boton tipo = "🔄" documento = {cliente}/>
        <Boton tipo = "❌" documento = {cliente}/>
        <br /><br />
    </Cliente>
    {/each}
</ul>

<style>
    h1 {
        margin: 50px;
    }
</style>