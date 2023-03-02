<script>
	import { setContext } from "svelte";
	import Nav from "./Nav.svelte";
	import {Router} from "svelte-routing"
	import Contenido from "./Contenido.svelte";

	const URL = {
		articulos:"https://concesionariomihailbackend.herokuapp.com/api/coches",
		clientes:"https://concesionariomihailbackend.herokuapp.com/api/clientes"
	}
	setContext("URL",URL);
</script>
<header>
<h1>Concesionario Mihail</h1>
<Router>
	<Nav/>
	<Contenido/>
</Router>
</header>
<body class="">
	
</body>
<style>

:global(body){
		margin: 0%;
		padding: 0%;

	}
	h1{
		text-align: center;
		font-size: 50px;
		font-family: Verdana, Geneva, Tahoma, sans-serif;
	}
	:global(*){
		color: whitesmoke;

		background-color:#912376;
	}
	:global(a) {
	color: whitesmoke; 
	font-size: 20px;
	font-weight: bold;
	text-decoration: none;
}

:global(a:hover){
	text-decoration: underline;
	color: #2d572c;
}
	
</style>