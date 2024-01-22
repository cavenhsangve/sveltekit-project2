<script lang="ts">
	import { enhance } from '$app/forms';
    import type { ActionData } from './$types';
    
    export let form: ActionData;
</script>

<pre>
    {JSON.stringify(form, null, 2)}
</pre>

<form method="post" class="mt-10 space-y-4" use:enhance>
    <input 
        class="bg-inherit appearance-none border border-gray-200 rounded-lg w-full py-2 px-2 text-gray-300 leading-tight focus:border-2 focus:outline-none" 
        type="text" 
        name="user"
        value={form?.data?.user ?? ''} 
    />
    {#if form?.errors?.user}
        <p class="error">Name is required</p>
    {/if}
    
    <input 
        class="bg-inherit appearance-none border border-gray-200 rounded-lg w-full py-2 px-2 text-gray-300 leading-tight focus:border-2 focus:outline-none" 
        type="password" 
        name="password"
    />
    {#if form?.errors?.password}
        <p class="error">Password is required</p>
    {/if}

    <button class="shadow bg-blue-500 hover:bg-blue-400 focus:shadow-outline focus:outline-none font-bold py-2 px-4 rounded-lg w-full" type="submit">
        Login
    </button>
</form>

<style>
    .error {
        color: tomato;
    }
</style>
