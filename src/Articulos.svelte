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
    let contador= 1;

    let getArticulos = async () => {
        const response = await fetch(URL.articulos);
        $data = await response.json();
    };
    

    onMount(getArticulos);
    $: datosFiltrados = $data.filter((articulo) =>
        RegExp(patron, "i").test(articulo.nombre)
    );
</script>
<div class="body">
<h1>Coches</h1>
<Buscar bind:busqueda={patron} />
<hr />
<div class="insertar">
    <h3>Insertar coche</h3>
<Articulo bind:articulo = {articuloInsertar}>
<Boton documento = {articuloInsertar}/>
</Articulo>
</div>
<br /><br />
<ul>
    {#each datosFiltrados as articulo,i}
        <br /><br />

    <div class="container">
        <div class="card">
          <div class="box">
            <div class="content">
                <h2>{i+1}</h2>
              <h3>Coche</h3>
              <Articulo bind:articulo = {articulo} >
                <br />
              <Boton tipo = "🔄" documento = {articulo}/>
              <br/>
              <Boton tipo = "❌" documento = {articulo}/>
            </Articulo>
            </div>
          </div>
        </div>
    </div>
    
    {/each}
</ul>
</div>
<style>
    h1 {
        margin: 50px;
    }
    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;700;800&display=swap");

ul{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
.body .container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  max-width: 1200px;
  margin: 40px 0;
}

.body .container .card {
  position: relative;
  min-width: 320px;
  height: 440px;
  box-shadow: inset 5px 5px 5px rgba(0, 0, 0, 0.2),
    inset -5px -5px 15px rgba(255, 255, 255, 0.1),
    5px 5px 15px rgba(0, 0, 0, 0.3), -5px -5px 15px rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  margin: 30px;
  transition: 0.5s;
}

.body .container .card .box {
  position: absolute;
  top: 20px;
  left: 20px;
  right: 20px;
  bottom: 20px;
  background: #2a2b2f;
  border-radius: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  transition: 0.5s;
}

.body .container .card .box:hover {
  transform: translateY(-50px);
}

.body .container .card .box:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 50%;
  height: 100%;
  background: rgba(255, 255, 255, 0.03);
}

.body .container .card .box .content {
  padding: 20px;
  text-align: center;
}

.body .container .card .box .content h2 {
    position: absolute;
    top: -118px;
    right: 30px;
    font-size: 7rem;
    color: rgba(255, 255, 255, 0.1);
}

.body .container .card .box .content h3 {
  font-size: 1.8rem;
  color: #fff;
  z-index: 1;
  transition: 0.5s;
  margin-bottom: 15px;
}

</style>
