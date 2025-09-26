<script>
    let showPopup = false;
    function openPopup() {
    showPopup = true;
    }

    function closePopup() {
        showPopup = false;
    }


</script>

<button class="temp-button" id="tempButton" on:click={openPopup}> Configurar Temperatura Padrão </button>
{#if showPopup}
    <div class="popup-overlay" on:click={closePopup}>
        <div class="popup" on:click|stopPropagation>
            <h3>Definir Temperatura</h3>
            <button on:click={closePopup}>Fechar</button>
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
</style>
