<script>
    import { onMount } from "svelte";
    export let documento = {};
    export let tipo = "👇🏻";
    import { getContext } from "svelte";
    import { data } from "./store";
    let URL = getContext("URL");
    let handler = () => {};

    function insertar() {
        let opciones = {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.clientes, opciones)
            .then((res) => res.json())
            .then(doc=> $data = [... $data,doc])
            .catch((error) => console.log(error));
    }
    function modificar() {
        let opciones = {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.clientes + documento._id, opciones)
            .then((res) => res.json())
            .then((datos) => console.log(datos))
            .catch((error) => console.log(error));
    }
    function eliminar() {
        let opciones = {
            method: "DELETE",
        };
        fetch(URL.clientes + documento._id, opciones)
            .then((res) => res.json())
            .then($data = $data.filter(doc => doc._id != documento._id))
            .catch((error) => console.log(error));
    }
    function setup() {
        switch (tipo) {
            case "👇🏻":
                handler = insertar;
                break;
            case "🔄":
                handler = modificar;
                break;
            case "❌":
                handler = eliminar;
                break;
            default:
        }
    }

    onMount(setup);
</script>

<input class="botonCliente" type="button" value={tipo} on:click={handler} />

<style>
    .botonCliente {
  background: #2362c1;
  width: 100px;
}
.botonCliente:hover{
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.6);
  background: #fff;
  color: #000;
}
</style>