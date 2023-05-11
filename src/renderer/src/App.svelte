<script>
	import TodoList from '@/lib/TodoList.svelte';
	import ItemInput from '@/lib/ItemInput.svelte';

	let items = ["First task", "Second task", "Third task"];

	function addItem(item) {
		items = [...items, item];
	}
	function editItem(index, value){
		items[index] = value;
	}
	function removeItem(index) {
		if(!confirm("Do you want to delete?")) return;
		items = items.filter((_, i) => i !== index);
	}
</script>

<main>
	<ItemInput onAdd={addItem} />
	<TodoList {items} onEdit={editItem} onRemove={removeItem} />
</main>

<style>
	main {
		background-color: lightblue;
		margin: 0;
		padding: 15px;
		min-height: calc(100vh - 30px);
	}
	:global(body) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
</style>
