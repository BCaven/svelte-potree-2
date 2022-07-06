<script>
    import {Container, Row, Col, Button, 
            ListGroup, ListGroupItem, Styles} from 'sveltestrap';
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

<!-- <div color="#808080" style="position: absolute; margin: 0; height: 20vh; width: 100vw; color: #808080"/> -->

<Container style="margin: 0; padding: 0; max-width: none; background-color: #808080">
    <Row style="height: 8vh">
        <Col cols="12" class="my-auto">
            <h1>Title</h1>
        </Col>
    </Row>
    <Row style="height: 8vh">
        <Col sm="12" class="my-auto">
            <p1>You could put a bunch of text right here to describe the project.</p1>
        </Col>
    </Row>
</Container>

<Container class="mx-auto" style="padding-top: 5px">
    <ListGroup style="overflow: scroll">
        {#each maps as map}
            <ListGroupItem>
                <Row>
                    <Col sm="8" class="text-start my-auto">{map.name}</Col>
                    <Col sm="2">
                        <Button on:click={() => mapIndex = map.index}>View Map</Button>
                    </Col>
                    <Col sm="2">
                        <Button>Edit Map</Button>
                    </Col>
                </Row>
            </ListGroupItem>
        {/each}
    </ListGroup>
</Container>

<!-- <Dropdown triggerElement={selectedMap}>
    <DropdownToggle caret>{label}</DropdownToggle>
    <DropdownMenu>
        {#each maps as map}
            <DropdownItem on:click = {() => selectedMap = map}>{map.name}</DropdownItem>
        {/each}
    </DropdownMenu>
</Dropdown> -->
<!-- these lines above make the dropdown. Idk why it requires so many different elements, but this is how it must
    be done using sveltestrap.-->

<!-- {#if selectedMap}
    <button on:click= {() => mapIndex = selectedMap.index}>Go to Map</button>
{/if} -->


