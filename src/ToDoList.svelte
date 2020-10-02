<body class="main">
	<div class="filter">
		絞り込み:
		<button class="button" on:click={() => { condition = null }}>すべて</button>
		<button class="button" on:click={() => { condition = false }}>未完了</button>
		<button class="button" on:click={() => { condition = true }}>完了</button>
	</div>
	<div class="add-todo">

		<input bind:this={initFocus} bind:value={title} class="textbox" placeholder="" type="text">
		<button class="add" on:click={() => add()}>タスク追加</button>

	</div>
	<div>
		<ul>
			{#each filteredTodoList(todoList.filter(t => t.delete === false), condition) as todo (todo.id)}
				<li>
					<input type="checkbox" bind:checked={todo.done}
					       onchange={localStorage.setItem("ToDo", JSON.stringify(todoList))}>
					{todo.title}
					<a on:click={todo.delete = true}><img src={GomiSvg} width="50" height="20" alt="gomi"></a>
				</li>
			{/each}
		</ul>
		<h4> 合計: {todoList.length}
			未完了: {todoList.filter(t => t.done === false).length}
			完了済み: {todoList.filter(t => t.done === true).length}
		</h4>
	</div>
</body>

<script>
	import {onMount} from "svelte";
	import GomiSvg from "../img/gomi.svg"

	let todoList = JSON.parse(localStorage.getItem("ToDo"));

	function gomi(todo){
		todo.delete = true;
	}

	onMount(() => {
		init()
	})

	let initFocus = null;

	function init() {
		title = ''
		initFocus.focus()
		localStorage.setItem("ToDo", JSON.stringify(todoList))
	}

	let title = ''

	function add() {
		if (title === '') return;
		todoList = [...todoList,
			{
				id: todoList.length,
				done: false,
				delete: false,
				title
			}]
		init()
		console.log(JSON.parse(localStorage.getItem("ToDo")) || "null")
	}

	let condition = false;

	function filteredTodoList(todoList, condition) {
		return condition === null ? todoList : todoList.filter(t => t.done === condition)
	}

</script>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600&display=swap" rel="stylesheet">
<style>

	.add-todo {
		overflow: hidden;
	}

	.add {
		background-color: rgb(75, 168, 51);
		border: none;
		box-shadow: 0 0 6px rgba(0, 0, 0, 0.3);
		color: white;
		font-size: 1.0em;
		width: 150px;
		margin: 1.0em;
		cursor: pointer;
		border-radius: 10px;
		padding: 20px;
	}

	.main {
		font-family: cursive;
		display: inline-block;
		background-color: #f4f4f4;
		background-image: linear-gradient(top, #C2C2C2, #F0F0F0);
		box-shadow: 0 3px 1px #EEEEEE, 0 3px 1px #B7B7B7 inset;
		padding: 20px;
	}

	.filter {
		background-color: rgb(62, 68, 163);
		border: none;
		border-radius: 3px;
		color: white;
		font-size: 1em;
		padding: 0.5em 1em;
		cursor: pointer;
	}


	.button {
		border-radius: 10px;
		color: rgba(30, 22, 54, 0.6);
		box-shadow: rgba(30, 22, 54, 0.4) 0 0px 0px 2px inset;
		-webkit-transition: all 200ms cubic-bezier(0.390, 0.500, 0.150, 1.360);
		-moz-transition: all 200ms cubic-bezier(0.390, 0.500, 0.150, 1.360);
		-ms-transition: all 200ms cubic-bezier(0.390, 0.500, 0.150, 1.360);
		-o-transition: all 200ms cubic-bezier(0.390, 0.500, 0.150, 1.360);
		transition: all 200ms cubic-bezier(0.390, 0.500, 0.150, 1.360);
		text-decoration: none;
		padding: 15px 20px;
		white-space: nowrap;
		margin: 5px;
	}

	.button:hover {
		color: rgba(255, 255, 255, 0.85);
		box-shadow: rgba(30, 22, 54, 0.7) 0 0px 0px 40px inset;
	}

	*::-webkit-input-placeholder {
		color: #fff;
	}

	*:-moz-placeholder {
		color: #fff;
	}

	*::-moz-placeholder {
		color: #fff;
	}

	*:-ms-input-placeholder {
		color: #fff;
	}

	.textbox {
		margin-top: 50px;
		font-family: cursive;
		font-size: 150%;
		border: 1px solid #acacac;
		color: #fff;
		opacity: .7;
		border-radius: 10px;
		padding: 20px;
		text-align: center;
		width: 400px;
		transition: all .3s;
		-webkit-transition: all .3s;
		-moz-transition: all .3s;
		outline: none;
		background-color: #acacac;
	}

	.textbox:focus {
		width: 500px;
		outline: none;
	}
</style>
