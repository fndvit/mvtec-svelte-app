<script>
    import { Map, Geocoder, Marker, controls } from '@beyonk/svelte-mapbox'
    export let options;
    export let accessToken;
    export let layout;

    const { GeolocateControl, NavigationControl, ScaleControl } = controls;
    let map;
    options.showCompass = false;
</script>

<div class='graphic {layout}'>

    <Map
    {accessToken}
    bind:this={map}
    {options}
    >
    <NavigationControl {options} />
    </Map>

</div>

<style>
    :global(.mapboxgl-ctrl-group){
        box-shadow: rgba(0,0,0,.2) 1px 1px 9px!important;
    }
</style>

<!-- <script>
	import { onMount, setContext } from "svelte";
	import { mapbox, key } from "./mapbox.js";
    import * as d3Scale from "d3-scale";
    
    export let style;
    export let data;
    export let join;
    export let scale;

    export let bounds, pitch, bearing, zoom, center, minZoom, maxZoom, minPitch, maxPitch;
    export let interactive, bearingSnap, pitchWithRotate, clickTolerance, attributionControl, customAttribution, logoPosition, failIfMajorPerformanceCaveat, preserveDrawingBuffer, antialias, refreshExpiredTiles, maxBounds, scrollZoom, boxZoom, dragRotate, dragPan, keyboard, doubleClickZoom, touchZoomRotate, touchPitch, trackResize;
    export let locale, localFontFamily, localIdeographFontFamily;

	setContext(key, {
		getMap: () => map,
    });
    
	let container;
	let map;
    let color;
    
	onMount(() => {
		const link = document.createElement("link");
		link.rel = "stylesheet";
        link.href = "https://unpkg.com/mapbox-gl/dist/mapbox-gl.css";
        
		// const raw = fetch("/data/paro-registrado-201901.json")
		// 	.then((res) => res.json())
        //     .then((json) => (data = json));
            
		link.onload = () => {
			map = new mapbox.Map({
				container,
				style: style,
				center: [0, 0],
            });
            
			// const color = d3Scale
			// 	.scaleOrdinal()
			// 	.domain([0, 10, 50, 100])
            //     .range(["#f3f2ed", "#c9e0e7", "#9abbd4", "#6785b5", "#2b4389"]);
                
			map.on("load", () => {
				// const matchExpression = ["match", ["get", " mun"]];
				// for (const [key, value] of Object.entries(data)) {
				// 	const id = key.padStart(5, "0");
				// 	matchExpression.push(id, color(value["tot"]));
				// }
				// matchExpression.push("rgba(0, 0, 0, 0)");
				// map.setPaintProperty(
				// 	"Municipios",
				// 	"fill-color",
				// 	matchExpression
				// );

				map.on("mouseenter", "Municipios", function (e) {
					// Change the cursor style as a UI indicator.
					/* map.getCanvas().style.cursor = "pointer";
					var coordinates = e.features[0].geometry.coordinates.slice();
					var description = e.features[0].properties.description;
					// Ensure that if the map is zoomed out such that multiple
					// copies of the feature are visible, the popup appears
					// over the copy being pointed to.
					while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
						coordinates[0] +=
							e.lngLat.lng > coordinates[0] ? 360 : -360;
					}
					// Populate the popup and set its coordinates
					// based on the feature found.
					popup
						.setLngLat(coordinates)
						.setHTML(description)
						.addTo(map); */
				});
				map.on("mouseleave", "Municipios", function () {
					/* map.getCanvas().style.cursor = "";
					popup.remove(); */
				});
			});
        };
        
        document.head.appendChild(link);
        
		return () => {
			map.remove();
			link.parentNode.removeChild(link);
		};
	});
</script>

<style>
	body {
		margin: 0;
		padding: 0;
	}
	div {
		width: 100%;
		height: 100vh;
	}
	.map-overlay {
		font: 12px/20px "Helvetica Neue", Arial, Helvetica, sans-serif;
		position: absolute;
		width: 25%;
		top: 0;
		left: 0;
		padding: 10px;
	}
	.map-overlay .map-overlay-inner {
		background-color: #fff;
		box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
		border-radius: 3px;
		padding: 10px;
		margin-bottom: 10px;
	}
</style>
<div bind:this={container}>
    {#if map}
        <slot />
    {/if}
</div> -->