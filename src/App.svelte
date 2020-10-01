<div>
	<ul>
		<li><Router {routes}/></li>
	</ul>
</div>

<script>
    import Router from 'svelte-spa-router'
    import ToDoList from './ToDoList.svelte'
	import home from './home.svelte'

    const routes = {
        '/': home,
        '/ToDoList': ToDoList,
    }
</script>
<style>

</style>
