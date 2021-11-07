<script>
    import { onMount } from "svelte";
    import { v4 as uuidv4 } from "uuid";
    import { items } from "../stores/stores";
    import TodoApi from "../django/TodoApi";
    import Items from "./Items.svelte";
    import NewItem from "./NewItem.svelte";

    function handleNewItem(e) {
        $items = [
            {
                id: uuidv4(),
                text: e.detail,
                completed: false,
            },
            ...$items,
        ];

        TodoApi.save($items);
    }

    function handleUpdate(e) {
        const index = $items.findIndex((item) => item.id === e.detail.id);

        $items[index] = e.detail;
        TodoApi.save($items);
    }

    function handleDelete(e) {
        $items = $items.filter((item) => item.id !== e.detail);
        TodoApi.save($items);
    }

    let itemsSorted = [];

    $: {
        itemsSorted = [...$items];
        itemsSorted.sort((a, b) => {
            if (a.completed && b.completed) return 0;
            if (a.completed) return 1;
            if (b.completed) return -1;
        });
    }

    onMount(async () => {
        // fetch from API
        $items = await TodoApi.getAll();
    });
</script>

<div class="p-3">
    <p class="py-2">더블 클릭 하시면 아이템이 삭제 됩니다.</p>
    <NewItem on:newItem={handleNewItem} />
    {#each itemsSorted as item (item.id)}
        <Items {...item} on:update={handleUpdate} on:delete={handleDelete} />
    {:else}
        <p class="m-0 text-center text-gray-200 font-bold font-3xl">
            리스트가 없습니다. 할일을 추가해 주세요.
        </p>
    {/each}
</div>
