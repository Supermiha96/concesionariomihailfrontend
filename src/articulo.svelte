<script>
    export let articulo = {"nombre" : "","precio" :0}
</script>

<input type="text" placeholder="Nombre" bind:value={articulo.nombre}/>
<input type="number" placeholder="Precio" bind:value={articulo.precio} />
<slot />