<div>
	絞り込み:
	<button on:click={() => { condition = null }}>すべて</button>
	<button on:click={() => { condition = false }}>未完了</button>
	<button on:click={() => { condition = true }}>完了</button>
</div>
<div>
	<input bind:this={initFocus} bind:value={title} type="text">
	<button on:click={() => add()}>タスク追加</button>
</div>
<div>
	<ul>
		{#each filteredTodoList(todoList, condition) as todo (todo.id)}
			<li>
				<input type="checkbox" bind:checked={todo.done}>
				{todo.title}
			</li>
		{/each}
	</ul>
	{todoList.length}
</div>

<script>
    import {link} from 'svelte-spa-router'
    import {onMount} from "svelte";

    let condition = null;

    let todoList = [
        {id: 0, done: false, title: 'レストランを予約する'},
        {id: 1, done: false, title: 'サプライズ用の指輪を買う'},
        {id: 2, done: false, title: 'フラッシュモブダンスを練習する'},
        {id: 3, done: false, title: "test"}
    ]

    onMount(() => {
        init()
    })

    let initFocus = null;

    function init() {
        title = ''
        initFocus.focus()
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
        console.log(todoList)
        init()
    }

    $: filteredTodoList = (todoList, condition) => {
        return condition === null ? todoList : todoList.filter(t => t.done === condition)
    }

</script>

<style>
    /* TODO: CSS得意なフレンズに頼む */
    /* https://svelte.dev/tutorial/styling */
</style>
