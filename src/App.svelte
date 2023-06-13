<script>
  import { onMount } from 'svelte';
	import QRCode from 'qrcode'

	let value = '';

  function render(url) {
		value = url;
		QRCode.toCanvas(document.getElementById('canvas'), url, {
			errorCorrectionLevel: 'H',
			width: 200,
			margin: 0,
			color: {
				dark:"#000000",
				light:"#ffffff"
			}
		});
  }
  
  onMount(() => {
		if (typeof browser !== "undefined") {
			browser.tabs.query({currentWindow: true, active: true})
				.then((tabs) => render(tabs[0].url))
		}
		else {
			render(window.location.href)
		}
		document.getElementById("url").focus();
	});
</script>

<main>
	<canvas id="canvas"></canvas>
	<input readonly value={value} id="url">
</main>

<style>
	main {
		text-align: center;
		width: 200px;
		margin: 0 auto;
	}

	#canvas, #url{
		min-width: 100%;
	}

	#url {
		font-family: inherit;
		font-size: 0.7em;
		-webkit-padding: 0.2em 0;
		padding: 0;
		margin: 0;
		box-sizing: border-box;
		border: 1px solid #ccc;
		border-radius: 2px;
	}
</style>