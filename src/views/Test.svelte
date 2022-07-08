<script>
    export let mapIndex;
    export let map;
</script>

<p1>{map.name}</p1>
<p2>Index: {map.index}</p2>
<button on:click={() => mapIndex = -1}>Return</button>