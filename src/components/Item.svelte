<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    export let itemName = "todo item";
    export let id;
    function removeItem() {
        console.log(id);
        dispatch("removeItem", id);
    }
</script>

<li class="border border-orange-200 p-4 my-2 rounded-md flex justify-between items-center hover:bg-orange-100 hover:border-none hover:cursor-pointer transition duration-200 ease-in-out">
    <span class="max-w-[12rem] text-orange-900">{itemName}</span>
    <button on:click={removeItem} class="mr-1 hover:cursor-pointer">
        <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="orange"
            height="12"
            viewBox="0 0 384 512"
            ><path
                d="M342.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L192 210.7 86.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L146.7 256 41.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L192 301.3 297.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L237.3 256 342.6 150.6z"
            /></svg
        >
    </button>
</li>
