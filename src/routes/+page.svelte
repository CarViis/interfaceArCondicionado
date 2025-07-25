<script>
 let salas = [
    { id: 1, titulo: "Sala de Aula"},
    { id: 2, titulo: "Laboratório de Informática"},
    { id: 3, titulo: "Auditório Principal"},
    { id: 4, titulo: "Sala Administrativa"},
    { id: 5, titulo: "Sala de Reuniões"},
    { id: 6, titulo: "Sala de Descanso"}
 ];
</script>

<div class="salas flex flex-row fustify-around">
    {#each salas as sala}
        <div class="sala bg-white p-4 rounded-lg shadow-md m-2 w-40 h-40 flex items-center justify-center">
        <h2 class="text-xl font-bold mb-2">{sala.titulo}</h2>
        </div>
    {/each}
</div>