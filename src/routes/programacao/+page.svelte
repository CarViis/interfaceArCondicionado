<script lang="ts">
    // Dias da semana
    let dias: string[] = ["Segunda", "Terça", "Quarta", "Quinta", "Sexta"];
    // Horários da manhã
    let horarios: string[] = [
        "07:00 - 07:45",
        "07:45 - 08:30",
        "08:50 - 09:35",
        "09:35 - 10:20",
        "10:30 - 11:15",
        "11:15 - 12:00",
        "13:00 - 13:45",
        "13:45 - 14:30",
        "14:50 - 15:35",
        "15:35 - 16:20",
        "16:30 - 17:15",
        "17:15 - 18:00"
    ];

    type StatusCell = {
        id: number;
        row: number;
        column: number;
        color: string;
    };

    let status: StatusCell[] = [];
    let id = 1;
    for (let i = 0; i < horarios.length; i++) {
        for (let j = 0; j < dias.length; j++) {
            status.push({
                id: id++,
                row: i,
                column: j,
                color: Math.random() > 0.5 ? '#8BC34A' : '#F44336'
            });
        }
    }

    function handleCellClick(cell: StatusCell) {
        // Example: toggle color on click
        cell.color = cell.color === '#8BC34A' ? '#F44336' : '#8BC34A';
        // Force Svelte to update
        status = [...status];
    }
</script>

<table>
    <thead>
        <tr>
            <th></th>
            {#each dias as dia}
                <th>{dia}</th>
            {/each}
        </tr>
    </thead>
    <tbody>
        {#each horarios as horario, i}
            <tr>
                <td>{horario}</td>
                {#each dias as dia, j}
                    {@const cell = status.find(s => s.row === i && s.column === j)}
                    <td
                        style="background-color: {cell ? cell.color : 'transparent'}"
                        on:click={() => cell && handleCellClick(cell)}
                    ></td>
                {/each}
            </tr>
        {/each}
    </tbody>
</table>

<style>
    table {
        border-collapse: collapse;
        width: 100%;
        margin-top: 20px;
    }
    th, td {
        border: 1px solid #ccc;
        padding: 8px 12px;
        text-align: center;
        width: 120px;
    }
    th:first-child,
    td:first-child {
        align-items: center;
        width: 60px; /* Change this value as needed */
        text-align: left; /* Optional: align text to the left */
    }
    th {
        background-color: #f2f2f2;
    }
    tr:hover {
        background-color: #f5f5f5;
    }
</style>