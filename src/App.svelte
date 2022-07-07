<script lang="ts">
  /*
  For potree:
  Annotations:
  - show header annotations, hide them when one is selected
  - make a grid of the headers in the top right corner for the user to choose from (adds accessability for larger scenes by reducing the need to manipulate the camera)
  - change the structure of annotations to include sub-tags
  - the tags have the thing they are storing, the type of thing they are, and the name of the tag
  
  Tags:
  - only show tags that can be seen by the camera (and are not blocked by a pointcloud/model)
  - add way to attach new tags to monuments: maybe repurpose potree's pin system to allow users to click on a model (which will be where the tag shows up in the renderer)
  - tags are "technically" attached to the 3D models - not the pointclouds - or at least that is how we are going to pick where they go (probably)
  


  Link tags to the Filter component
    - get the potree component to list all visible tags

  
  
  
  */


  /*
  Control all of your basic processes from this program
  
  
  
  */

//import PotreeViewer from "./PotreeViewer.svelte";
  	import Title from "./views/Title.svelte"; // change these
	import Test from "./views/Test.svelte";
	import Map from "./views/Map.svelte";
	import Info from "./views/Info.svelte";
	import { MapData } from "./classes/MapData.js";
	import PotreeViewer from "./views/Potree.svelte";

	let mapIndex = -1; // -1 means home page
	let infoId = 0;
	let maps = [ // these are place-holders, will need to change them to jsons for the actual thing
		new MapData("Example 1", 0, null, "http://127.0.0.1:5500/Potree/potree-1.8/examples/cesium_ca13.html"),
		new MapData("Example 2", 1, null, "http://127.0.0.1:5500/Potree/potree-1.8/examples/cesium_ca13.html"),
		new MapData("Example 3", 2, null, "http://127.0.0.1:5500/Potree/potree-1.8/examples/cesium_sorvilier.html"),
		new MapData("Example 4", 3, null, null),
		new MapData("Example 5", 4, null, null)
		
	];
	let infos = [
		"example info 1",
		"example info 2"
	];
	// let showInfo = false;
	// $: map = maps[mapIndex]; 
	// $: info = infos[infoId];
	
	
</script>


<main>
	
	
	{#if mapIndex < 0}
		<Title bind:mapIndex bind:maps/>
	{:else}
		<PotreeViewer/>
		<!-- <Test bind:mapIndex bind:map={maps[mapIndex]}/> -->
		<!-- {#if !showInfo}
			<Map map = {maps} bind:infoId bind:showInfo bind:mapIndex/>
		{/if} -->
	{/if}

	<!-- {#if showInfo} could totally put this in the map file... but it feels better to have it all controlled by the app
		<Info {info} bind:showInfo/>
	{/if} -->
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>