<script>
    import Item from "./Item.svelte";

    let todos = [
        {
            id: 1,
            inputValue: "tidy room",
        },
        {
            id: 2,
            inputValue: "do laundry",
        },
        {
            id: 3,
            inputValue: "buy groceries",
        },
    ];

    function addTodo() {
        todos = [ todos.concat({ id: 4, inputValue: "" })]
    }

</script>

<div class="border p-4 m-4 min-w-[18rem] rounded-md">
    <ul>
        {#each todos as todo}
            <Item itemName={todo.inputValue} />
        {/each}
    </ul>
</div>
