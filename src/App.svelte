<script>
  import { onMount } from 'svelte';
  import { default as QrCode } from 'qrious';

  const QRcode = new QrCode();
  let image = '';
	let value = '';

  function render(url) {
		value = url;
    QRcode.set({
      background: "#fff",
      foreground: "#000",
			padding: 0,
      size: 200,
      value,
    });
    image = QRcode.toDataURL('image/jpeg');
  }
  
  onMount(() => {
		if (typeof browser !== "undefined") {
			browser.tabs.query({currentWindow: true, active: true})
				.then((tabs) => {
					render(tabs[0].url);
				})
		}
		else {
			render(window.location.href)
		}
		document.getElementById("url").focus()
	});
</script>

<main>
	<img src={image} alt={value} id="qr"/>
	<input readonly value={value} id="url">
</main>

<style>
	main {
		text-align: center;
		max-width: 200px;
		margin: 0 auto;
	}

	#qr, #url{
		width: 100%;
	}

	#url {
		font-family: inherit;
		font-size: 0.7em;
		-webkit-padding: 0.2em 0;
		padding: 0.2em;
		box-sizing: border-box;
		border: 1px solid #ccc;
		border-radius: 2px;
	}


</style>