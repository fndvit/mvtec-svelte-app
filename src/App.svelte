<script>
	//Some components
	import Line from './components/charts/Line.svelte'
	import Area from './components/charts/Area.svelte'
	import Multiline from './components/charts/Multiline.svelte'
	import Scatter from './components/charts/Scatter.svelte'
	import Mapbox from './components/maps/Mapbox.svelte'
	import Map from './components/maps/Map.svelte'

	//Test data
	import world from './data/world.json';
	import cases from './data/covid-cases.json';
	import weather from './data/weather.json';
	import weather2 from './data/weather2.json';
	import weather3 from './data/weather3.json';

	import locale from '@reuters-graphics/d3-locale';
	import { geoWinkel3 } from 'd3-geo-projection';
	import { scaleQuantize } from 'd3-scale';
	import {extent} from 'd3-array';
	
	let color = '#5cc6b2';

	const loc = new locale('es');
	const format = {
		x: loc.formatTime('%b %e'),
        y: loc.format(',.1d'),
    }

	weather.forEach(d => d.time = new Date(d.time));
	weather2.forEach(d => d.time = new Date(d.time));

	const projection = geoWinkel3()
				.rotate([-11, 0])
				.precision(1);

	$: palette = () => {
		const _extent = extent(cases.data, d => d.latest.cases)
		const max = _extent[0] > _extent[1] ? _extent[0] : _extent[1];
		const min = _extent[0] < _extent[1] ? _extent[0] : _extent[1];
		const d = (max-min)/9;

		return scaleQuantize()
				.range(['#ffe461', '#ffc755', '#fea94d', '#f68c4a', '#ea704a', '#da554e', '#c73a55', '#ae1f5f', '#90006c'])
				.domain([... Array(9)].map((_d, i) => min + d * i))
				.nice();
	}

</script>

<main>

	<Multiline 
		data={weather2}
		title='Title' desc='Description'
		key={{x: 'time', y: ['ny1', 'sf1', 'au1']}}
		{format}
		color={['#fc0', '#036', '#f0c']}
		layout='col'
	/>

	<Line 
		data={weather}
		title='Title' desc='Description'
		key={{x: 'time', y: 'value'}}
		{format}
		{color}
		layout='col'
	/>

	<Area 
		data={weather}
		title='Title' desc='Description'
		key={{x: 'time', y: 'value'}}
		{format}
		{color}
		layout='col'
	/>

	<Scatter 
		data={weather3}
		title='Title' desc='Description'
		key={{x: 'pressure', y: 'temperatureHigh', size:'moonPhase'}}
		{format}
		{color}
		layout='col'
	/>
	
	<Mapbox 
		options={
			{style:'mapbox://styles/fndvit/ckc1oqzq94nh91imn76jqxcha',
			scrollZoom:false,
			center: [-7.889722,42.782222],
			zoom: 6.5}
		}
		accessToken='pk.eyJ1IjoiZm5kdml0IiwiYSI6ImNrYzBzYjhkMDBicG4yc2xrbnMzNXVoeDIifQ.mrdvw_7AIeOwa5IgHLaHJg'
		layout='wide'
	/>

	<Map 
		data={cases.data}
		map={world}
		geo='countries'
		scale={palette()}
		projection={projection}
    	join={{data:'geoid', map:'alpha3'}}
    	value=''
    	legend={{title: '', format: ''}}
		layout='wide'
	/>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	:global(.graphic) {
		height:50vh;
		margin-bottom:3rem;
	}
</style>