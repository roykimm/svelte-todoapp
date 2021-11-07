<script>
    import TodoList from "../components/TodoList.svelte";
    import Header from "../components/Header.svelte";
    import Footer from "../components/Footer.svelte";
</script>

<div class="bg-gray-300  min-h-full">
    <Header />
    <div class="container mx-auto">
        <TodoList />
    </div>
    <Footer />
</div>
