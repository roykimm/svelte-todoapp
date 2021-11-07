<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();
    let value = "";

    function handleKeyUp({ key }) {
        if (key !== "Enter" || value.length === 0) return;
        dispatch("newItem", value);
        value = "";
    }
</script>

<input
    class="box-border mb-3 p-3 border-none outline-none w-full bg-gray-600 text-white cursor-pointer"
    type="text"
    on:keyup={handleKeyUp}
    bind:value
    placeholder="+ 아이템 추가"
/>
