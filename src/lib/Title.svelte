<script>
    import {Dropdown, DropdownToggle, DropdownItem} from 'sveltestrap';
    import Map from './Map.svelte';

    export let mapIndex = -1;
    export let maps = [];

    let selectedMap = maps[0];
</script>

<p1> Choose a map </p1>
<br/>

<Dropdown triggerElement={selectedMap}>
    <DropdownToggle caret>{selectedMap.name}</DropdownToggle>
    {#each maps as map}
        <DropdownItem>{map.name}</DropdownItem>
    {/each}
</Dropdown>

<button on:click= {() => mapIndex = selectedMap.index}>Go to Map</button>
