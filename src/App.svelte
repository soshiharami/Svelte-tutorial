<div>
	<ul>
		<li><Router {routes}/></li>
	</ul>
</div>

<script>
    import Router from 'svelte-spa-router'
    import ToDoList from './ToDoList.svelte'
	import home from './home.svelte'
    import Addition from './Addition.svelte'
    import snake from './snake.svelte'

    const routes = {
        '/': home,
        '/ToDoList': ToDoList,
	    '/Addition': Addition,
	    '/snake': snake
    }
</script>
<style>
	ul{
		list-style: none;
	}
</style>
