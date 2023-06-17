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
		}, (err, canvas) =>!err && drawCat(canvas));
  }

	function drawCat(canvas) {
		const ctx = canvas.getContext("2d");
		const pi = Math.PI;
		const mid = ctx.canvas.width/2;
		const circleDiameter = 0.2 * ctx.canvas.width
		const catWidth = 0.7 * circleDiameter;
		const catHeight = 0.55 * circleDiameter;
		const leftOfFace = () => (ctx.canvas.width - catWidth)/2;
		const rightOfFace = () => leftOfFace() + catWidth;
		const centerOfFaceX = () => mid;
		const centerOfFaceY = () => mid+2;
		const eyeRadius = 0.05 * catWidth;
  	const eyeOffsetY = 0.15 * catHeight;
		const whiskerLength = 0.2 * catWidth;
		
		// background container
		ctx.beginPath();
		ctx.fillStyle = "white";
		ctx.arc(mid,		mid,		circleDiameter/2,		0,		2*pi);
		ctx.fill();
		ctx.closePath();
		ctx.beginPath();
		ctx.fillStyle = "black";
		ctx.arc(mid,		mid,		circleDiameter/2,		0,		2*pi);
		ctx.stroke();

		// draw face
		ctx.beginPath();
		ctx.fillStyle = "black";
		ctx.ellipse(centerOfFaceX(),	centerOfFaceY(),		catWidth/2,		catHeight/2,		0,		0,		2*Math.PI,);
		ctx.fill();
		
		// left ear
		ctx.beginPath();	
		ctx.moveTo(leftOfFace(), centerOfFaceY());
		ctx.quadraticCurveTo(
			leftOfFace(),
			(ctx.canvas.height - 2.3*catHeight)/2,
			centerOfFaceX(),
			centerOfFaceY()
		);
		ctx.fill();

		// right ear
		ctx.beginPath();
		ctx.moveTo(rightOfFace(), centerOfFaceY());
		ctx.quadraticCurveTo(
			rightOfFace(),
			(ctx.canvas.height - 2.3*catHeight)/2,
			centerOfFaceX(),
			centerOfFaceY()
		);
		ctx.fill();
		ctx.closePath();
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