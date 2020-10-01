<body class="main">
	<div class="filter">
		絞り込み:
		<button on:click={() => { condition = null }}>すべて</button>
		<button on:click={() => { condition = false }}>未完了</button>
		<button on:click={() => { condition = true }}>完了</button>
	</div>
	<div>
		<div class="cp_iptxt">
			<label>
				<input class="ef" type="text" placeholder="" bind:this={initFocus} bind:value={title}>
			</label>
			<label>やること</label>
			<span class="focus_line"><i></i></span>
		</div>
		<button on:click={() => add()} class="add">タスク追加</button>

	</div>
<div>
	<ul>
		{#each filteredTodoList(todoList, condition) as todo (todo.id)}
			<li>
				<label>
					<input type="checkbox" bind:checked={todo.done} onchange={localStorage.setItem("ToDo", JSON.stringify(todoList))}>
					{todo.title}
				</label>
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

	let todoList = JSON.parse(localStorage.getItem("ToDo"));

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

   :global(body) {
        background-color: #ababab;
        font-size:100%;
	    font-family: 'Playfair Display', serif;
        line-height:1.5;
	    font-weight: 900;
	    color:#333333;
    }

    .add {
        display: block;
        background-color: rgb(75, 168, 51);
        border: none;
        box-shadow: 0 0 6px rgba(0, 0, 0, 0.3);
        color: white;
        font-size: 1.5em;
        width: 20%;
        padding: 0.5em 0;
        margin: 1em 0;
        cursor: pointer;
    }

   .main {
        display: inline-block;
        background-color : #f4f4f4;
        background-image: linear-gradient(top , #C2C2C2, #F0F0F0);
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

</style>
