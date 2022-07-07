<body>
	<script src="../libs/jquery/jquery-3.1.1.min.js"></script>
	<script src="../libs/spectrum/spectrum.js"></script>
	<script src="../libs/jquery-ui/jquery-ui.min.js"></script>
	
	
	<script src="../libs/other/BinaryHeap.js"></script>
	<script src="../libs/tween/tween.min.js"></script>
	<script src="../libs/d3/d3.js"></script>
	<script src="../libs/proj4/proj4.js"></script>
	<script src="../libs/openlayers3/ol.js"></script>
	<script src="../libs/i18next/i18next.js"></script>
	<script src="../libs/jstree/jstree.js"></script>
	<script src="../build/potree/potree.js"></script>
	<script src="../libs/plasio/js/laslaz.js"></script>

	<div class="potree_container" style="position: absolute; width: 100%; height: 100%; left: 0px; top: 0px; ">
		<div id="potree_render_area" style="background-image: url('../build/potree/resources/images/background.jpg');">
		</div>
	</div>
</body>

<script>
    import * as THREE from "../libs/three.js/build/three.module.js";
	import { PLYLoader } from "../libs/three.js/loaders/PLYLoader.js";

    // export let annotations = [];
    // export let map = "default";

    //This is all copied from chase

    window.viewer = new Potree.Viewer(document.getElementById("potree_render_area"));
	const loader = new PLYLoader();
	
	viewer.setEDLEnabled(true);
	viewer.setFOV(60);
	viewer.setPointBudget(1_000_000);
	viewer.loadSettingsFromURL();
	// viewer.light
	
	viewer.setDescription("");

	viewer.scene.view.position.set(100,210,0);
	viewer.scene.view.lookAt(new THREE.Vector3(100,210,0));
	
	viewer.loadGUI(() => {
		viewer.setLanguage('en');
		_("#menu_appearance").next().show(); //I am not sure that this is right. This underscore used to be a $ but idk what that did
		//viewer.toggleSidebar();
	});
	
	// Point Cloud
	Potree.loadPointCloud("../pointclouds/PotP1W/metadata.json", "lion", function(e){
		viewer.scene.addPointCloud(e.pointcloud);
		
		let material = e.pointcloud.material;
		material.size = 1;
		material.pointSizeType = Potree.PointSizeType.ATTENUATED;
		
		viewer.fitToScreen();
	});

	// Creating ambient light for all of the mesh models
	const light = new THREE.AmbientLight(); // soft white light
		viewer.scene.scene.add( light );

		// { // ANNOTATIONS
			

			

		// 	let aSanSimeon = new Potree.Annotation({
		// 		title: "San Simeon",
		// 		position: [664147.50, 3946008.73, 16.30],
		// 		cameraPosition: [664941.80, 3943568.06, 1925.30],
		// 		cameraTarget: [664147.50, 3946008.73, 16.30],
		// 	});
		// 	aCA13.add(aSanSimeon);

		// 	let aHearstCastle = new Potree.Annotation({
		// 		title: "Hearst Castle",
		// 		position: [665744.56, 3950567.52, 500.48],
		// 		cameraPosition: [665692.66, 3950521.65, 542.02],
		// 		cameraTarget: [665744.56, 3950567.52, 500.48],
		// 	});
		// 	aCA13.add(aHearstCastle);

		// 	let aMorroBay = new Potree.Annotation({
		// 		title: "Morro Bay",
		// 		position: [695483.33, 3916430.09, 25.75],
		// 		cameraPosition: [694114.65, 3911176.26, 3402.33],
		// 		cameraTarget: [695483.33, 3916430.09, 25.75],
		// 	});
		// 	aCA13.add(aMorroBay);

		// 	let aMorroRock = new Potree.Annotation({
		// 		title: "Morro Rock",
		// 		position: [693729.66, 3916085.19, 90.35],
		// 		cameraPosition: [693512.77, 3915375.61, 342.33],
		// 		cameraTarget: [693729.66, 3916085.19, 90.35],
		// 	});
		// 	aMorroBay.add(aMorroRock);

		// 	let aMorroBayMutualWaterCo = new Potree.Annotation({
		// 		title: "Morro Bay Mutual Water Co",
		// 		position: [694699.45, 3916425.75, 39.78],
		// 		cameraPosition: [694377.64, 3916289.32, 218.40],
		// 		cameraTarget: [694699.45, 3916425.75, 39.78],
		// 	});
		// 	aMorroBay.add(aMorroBayMutualWaterCo);

		// 	let aLilaKeiserPark = new Potree.Annotation({
		// 		title: "Lila Keiser Park",
		// 		position: [694674.99, 3917070.49, 10.86],
		// 		cameraPosition: [694452.59, 3916845.14, 298.64],
		// 		cameraTarget: [694674.99, 3917070.49, 10.86],
		// 	});
		// 	aMorroBay.add(aLilaKeiserPark);

		// 	let aSanLuisObispo = new Potree.Annotation({
		// 		title: "San Luis Obispo",
		// 		position: [712573.39, 3907588.33, 146.44],
		// 		cameraPosition: [711158.29, 3907019.82, 1335.89],
		// 		cameraTarget: [712573.39, 3907588.33, 146.44],
		// 	});
		// 	aCA13.add(aSanLuisObispo);

		// 	let aLopezHill = new Potree.Annotation({
		// 		title: "Lopez Hill",
		// 		position: [728635.63, 3895761.56, 456.33],
		// 		cameraPosition: [728277.24, 3895282.29, 821.51],
		// 		cameraTarget: [728635.63, 3895761.56, 456.33],
		// 	});
		// 	aCA13.add(aLopezHill);

		// 	let aWhaleRockReservoir = new Potree.Annotation({
		// 		title: "Whale Rock Reservoir",
		// 		position: [692845.46, 3925528.53, 140.91],
		// 		cameraPosition: [693073.32, 3922354.02, 2154.17],
		// 		cameraTarget: [692845.46, 3925528.53, 140.91],
		// 	});
		// 	aCA13.add(aWhaleRockReservoir);

		// }

		// { // TREE RETURNS POI - ANNOTATION & VOLUME
		// 	let aRoot = scene.annotations;

		// 	let elTitle = $(`
		// 	<span>
		// 		Tree Returns:
		// 		<img name="action_return_number" src="${Potree.resourcePath}/icons/return_number.svg" class="annotation-action-icon"/>
		// 		<img name="action_rgb" src="${Potree.resourcePath}/icons/rgb.png" class="annotation-action-icon"/>
		// 	</span>`);

		// 	elTitle.find("img[name=action_return_number]").click( () => {
		// 		event.stopPropagation();
		// 		material.activeAttributeName = "return_number";
		// 		material.pointSizeType = Potree.PointSizeType.FIXED;
		// 		material.size = 5;
		// 		potreeViewer.setClipTask(Potree.ClipTask.SHOW_INSIDE);
		// 	});
			
		// 	elTitle.find("img[name=action_rgb]").click( () => {
		// 		event.stopPropagation();
		// 		material.activeAttributeName = "rgba";
		// 		material.pointSizeType = Potree.PointSizeType.ADAPTIVE;
		// 		material.size = 1;
		// 		potreeViewer.setClipTask(Potree.ClipTask.HIGHLIGHT);
		// 	});

		// 	elTitle.toString = () => "Tree Returns";
			

		// 	let aTreeReturns = new Potree.Annotation({
		// 		title: elTitle,
		// 		position: [675756.75, 3937590.94, 80.21],
		// 		cameraPosition: [675715.78, 3937700.36, 115.95],
		// 		cameraTarget: [675756.75, 3937590.94, 80.21],
		// 	});
		// 	aRoot.add(aTreeReturns);
		// 	aTreeReturns.domElement.find(".annotation-action-icon:first").css("filter", "invert(1)");

		// 	let volume = new Potree.BoxVolume();
		// 	volume.position.set(675755.4039368022, 3937586.911614576, 85);
		// 	volume.scale.set(119.87189835418388, 68.3925257233834, 51.757483718373265);
		// 	volume.rotation.set(0, 0, 0.8819755090987993, "XYZ");
		// 	volume.clip = true;
		// 	volume.visible = false;
		// 	volume.name = "Trees";
		// 	scene.addVolume(volume);
		// }

	// Root Annotation
	let aRoot = viewer.scene.annotations;


	// Temple of Antoninus and Faustina
	loader.load(Potree.resourcePath + "../models/toaf.ply", (geometry) => {
		const textureLoader = new THREE.TextureLoader();

		const diffuseMap = textureLoader.load(Potree.resourcePath + "../models/toaf_tex.jpg");
		diffuseMap.encoding = THREE.sRGBEncoding;

		const normalMap = textureLoader.load(Potree.resourcePath + "../models/toaf_norm.jpg");
		normalMap.encoding = THREE.sRGBEncoding;

		geometry.computeVertexNormals();

		let mesh;
		{
			const material = new THREE.MeshStandardMaterial({
				color: 0xffffff,
				roughness: 0.5,
				map: diffuseMap,
				normalMap: normalMap,
				normalMapType: THREE.ObjectSpaceNormalMap,
			});
			mesh = new THREE.Mesh(geometry, material);
			mesh.position.set(48.5, 238.5, -13);
			mesh.rotation.set(0, 0, -Math.PI * .19);
			mesh.visible = false;

			viewer.scene.scene.add(mesh);
		}

		viewer.onGUILoaded(() => {
			// Add entries to object list in sidebar
			let tree = _(`#jstree_scene`);
			let parentNode = "other";

			let meshID = tree.jstree('create_node', parentNode, {
				"text": "Temple of Antoninus and Faustina",
				"icon": `${Potree.resourcePath}/icons/triangle.svg`,
				"data": geometry
			},
				"last", false, false);
			tree.jstree(mesh.visible ? "check_node" : "uncheck_node", meshID);

		});

		// Annotations
		let aToaf = new Potree.Annotation({
			title: "Temple of Antoninus and Faustina",
			position: [48.5, 238.5, 10],
			cameraPosition: [80, 220, 10],
			cameraTarget: [51, 236, 0],
			collapseThreshold: 2000,

		});
		aToaf.addEventListener('click', () => {
			mesh.visible = true;
			console.log(aToaf)
		})
		aRoot.add(aToaf);

		let toafPillars = new Potree.Annotation({
			title: "Cool Pillars",
			position: [53, 224, -2],
			cameraPosition: [57, 221, -2],
			cameraTarget: [53, 224, -2],
		});
		aToaf.add(toafPillars);

		let toafStairs = new Potree.Annotation({
			title: "Old Stairs",
			position: [60, 230, -10],
			cameraPosition: [80, 220, 10],
			cameraTarget: [60, 230, -10],
		});
		aToaf.add(toafStairs);
	});

	// Temple of Castor and Pollux
	loader.load(Potree.resourcePath + "../models/tocap.ply", (geometry) => {
		const textureLoader = new THREE.TextureLoader();

		const diffuseMap = textureLoader.load(Potree.resourcePath + "../models/tocap_tex.jpg");
		diffuseMap.encoding = THREE.sRGBEncoding;

		const normalMap = textureLoader.load(Potree.resourcePath + "../models/tocap_norm.jpg");
		normalMap.encoding = THREE.sRGBEncoding;

		geometry.computeVertexNormals();

		let mesh;
		{
			const material = new THREE.MeshStandardMaterial({
				color: 0xffffff,
				roughness: 0.5,
				map: diffuseMap,
				normalMap: normalMap,
				normalMapType: THREE.ObjectSpaceNormalMap,
			});
			mesh = new THREE.Mesh(geometry, material);
			mesh.position.set(104.3, 160.1, -13);
			mesh.rotation.set(0, 0, -Math.PI * .155) //

			viewer.scene.scene.add(mesh);
		}

		viewer.onGUILoaded(() => {
			// Add entries to object list in sidebar
			let tree = _(`#jstree_scene`);
			let parentNode = "other";

			let meshID = tree.jstree('create_node', parentNode, {
				"text": "Temple of Castor and Pollux",
				"icon": `${Potree.resourcePath}/icons/triangle.svg`,
				"data": geometry
			},
				"last", false, false);
			tree.jstree(mesh.visible ? "check_node" : "uncheck_node", meshID);

		});
	});
	
	// Temple of Saturn
	loader.load(Potree.resourcePath + "../models/tos.ply", (geometry) => {
		const textureLoader = new THREE.TextureLoader();

		const diffuseMap = textureLoader.load(Potree.resourcePath + "../models/tos_tex.jpg");
		diffuseMap.encoding = THREE.sRGBEncoding;

		const normalMap = textureLoader.load(Potree.resourcePath + "../models/tos_norm.jpg");
		normalMap.encoding = THREE.sRGBEncoding;

		geometry.computeVertexNormals();

		let mesh;
		{
			const material = new THREE.MeshStandardMaterial({
				color: 0xffffff,
				roughness: 0.5,
				map: diffuseMap,
				normalMap: normalMap,
				normalMapType: THREE.ObjectSpaceNormalMap,
			});
			mesh = new THREE.Mesh(geometry, material);
			mesh.position.set(9.2, 30.5, -7);
			mesh.rotation.set(0, 0, -Math.PI * .69) // 

			viewer.scene.scene.add(mesh);
		}

		viewer.onGUILoaded(() => {
			// Add entries to object list in sidebar
			let tree = _(`#jstree_scene`);
			let parentNode = "other";

			let meshID = tree.jstree('create_node', parentNode, {
				"text": "Temple of Saturn",
				"icon": `${Potree.resourcePath}/icons/triangle.svg`,
				"data": geometry
			},
				"last", false, false);
			tree.jstree(mesh.visible ? "check_node" : "uncheck_node", meshID);

		});
	});

	// Temple of Vespasian and Titus
	loader.load(Potree.resourcePath + "../models/tovat.ply", (geometry) => {
		const textureLoader = new THREE.TextureLoader();

		const diffuseMap = textureLoader.load(Potree.resourcePath + "../models/tovat_tex.jpg");
		diffuseMap.encoding = THREE.sRGBEncoding;

		const normalMap = textureLoader.load(Potree.resourcePath + "../models/tovat_norm.jpg");
		normalMap.encoding = THREE.sRGBEncoding;

		geometry.computeVertexNormals();

		let mesh;
		{
			const material = new THREE.MeshStandardMaterial({
				color: 0xffffff,
				roughness: 0.5,
				map: diffuseMap,
				normalMap: normalMap,
				normalMapType: THREE.ObjectSpaceNormalMap,
			});
			mesh = new THREE.Mesh(geometry, material);
			mesh.position.set(-17.6, 20, -10.5);
			mesh.rotation.set(0, 0, -Math.PI * 1.69) // 

			viewer.scene.scene.add(mesh);
		}

		viewer.onGUILoaded(() => {
			// Add entries to object list in sidebar
			let tree = _(`#jstree_scene`);
			let parentNode = "other";

			let meshID = tree.jstree('create_node', parentNode, {
				"text": "Temple of Vespasian and Titus",
				"icon": `${Potree.resourcePath}/icons/triangle.svg`,
				"data": geometry
			},
				"last", false, false);
			tree.jstree(mesh.visible ? "check_node" : "uncheck_node", meshID);

		});
	});

</script>