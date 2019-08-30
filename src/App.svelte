<script>
	import hexToRgba from 'hex-to-rgba';

	let color = '#000000';

	function getColorValues(color, rgbVal) {
		const rgb = hexToRgba(color).match(/\((.*)\)/)[1].split(',');

		if(rgbVal === 'r') {
			return `rgb(${rgb[0]}, 00, 00)`
		}

		if(rgbVal === 'g') {
			return `rgb(00, ${rgb[1]}, 00)`
		}

		if(rgbVal === 'b') {
			return `rgb(00, 00, ${rgb[2]})`
		}
	}
</script>

<style>
	:global(body),
	:global(html) {
		height: 100vh;
		width: 100vw;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	* {
		transition: .5s;
	}

	h1 {
		font-size: calc(3rem + 2vh + 2vw);
		margin-bottom: 3rem;
		position: relative;
		color: transparent;
	}

	h1:after {
		color: gray;
		content: '(hover to see rgb)';
		text-align: center;
		font-size: 1rem;
		position: absolute;
		top: calc(100% + .5rem);
		left: 0;
		right: 0;
		width: 100%;
	}

	h1:hover {
		color: gray;
		cursor: help;
	}

	h1 span {
		display: block;
		position: absolute;
		width: 100%;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		mix-blend-mode: multiply;
		transform-origin: center center;
	}

	h1:hover span:nth-child(1) {
		transform: translate(0, -1em);
	}

	h1:hover span:nth-child(2) {
		transform: translate(-3em, 1em);
	}

	h1:hover span:nth-child(3) {
		transform: translate(3em, 1em);
	}

	input[type="color"] {
		height: 5rem;
		width: 5rem;
	}
	input[type="color"]:hover {
		cursor: pointer;
	}
</style>

<h1 style="color: {color ? color : 'gray'};">
	{color}
	<span style="color: {color ? getColorValues(color, 'r') : 'gray'};">
		{color}
	</span>
	<span style="color: {color ? getColorValues(color, 'g') : 'gray'};">
		{color}
	</span>
	<span style="color: {color ? getColorValues(color, 'b') : 'gray'};">
		{color}
	</span>
</h1>

<input type="color" bind:value="{color}" />
