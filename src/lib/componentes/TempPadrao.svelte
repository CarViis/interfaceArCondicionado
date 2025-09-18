<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    export let salaId: string = '';

    const dispatch = createEventDispatcher();

    let showPopup = false;
    let temperatura: number = 22;
    let loading = false;
    let error: string | null = null;

    function openPopup() {
        showPopup = true;
        loadCurrent();
    }

    function closePopup() {
        showPopup = false;
        error = null;
    }

    async function loadCurrent() {
        if (!salaId) return;
        loading = true;
        try {
            const res = await fetch(`https://6895f772039a1a2b2890fb37.mockapi.io/api/v1/Salas/${salaId}`);
            if (!res.ok) throw new Error('Falha ao buscar sala');
            const data = await res.json();
            temperatura = Number(data.temperatura) || 22;
            // garante que esteja no intervalo
            if (temperatura < 18) temperatura = 18;
            if (temperatura > 30) temperatura = 30;
        } catch (e) {
            console.error(e);
            error = 'Não foi possível carregar a temperatura atual.';
        } finally {
            loading = false;
        }
    }

    function validateTemp(v: number) {
        if (isNaN(v)) return 18;
        if (v < 18) return 18;
        if (v > 30) return 30;
        return Math.round(v);
    }

    async function save() {
        if (!salaId) {
            error = 'Sala inválida.';
            return;
        }
        error = null;
        const value = validateTemp(temperatura);
        loading = true;
        try {
            const res = await fetch(`https://6895f772039a1a2b2890fb37.mockapi.io/api/v1/Salas/${salaId}`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ temperatura: value })
            });
            if (!res.ok) throw new Error('Falha ao atualizar');
            const data = await res.json();
            dispatch('updated', { temperatura: Number(data.temperatura) });
            closePopup();
        } catch (e) {
            console.error(e);
            error = 'Erro ao salvar temperatura.';
        } finally {
            loading = false;
        }
    }
</script>

<button class="temp-button" id="tempButton" on:click={openPopup}> Configurar Temperatura Padrão </button>
{#if showPopup}
    <div class="popup-overlay" on:click={closePopup}>
        <div class="popup" on:click|stopPropagation>
            <h3>Definir Temperatura</h3>
            {#if loading}
                <div>Carregando...</div>
            {:else}
                <div style="display:flex;align-items:center;gap:12px; margin: 12px 0;">
                    <button on:click={() => temperatura = validateTemp(temperatura - 1)} disabled={temperatura <= 18}>-</button>
                    <input type="number" bind:value={temperatura} min="18" max="30" step="1" style="width:70px;text-align:center;" />
                    <button on:click={() => temperatura = validateTemp(temperatura + 1)} disabled={temperatura >= 30}>+</button>
                </div>
                {#if error}
                    <div style="color: red;">{error}</div>
                {/if}
                <div style="display:flex;gap:8px;justify-content:center;margin-top:8px;">
                    <button on:click={save}>Salvar</button>
                    <button on:click={closePopup}>Fechar</button>
                </div>
            {/if}
        </div>
    </div>
{/if}

<style>
    .temp-button {
        background: lightgray;
        color: black;
        border: none;
        padding: 10px 20px;
        font-size: 16px;
        font-weight: 600;
        border-radius: 8px;
        cursor: pointer;
        margin: 10px;
        border: 1px solid black;
    }
    .popup-overlay {
        position: fixed;
        inset: 0;
        background: rgba(0,0,0,0.4);
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .popup {
        background: white;
        padding: 18px;
        border-radius: 12px;
        min-width: 300px;
        box-shadow: 0 6px 20px rgba(0,0,0,0.2);
    }
</style>
