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
                color: "#F44336",
                isInterval: horarios[i].intervalo
            });
        }
    }

    let showPopup = false;
    let selectedCell: StatusCell | null = null;

    function handleCellClick(cell: StatusCell) {
        if (!cell.isInterval) {
            selectedCell = cell;
            changeColor();
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
</style>