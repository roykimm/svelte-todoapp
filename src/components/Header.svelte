<script>
    import { items } from "../stores/stores";

    console.log($items);
    $: itemCount = $items.length;
    $: completedItemCount = $items.filter(
        (item) => item.completed !== true
    ).length;
</script>

<div
    class="flex justify-between align-center px-5 py-5 text-gray-500 font-bold text-xl bg-gray-400"
>
    <span>Bella's Todolist</span>
    <span class="text-md">remains : {completedItemCount} / {itemCount}</span>
</div>
