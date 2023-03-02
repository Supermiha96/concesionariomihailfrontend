<script>
    export let cliente = {"nombre" : "","apellidos" :0}
</script>

<input type="text" placeholder="Nombre" bind:value={cliente.nombre}/>
<input type="text" placeholder="Apellidos" bind:value={cliente.apellidos} />
<slot />