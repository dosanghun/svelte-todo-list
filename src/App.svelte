<script lang="ts">
	import NavBar from "./components/NavBar.svelte";
	import TodoList from "./components/TodoList.svelte";
	import TodoInput from "./components/TodoInput.svelte";

	let todos = [
		{ id: 0, checked: false, text: "finish Svelte tutorial" },
		{ id: 1, checked: false, text: "build an app" },
		{ id: 2, checked: false, text: "world domination" },
	];

	const onHandleCheck = (id: number) => {
		const index = todos.findIndex((t) => t.id === id);
		todos[index].checked = !todos[index]?.checked;
	};

	const onHandleRemove = (id: number) => {
		todos = todos.filter((t) => t.id !== id);
	};

	const onHandleModify = (id: number, text: string) => {
		const index = todos.findIndex((t) => t.id === id);
		todos[index].text = text;
	};

	let todoInput = "";
	const onHandleAdd = () => {
		if (!todoInput) return;

		const newTodo = {
			id: ++lastId,
			checked: false,
			text: todoInput,
		};

		todos = [...todos, newTodo];

		todoInput = "";
	};

	const onHandleKeyup = (e) => {
		todoInput = e.target.value;
		if (e.keyCode === 13) onHandleAdd();
	};

	$: lastId = todos[todos.length - 1]?.id || 0;
</script>

<section class="hero is-primary is-fullheight">
	<div class="hero-head">
		<NavBar />
	</div>

	<div class="hero-body">
		<div class="container has-text-centered">
			<div class="columns is-desktop">
				<div class="column" />
				<div class="column">
					<h1 class="title">Todo List</h1>
					<h2 class="subtitle">Built with Svelte, Bulma</h2>
					<TodoInput {todoInput} {onHandleKeyup} {onHandleAdd} />
					<TodoList
						{todos}
						{onHandleCheck}
						{onHandleRemove}
						{onHandleModify}
					/>
				</div>
				<div class="column" />
			</div>
		</div>
	</div>
</section>
