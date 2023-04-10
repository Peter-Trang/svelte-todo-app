<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();
    let inputField;
    let inputValue = "";

    function submit() {
        dispatch("inputValue", inputValue);
        inputField.value = "";
    }
</script>

<div class="border p-4 rounded-md min-w-[18rem] flex justify-between">
    <input
        bind:this={inputField}
        type="text"
        bind:value={inputValue}
        placeholder="Add your todo..."
        class="focus:!outline-none border p-2 rounded-md"
        on:keydown={(e) => {
            if (e.key === "Enter") {
                submit();
            }
        }}
    />
    <button
        on:click={submit}
        class="bg-orange-500 border-none hover:bg-orange-400 h-11 px-4 rounded-md transition duration-200 ease-in-out"
    >
        <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="white"
            height="12"
            viewBox="0 0 448 512"
            ><path
                d="M256 80c0-17.7-14.3-32-32-32s-32 14.3-32 32V224H48c-17.7 0-32 14.3-32 32s14.3 32 32 32H192V432c0 17.7 14.3 32 32 32s32-14.3 32-32V288H400c17.7 0 32-14.3 32-32s-14.3-32-32-32H256V80z"
            /></svg
        >
    </button>
</div>
