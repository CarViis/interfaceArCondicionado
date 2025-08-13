<script lang="ts">
import { onMount } from "svelte";

type Sala = {
    id: string;
    nome: string;
    status: string;
    temperatura: string;
    numero: string;
    ligado: boolean;
};

let Salas: Sala[] = [];

async function load() { 
    try {
        const resposta = await fetch("https://6895f772039a1a2b2890fb37.mockapi.io/api/v1/Salas");
        const data = await resposta.json();
        return data.map((sala: any) => ({ ...sala, ligado: false })) as Sala[];
    } catch (error) {
        console.error("Erro ao buscar salas:", error);
        return [];
    } 
} 

onMount(async () => {
    Salas = await load();
});
</script>


<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 max-w-6xl mx-auto my-8">
    {#each Salas as sala, i (sala.id)}
        <div class="bg-gray-100 border-2 border-gray-300 rounded-xl shadow-md p-6 text-center hover:shadow-lg hover:border-gray-500 transition">
            <h1 class="text-lg font-semibold mb-3 text-gray-800">{sala.nome}</h1>
            <p class="mb-1 text-gray-600">{sala.status}</p>
            <p class="mb-1 text-gray-600">{sala.temperatura}</p>
            <p class="mb-1 text-gray-600">{sala.numero}</p>
            <p class="mb-1 text-gray-600">
                <input type="checkbox" id={"chk" + sala.id} bind:checked={sala.ligado} class="chk" />
                <label for={"chk" + sala.id} class="switch">
                    <span class="slider"></span>
                </label>
            </p>
        </div>
    {/each}
</div>

<style>
    .chk {
        display: none;
    }
    .switch {
        position: relative;
        background-color: #777;
        width: 220px;
        height:60px;
        border-radius: 40px;
        display: flex;
        align-items: center;
        padding: 5px;
        transition: all .5s ease-in-out;
        cursor: pointer;
    }
    .slider {
        position: absolute;
        background-color: #fff;
        border-radius: 50%;
        width: 50px;
        height: 50px;
        transition: all .5s ease-in-out;
        left: 5px;
    }
    .chk:checked + .switch {
        background-color: #00d0ff;
    }
    .chk:checked + .switch .slider {
        transform: translateX(160px);
    }
</style>