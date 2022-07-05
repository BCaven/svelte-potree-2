<script>
    export let mapIndex = -1;
    export let map = "Example map 1";
    export let start = false;
</script>

<p1> Choose a map </p1>
<br/>
Chosen map: {map}

{#if mapId < 2}
<button on:click={() => mapId++} style="position:absolute; top:100px; left:45%"> up </button>
{/if}
{#if mapId > 0}
<button on:click={() => mapId--} style="position:absolute; top:100px; left:47%"> down </button>
{/if}
<button on:click={() => start = true} style="position:absolute; top:100px; left:50%"> start </button>

<button style="position:absolute; top:50%; left:50%">Add a new map</button>
