<script lang="ts">
	import { enhance } from '$app/forms';
	import { invalidateAll } from '$app/navigation';
	import type { SubmitFunction } from '@sveltejs/kit';
    import type { ActionData, PageData } from './$types';
    
    export let data: PageData;
    export let form: ActionData;

    let loading = false

    const addTodo: SubmitFunction = () => {
        // do smtg before the form submits
        loading = true

        return async ({update}) => {
            // do smtg after the form submits
            loading = false
            await update()
        }
    }
</script>

<pre>
    {JSON.stringify(data, null, 2)}
</pre>

<ul class="p-0">
    {#each data.todos as todo}
        <li class="flex justify-between items-center space-y-8">
            <span class="capitalize">{todo.text}</span>
            <!-- use:enchance: instead of refreshing the page when submitting form, use javascript -->
            <form method="POST" action="?/removeTodo" use:enhance> 
                <input type="hidden" name="id" value={todo.id}>
                <button class="font-bold py-1 px-2 rounded bg-blue-500 hover:bg-blue-400" type="submit">Delete</button>
            </form>
        </li>
    {/each}
</ul>

<form method="POST" action="?/addTodo" use:enhance={addTodo} class="mt-10 space-y-2">
    <input class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" type="text" name="todo" />
    {#if form?.missing}
        <p class="error text-red-700">This field is required</p>
    {/if}
    <button class="shadow bg-blue-500 hover:bg-blue-400 focus:shadow-outline focus:outline-none font-bold py-2 px-4 rounded w-full" type="submit">
        + Add Todo
    </button>
    <button formaction="?/clearTodos" class="shadow bg-slate-500 hover:bg-blue-400 focus:shadow-outline focus:outline-none font-bold py-2 px-4 rounded w-full" type="submit">Clear</button>
</form>

{#if form?.success}
    <p>Added todo!</p>
{/if}

<!-- <style>
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
</style> -->