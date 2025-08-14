<script lang="ts">
    export let dias: string[] = ["Segunda", "Terça", "Quarta", "Quinta", "Sexta"];
    export let horarios: { label: string, intervalo?: boolean }[] = [
        { label: "07:00 - 07:45" },
        { label: "07:45 - 08:30" },
        { label: "08:50 - 09:35" },
        { label: "09:35 - 10:20" },
        { label: "10:30 - 11:15" },
        { label: "11:15 - 12:00" },
        { label: "Intervalo Entre Turnos", intervalo: true },
        { label: "13:00 - 13:45" },
        { label: "13:45 - 14:30" },
        { label: "14:50 - 15:35" },
        { label: "15:35 - 16:20" },
        { label: "16:30 - 17:15" },
        { label: "17:15 - 18:00" },
        { label: "Intervalo Entre Turnos", intervalo: true },
        { label: "18:45 - 19:30" },
        { label: "19:30 - 20:15" },
        { label: "20:25 - 21:10" },
        { label: "21:10 - 21:55" }
    ];

    type StatusCell = {
        id: number;
        row: number;
        column: number;
        color: string;
        isInterval?: boolean;
    };

    let status: StatusCell[] = [];
    let id = 1;
    for (let i = 0; i < horarios.length; i++) {
        for (let j = 0; j < dias.length; j++) {
            status.push({
                id: id++,
                row: i,
                column: j,
                color: horarios[i].intervalo
                    ? "#bdbdbd"
                    : (Math.random() > 0.5 ? "#8BC34A" : "#F44336"),
                isInterval: horarios[i].intervalo
            });
        }
    }

    let showPopup = false;
    let selectedCell: StatusCell | null = null;

    function handleCellClick(cell: StatusCell) {
        if (!cell.isInterval) {
            selectedCell = cell;
            showPopup = true;
        }
    }

    function changeColor() {
        if (selectedCell) {
            selectedCell.color = selectedCell.color === '#8BC34A' ? '#F44336' : '#8BC34A';
            status = [...status];
            showPopup = false;
            selectedCell = null;
        }
    }

    function closePopup() {
        showPopup = false;
        selectedCell = null;
    }
</script>

<div class="flex justify-center mx-auto">
    <table>
        <thead>
            <tr>
                <th class="horario-coluna">Horário</th>
                {#each dias as dia}
                    <th>{dia}</th>
                {/each}
            </tr>
        </thead>
        <tbody>
            {#each horarios as horario, i}
                <tr class={horario.intervalo ? "intervalo" : ""}>
                    <td class={horario.intervalo ? "intervalo-horario" : ""}>{horario.label}</td>
                    {#each dias as dia, j}
                        {@const cell = status.find(s => s.row === i && s.column === j)}
                        <td
                            style="background-color: {cell ? cell.color : 'transparent'}; cursor: {cell && !cell.isInterval ? 'pointer' : 'default'}"
                            on:click={() => cell && handleCellClick(cell)}
                        >
                        </td>
                    {/each}
                </tr>
            {/each}
        </tbody>
    </table>
</div>

{#if showPopup && selectedCell}
    <div
        class="popup-overlay"
        role="button"
        tabindex="0"
        aria-label="Fechar popup"
        on:click={closePopup}
        on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') closePopup(); }}
    >
        <div
            class="popup"
            role="dialog"
            aria-modal="true"
            tabindex="0"
            on:click|stopPropagation
            on:keydown|stopPropagation
        >
            <p>Alterar cor da célula?</p>
            <button on:click={changeColor}>
                Mudar para {selectedCell.color === '#8BC34A' ? 'Vermelho' : 'Verde'}
            </button>
            <button on:click={closePopup}>Cancelar</button>
        </div>
    </div>
{/if}

<style>
table {
    border-collapse: collapse;
    width: 100%;
    margin-top: 20px;
}
th, td {
    border: 1px solid #333;
    padding: 8px 12px;
    text-align: center;
    width: 120px;
}
.horario-coluna,
td.intervalo-horario {
    width: 150px;
    text-align: left;
    font-weight: bold;
    background-color: #e0e0e0;
}
th {
    background-color: #e0e0e0;
}
tr.intervalo td {
    background-color: #bdbdbd !important;
    font-weight: bold;
    text-align: center;
}
tr.intervalo td.intervalo-horario {
    background-color: #bdbdbd !important;
    font-weight: bold;
    text-align: left;
}
tr:hover:not(.intervalo) {
    background-color: #f5f5f5;
}
.popup-overlay {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0,0,0,0.3);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
}
.popup {
    background: #fff;
    padding: 24px 18px;
    border-radius: 8px;
    box-shadow: 0 2px 8px #3333;
    min-width: 220px;
    text-align: center;
}
.popup button {
    margin: 8px 6px 0 6px;
    padding: 6px 16px;
    border: none;
    border-radius: 4px;
    background: #e0e0e0;
    cursor: pointer;
    font-weight: bold;
}
.popup button:first-child {
    background: #8BC34A;
    color: #fff;
}
.popup button:last-child {
    background: #F44336;
    color: #fff;
}
</style>