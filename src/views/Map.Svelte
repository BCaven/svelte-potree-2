<script>
    //import PotreeViewer from "./PotreeViewer.svelte";
    export let map = "default map";
    export let infoId;
    export let showInfo = false;
    export let start;
    function onInfoClick (id) {
        infoId = id;
        showInfo = true;
    }
</script>


{map}



<!--<PotreeViewer/>-->

<iframe src="{map}" title="potree iframe" style="position: absolute; width: 100%; height: 100%; left: 0px; top: 0px;"/>


<div class="toolbar">
    <button on:click = {() => start = false}> return </button>
   <!-- <button on:click = {() => onInfoClick(0)}> Info 1 </button>  to pass a function that has parameters to on:click you have to wrap it in another function-->
    <!-- <button on:click = {() => onInfoClick(1)}> Info 2 </button> -->
    <button on:click = {() => onInfoClick(0)}> help </button>
    <button> demo </button>
</div>

<style>
    .toolbar {
        display: grid;
        grid-template-columns: repeat(3, 5em);
		grid-template-rows: repeat(4, 3em);
		grid-gap: 0.5em;
        position: absolute;
        right: 10px;
        top: 10px;
    }
    button {
        margin: 0
    }
</style>