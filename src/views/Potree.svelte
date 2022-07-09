<head>
	<meta charset="utf-8">
	<meta name="description" content="">
	<meta name="author" content="">
	<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
	<title>Potree Viewer</title>

	<link rel="stylesheet" type="text/css" href="../build/potree/potree.css">
	<link rel="stylesheet" type="text/css" href="../libs/jquery-ui/jquery-ui.min.css">
	<link rel="stylesheet" type="text/css" href="../libs/openlayers3/ol.css">
	<link rel="stylesheet" type="text/css" href="../libs/spectrum/spectrum.css">
	<link rel="stylesheet" type="text/css" href="../libs/jstree/themes/mixed/style.css">
	<!-- <link rel="stylesheet" type="text/css" href="../libs/Cesium/Widgets/CesiumWidget/CesiumWidget.css"> -->
</head>

<script>

    // src="../libs/jquery/jquery-3.1.1.min.js"
	// src="../libs/spectrum/spectrum.js"
	// src="../libs/jquery-ui/jquery-ui.min.js"
	// src="../libs/other/BinaryHeap.js"
	// src="../libs/tween/tween.min.js"
	// src="../libs/d3/d3.js"
	// src="../libs/proj4/proj4.js"
	// src="../libs/openlayers3/ol.js"
	// src="../libs/i18next/i18next.js"
	// src="../libs/jstree/jstree.js"
	// src="../libs/plasio/js/laslaz.js"
	// src="../libs/Cesium/Cesium.js"

	// import * as Cesium from 'Cesium';
    import * as Potree from '../potree/Potree.js';
	import * as THREE from 'three';
	import { onMount } from 'svelte';

	let tiffTest, potree_render_area, potree_sidebar_container;
	//We bind the elements to the above variables in order to aoid using get element by ID. Svelte does not like
	//get element by ID

	onMount(() => {
		window.viewer = new Potree.Viewer(potree_render_area);
		
		viewer.setEDLEnabled(true);
		viewer.setFOV(60);
		viewer.setPointBudget(2_000_000);
		viewer.setMinNodeSize(0);
		viewer.loadSettingsFromURL();
		viewer.setServer("http://localhost:3000");
		
		viewer.setDescription("");
		
		viewer.loadGUI().then(() => {
			viewer.setLanguage('en');
			window.$("#menu_appearance").next().show();
			// viewer.toggleSidebar();
		});

		let light = new THREE.SpotLight();
		light.distance = 15;
		light.angle = (60 / 180) * Math.PI;
		light.position.set(8.489, 3.577, 5.796);
		light.lookAt(new THREE.Vector3(1.219, -0.171, 2.776));
		viewer.scene.scene.add(light);

		let sph = new Potree.SpotLightHelper(light, new THREE.Color().setHex(0xff0000));
		viewer.scene.scene.add(sph);
		
		// Sigeom
		Potree.loadPointCloud("http://5.9.65.151/mschuetz/potree/resources/pointclouds/archpro/heidentor/cloud.js", "Heidentor", function(e){
			viewer.scene.addPointCloud(e.pointcloud);
			e.pointcloud.position.z = 0;
			let material = e.pointcloud.material;
			material.size = 1;
			material.pointSizeType = Potree.PointSizeType.ADAPTIVE;
			material.activeAttributeName = "elevation";
			material.uniforms.uShadowColor.value = [0.6, 0.6, 0.6];

			viewer.scene.view.position.set(19.474, -14.324, 12.829);
			viewer.scene.view.lookAt(0.339, 0.145, 4.073);
		});

		
		Potree.loadPointCloud("../pointclouds/lion_takanawa/cloud.js", "lion", function(e){
			viewer.scene.addPointCloud(e.pointcloud);
			
			let material = e.pointcloud.material;
			material.size = 1;
			material.pointSizeType = Potree.PointSizeType.ADAPTIVE;
			material.uniforms.uShadowColor.value = [0.6, 0.6, 0.6];
			
			e.pointcloud.position.set(0, -2, 0);
			
		});
	});


</script>


<div class="potree_container" style="position: absolute; width: 100%; height: 100%; left: 0px; top: 0px; ">
	<div bind:this={potree_render_area} style="background-image: url('../build/potree/resources/images/background.jpg');"></div>
	<div bind:this={potree_sidebar_container}> </div>
	<input bind:this={tiffTest} type="button" value="tiff test" />
</div>


