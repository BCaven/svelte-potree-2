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


  import { onMount } from 'svelte';

  import * as THREE from 'three';

  let canvas: HTMLCanvasElement;

  onMount(() => {
    
    let gl = canvas.getContext('webgl', {
      alpha: true,
			depth: true,
			stencil: false,
			antialias: false,
			//premultipliedAlpha: _premultipliedAlpha,
			preserveDrawingBuffer: true,
			powerPreference: "high-performance",
    });

    gl.getExtension('EXT_frag_depth');
		gl.getExtension('WEBGL_depth_texture');
		gl.getExtension('WEBGL_color_buffer_float')

		let extVAO = gl.getExtension('OES_vertex_array_object');
    
    let renderer = new THREE.WebGLRenderer({
      alpha: true,
      premultipliedAlpha: false,
			canvas: canvas,
			context: gl,
      failIfMajorPerformanceCaveat: true
    });





  });

</script>

<main>

  <canvas bind:this={canvas}></canvas>

</main>