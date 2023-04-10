<script>
    import SubmitField from "./SubmitField.svelte";
    import Item from "./Item.svelte";

    let todos = [];
    let idCounter = 1;
    let currentPage = 1;
    let todosPerPage = 4;

    function handleInput(event) {
        addTodo(event.detail);
    }
    function addTodo(inputVal) {
        todos = [...todos, { id: idCounter, inputValue: inputVal }];
        idCounter++;
    }
    function handleRemove(event) {
        removeItem(event.detail);
    }
    function removeItem(id) {
        todos = todos.filter((todo) => todo.id !== id);
    }

    $: start = (currentPage - 1) * todosPerPage;
    $: end = start + todosPerPage;
    $: currentTodos = todos.slice(start, end);

    function nextPage() {
        if (currentPage < Math.ceil(todos.length / todosPerPage)) {
            currentPage += 1;
        }
    }

    function prevPage() {
        if (currentPage > 1) {
            currentPage -= 1;
        }
    }
</script>

<div class="flex flex-col items-center m-10">
    <div class="bg-orange-500 px-10 py-4 rounded-md text-white text-center min-w-[18rem]">
        <h1 class="uppercase text-2xl font-bold">svelte todo app</h1>
        <p class="mb-0">current todos:</p>
    </div>
    <div class="border border-orange-200 p-4 m-4 min-w-[18rem] min-h-[22rem] flex flex-col justify-between rounded-md">
        <ul>
            {#if todos.length === 0}
                <li
                    class="border border-gray-100 p-4 my-2 rounded-md flex justify-between items-center text-gray-400"
                >
                    No todos yet!
                </li>
            {:else if todos.length > todosPerPage}
                {#each currentTodos as todo}
                    <Item
                        itemName={todo.inputValue}
                        id={todo.id}
                        on:removeItem={handleRemove}
                    />
                {/each}
            {:else}
                {#each todos as todo, i}
                    <Item
                        itemName={todo.inputValue}
                        id={todo.id}
                        on:removeItem={handleRemove}
                    />
                {/each}
            {/if}
        </ul>
        {#if todos.length > todosPerPage}
            <div class="flex justify-end gap-x-2">
                {#if currentPage > 1}
                    <button
                        class="bg-orange-500 py-1 w-[5rem] rounded-md font-semibold text-white hover:bg-orange-400 transition duration-200 ease-in-out"
                        on:click={prevPage}
                    >
                        Previous
                    </button>
                    <button
                        class="disabled:bg-orange-200 hover:cursor-default py-1 w-[5rem] rounded-md font-semibold text-white bg-orange-200"
                        on:click={nextPage}
                    >
                        Next
                    </button>
                {/if}
                {#if currentPage < Math.ceil(todos.length / todosPerPage)}
                    <button
                        class="disabled:bg-orange-200 hover:cursor-default py-1 w-[5rem] rounded-md font-semibold text-white bg-orange-200"
                        on:click={nextPage}
                    >
                        Previous
                    </button>
                    <button
                        class="bg-orange-500 py-1 w-[5rem] rounded-md font-semibold text-white hover:bg-orange-400 transition duration-200 ease-in-out"
                        on:click={nextPage}
                    >
                        Next
                    </button>
                {/if}
            </div>
        {/if}
    </div>

    <SubmitField on:inputValue={handleInput} />
</div>
