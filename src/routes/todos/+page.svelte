<script lang="ts">
    import type { PageData } from './$types';
    
    export let data: PageData;

    // todo
    async function addTodo(event: Event) {}

    // todo
    async function removeTodo(event: Event) {}
</script>

<pre>
    {JSON.stringify(data, null, 2)}
</pre>

<ul>
    {#each data.todos as todo}
        <li>
            <span>{todo.text}</span>
            <form on:submit|preventDefault={removeTodo} method="POST">
                <input type="hidden" name="id" value={todo.id}>
                <button class="delete delete-blue" type="submit">Delete</button>
            </form>
        </li>
    {/each}
</ul>

<form on:submit|preventDefault={addTodo} method="POST">
    <input class="submit-box"type="text" name="todo" />
    <button class="submit-btn" type="submit">+ Add Todo</button>
</form>

<style>
    ul {
        padding: 0;
    }

    li {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    span {
        text-transform: capitalize;
    }

    .delete {
        @apply font-bold py-2 px-4 rounded;
    }

    .delete-blue {
        @apply bg-blue-500;
    }

    .delete-blue:hover {
        @apply bg-blue-700;
    }

    .submit-box {
        @apply block px-4 py-2 text-gray-700;
    }

    .error {
        color: tomato;
    }
</style>