<script>
    import { getContext, setContext } from "svelte";
    import { onMount } from "svelte";
    import Articulo from "./articulo.svelte";
    import Boton from "./Boton.svelte";
    import Buscar from "./buscar.svelte";
    import { data } from "./store";
    let articuloInsertar = {}
    let datosFiltrados = [];
    let patron = "";
    const URL = getContext("URL");

    let getArticulos = async () => {
        const response = await fetch(URL.articulos);
        $data = await response.json();
    };
    

    onMount(getArticulos);
    $: datosFiltrados = $data.filter((articulo) =>
        RegExp(patron, "i").test(articulo.nombre)
    );
</script>

<h1>Articulos</h1>
<Buscar bind:busqueda={patron} />
<hr />

<Articulo bind:articulo = {articuloInsertar}>
<Boton documento = {articuloInsertar}/>
</Articulo>
<br /><br />
<ul>
    {#each datosFiltrados as articulo}
        <Articulo bind:articulo = {articulo} >
        <br />
        
        <Boton tipo = "🔄" documento = {articulo}/>
        <Boton tipo = "❌" documento = {articulo}/>
        <br /><br />
    </Articulo>
    {/each}
</ul>

<style>
    h1 {
        margin: 50px;
    }
</style>
