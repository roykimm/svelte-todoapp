<script>
    import { items } from "../stores/stores";
    import { fly } from "svelte/transition";
    let logo = "bellalogo.png";

    console.log($items);
    $: itemCount = $items.length;
    $: completedItemCount = $items.filter(
        (item) => item.completed !== true
    ).length;
</script>

<div
    class="flex justify-between align-center px-5 py-5 text-gray-500 font-bold text-xl bg-gray-400"
>
    <div class="flex">
        <img
            class="w-20 mx-5"
            in:fly={{ delay: 1000, x: 100 }}
            src={logo}
            alt="bella!"
        />
        <span>Bella's Todolist</span>
    </div>
    <span class="text-md">remains : {completedItemCount} / {itemCount}</span>
</div>
