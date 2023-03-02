<script>
    import {Link} from "svelte-routing"
</script>
<nav>
	<ul>
		<li><Link to="/">Inicio</Link></li>
		<li><Link to="/articulos">Articulos</Link></li>
		<li><Link to="/clientes">Clientes</Link></li>
	</ul>
</nav>
<style>
    ul{
        display: flex;
        justify-content: space-around;
        list-style: none;
        text-decoration: none;
        margin-top: 3em;
        
    }
    
</style>