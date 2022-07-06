<script>
    import {Dropdown, DropdownToggle, DropdownMenu, DropdownItem, Styles} from 'sveltestrap';
    import Map from './Map.svelte';

    export let mapIndex = -1;
    export let maps = [];

    let selectedMap = null;
    let label = "Select a Map"
    $: if (selectedMap){
        label = selectedMap.name
    } else {
        label = "Select a Map"
    }
</script>

<Styles />
<!-- Styles must be here in order for sveltestrap components to work -->

<br/>

<Dropdown triggerElement={selectedMap}>
    <DropdownToggle caret>{label}</DropdownToggle>
    <DropdownMenu>
        {#each maps as map}
            <DropdownItem on:click = {() => selectedMap = map}>{map.name}</DropdownItem>
        {/each}
    </DropdownMenu>
</Dropdown>
<!-- these lines above make the dropdown. Idk why it requires so many different elements, but this is how it must
    be done using sveltestrap.-->

{#if selectedMap}
    <button on:click= {() => mapIndex = selectedMap.index}>Go to Map</button>
{/if}
