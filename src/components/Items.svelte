<script>
    export let id, text, completed;
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    function triggerUpdate() {
        dispatch("update", { id, text, completed });
    }

    function handleDoubleClick() {
        const yes = confirm("아이템을 삭제 하시겠습니까?");

        if (yes) {
            dispatch("delete", id);
        }
    }
</script>

<div
    class={`group flex align-center  hover:bg-blue-100 justify-center py-3 px-3 my-2 ${
        completed ? "bg-gray-500 line-through " : "bg-white"
    }`}
    on:dblclick={handleDoubleClick}
>
    <input
        class={`flex-grow font-bold text-md bg-none border-0 outline-none group-hover:bg-blue-100 ${
            completed ? "bg-gray-500 text-gray-300" : "bg-white"
        }`}
        type="text"
        bind:value={text}
        readonly={completed}
        on:keyup={({ key, target }) => key === "Enter" && target.blur()}
        on:blur={() => triggerUpdate()}
    />
    <input
        class="m-2 text-justify"
        type="checkbox"
        bind:checked={completed}
        on:change={() => triggerUpdate()}
    />
</div>
