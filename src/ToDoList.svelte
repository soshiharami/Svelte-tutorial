<body class="main">
	<div class="filter">
		絞り込み:
		<button on:click={() => { condition = null }}>すべて</button>
		<button on:click={() => { condition = false }}>未完了</button>
		<button on:click={() => { condition = true }}>完了</button>
	</div>
	<div>
		<div class="cp_iptxt">
			<input class="ef" type="text" placeholder="" bind:this={initFocus} bind:value={title}>
			<label>やること</label>
			<span class="focus_line"><i></i></span>
		</div>
		<button on:click={() => add()} class="add">タスク追加</button>

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
</body>

<script>
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

    :global(body) {
        background-color: #ababab;
        font-size:95%;
        font-family: "ＭＳ ゴシック",sans-serif;
        line-height:1.5;
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
        box-shadow: 0px 3px 1px #EEEEEE, 0px 3px 1px #B7B7B7 inset;
        padding: 20px;

    }

    .button-container {
        padding: 1em 0;
        text-align: right;
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

    .save:disabled {
        opacity: 0.3;
        cursor: auto;
    }

    .cp_iptxt {
        position: relative;
        width: 80%;
        margin: 40px 3%;
    }

    .cp_iptxt input[type='text'] {
        font: 15px/24px sans-serif;
        box-sizing: border-box;
        width: 100%;
        letter-spacing: 1px;
        padding-left: 4em;
    }

    .cp_iptxt input[type='text']:focus {
        outline: none;
    }

    .ef {
        padding: 7px 14px;
        transition: 0.4s;
        border: 1px solid #1b2538;
        background: transparent;
    }

    .ef ~ .focus_line:before,
    .ef ~ .focus_line:after {
        position: absolute;
        top: 0;
        right: 0;
        width: 0;
        height: 2px;
        content: '';
        transition: 0.2s;
        transition-delay: 0.2s;
        background-color: #da3c41;
    }

    .ef ~ .focus_line:after {
        top: auto;
        right: auto;
        bottom: 0;
        left: 0;
        transition-delay: 0.6s;
    }

    .ef ~ .focus_line i:before,
    .ef ~ .focus_line i:after {
        position: absolute;
        top: 0;
        left: 0;
        width: 2px;
        height: 0;
        content: '';
        transition: 0.2s;
        background-color: #da3c41;
    }

    .ef ~ .focus_line i:after {
        top: auto;
        right: 0;
        bottom: 0;
        left: auto;
        transition-delay: 0.4s;
    }

    .ef:focus ~ .focus_line:before,
    .ef:focus ~ .focus_line:after,
    .cp_iptxt.ef ~ .focus_line:before,
    .cp_iptxt.ef ~ .focus_line:after {
        width: 100%;
        transition: 0.2s;
        transition-delay: 0.6s;
    }

    .ef:focus ~ .focus_line:after,
    .cp_iptxt.ef ~ .focus_line:after {
        transition-delay: 0.2s;
    }

    .ef:focus ~ .focus_line i:before,
    .ef:focus ~ .focus_line i:after,
    .cp_iptxt.ef ~ .focus_line i:before,
    .cp_iptxt.ef ~ .focus_line i:after {
        height: 100%;
        transition: 0.2s;
    }

    .ef:focus ~ .focus_line i:after,
    .cp_iptxt.ef ~ .focus_line i:after {
        transition-delay: 0.4s;
    }

    .ef ~ label {
        position: absolute;
        z-index: -1;
        top: 10px;
        left: 14px;
        width: 100%;
        transition: 0.3s;
        letter-spacing: 0.5px;
        color: #aaaaaa;
    }

    .ef:focus ~ label, .cp_iptxt.ef ~ label {
        font-size: px;
        top: -18px;
        left: 0;
        transition: 0.3s;
        color: #da3c41;
    }
</style>
