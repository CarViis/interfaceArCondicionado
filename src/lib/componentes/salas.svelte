<script lang="ts">
import { onMount } from "svelte";
import { goto } from "$app/navigation";

type Sala = {
    id: string;
    nome: string;
    status: string;
    temperatura: number;
    numero: string;
    ligado: boolean;
};

let Salas: Sala[] = [];

async function load() { 
    try {
        const resposta = await fetch("https://6895f772039a1a2b2890fb37.mockapi.io/api/v1/Salas");
        const data = await resposta.json();
        return data.map((sala: any) => ({ ...sala, ligado: false, temperatura: Number(sala.temperatura) || 22 })) as Sala[];
    } catch (error) {
        console.error("Erro ao buscar salas:", error);
        return [];
    } 
} 

onMount(async () => {
    Salas = await load();
});

function aumentarTemp(i: number) {
    if (Salas[i].temperatura < 30) Salas[i].temperatura += 1;
}
function diminuirTemp(i: number) {
    if (Salas[i].temperatura > 16) Salas[i].temperatura -= 1;
}
</script>

<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 max-w-6xl mx-auto my-8">
    {#each Salas as sala, i (sala.id)}
        <div class="card"  >
            <div class="card-header">
                <h1 class="card-title">{sala.nome}</h1>
            </div>
            <div class="temp-bar">
                <button class="temp-btn minus" on:click={() => diminuirTemp(i)}>-</button>
                <span class="temp-value">{sala.temperatura} °C</span>
                <button class="temp-btn plus" on:click={() => aumentarTemp(i)}>+</button>
            </div>
            <div class="card-footer">
                <label class="switch-cool">
                    <input type="checkbox" bind:checked={sala.ligado} />
                    <span class="slider-cool"></span>
                </label>
                <span class="mode-label">
                    {#if sala.ligado}
                        <span class="icon-snow">❄️</span> FRIO
                    {:else}
                        Desligado
                    {/if}
                </span>
                
            </div>
            <a class="detalhes-btn" href="/programacao/${sala.id}" >
                    Programar
            </a>
        </div>
    {/each}
</div>

<style>
.card {
    background: #fff;
    border-radius: 22px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    padding: 22px 18px 18px 18px;
    text-align: center;
    min-width: 220px;
    max-width: 260px;
    margin: auto;
    display: flex;
    flex-direction: column;
    gap: 16px;
}
.card-header {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-bottom: 8px;
}
.icon-temp {
    font-size: 1.5rem;
}
.card-title {
    font-size: 1.2rem;
    font-weight: bold;
    letter-spacing: 1px;
}
.temp-bar {
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(90deg, #1e3a8a 0%, #e11d48 100%);
    border-radius: 14px;
    padding: 8px 0;
    gap: 10px;
    margin-bottom: 8px;
}
.temp-btn {
    border: none;
    outline: none;
    width: 38px;
    height: 38px;
    border-radius: 50%;
    font-size: 1.4rem;
    font-weight: bold;
    cursor: pointer;
    color: #fff;
    background: #1e3a8a;
    transition: background 0.2s;
    user-select: none;
}
.temp-btn.plus {
    background: #e11d48;
}
.temp-btn.minus {
    background: #1e3a8a;
}
.temp-btn:active {
    filter: brightness(0.85);
}
.temp-value {
    font-size: 1.3rem;
    font-weight: bold;
    color: #222;
    background: rgba(255,255,255,0.7);
    border-radius: 8px;
    padding: 0 12px;
    min-width: 70px;
    display: inline-block;
}
.card-footer {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    margin-top: 6px;
}
.switch-cool {
    position: relative;
    display: inline-block;
    width: 48px;
    height: 28px;
}
.switch-cool input {
    opacity: 0;
    width: 0;
    height: 0;
}
.slider-cool {
    position: absolute;
    cursor: pointer;
    top: 0; left: 0; right: 0; bottom: 0;
    background-color: #ccc;
    border-radius: 14px;
    transition: .4s;
}
.slider-cool:before {
    position: absolute;
    content: "";
    height: 22px;
    width: 22px;
    left: 3px;
    bottom: 3px;
    background-color: white;
    border-radius: 50%;
    transition: .4s;
}
.switch-cool input:checked + .slider-cool {
    background-color: #1de9b6;
}
.switch-cool input:checked + .slider-cool:before {
    transform: translateX(20px);
}
.mode-label {
    font-size: 1.1rem;
    font-weight: 600;
    color: #222;
    display: flex;
    align-items: center;
    gap: 6px;
}
.icon-snow {
    font-size: 1.2rem;
}
</style>