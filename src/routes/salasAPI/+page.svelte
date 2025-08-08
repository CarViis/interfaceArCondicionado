<script lang="ts">
    import { onMount } from "svelte";
    import { on } from "svelte/events";

    let Salas = $state([])
    async function load() { 
        try {
        const resposta = await fetch("https://6895f772039a1a2b2890fb37.mockapi.io/api/v1/Salas")
        const Salas = await resposta.json();
        return Salas;
        } catch (error) {
            console.error("Erro ao buscar livros:", error);
        } 
    } 
    onMount(async () => {
        Salas = await load();
    });
</script>


<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 max-w-6xl mx-auto my-8">
    {#each Salas as sala}
        <div class="bg-gray-100 border-2 border-gray-300 rounded-xl shadow-md p-6 text-center hover:shadow-lg hover:border-gray-500 transition">
            <h1 class="text-lg font-semibold mb-3 text-gray-800">{sala.nome}</h1>
            <p class="mb-1 text-gray-600">{sala.status}</p>
            <p class="mb-1 text-gray-600">{sala.temperatura}</p>
            <p class="mb-1 text-gray-600">{sala.numero}</p>
        </div>
    {/each}
</div>

