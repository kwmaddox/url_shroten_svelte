<script>
	window.history.replaceState(null, null, '')

	let url
	$: urlParams = new URLSearchParams(window.location.search)
	$: urlToken = urlParams.get('url')

	function handleSubmit(event) {
		url = document.getElementById('url').value
		urlToken = Math.random().toString(36).substring(2,8)
		window.history.pushState(urlToken, null, '?url='+urlToken)

	}

	window.onpopstate = (event) => {
		urlToken = event.state
	}



</script>

<style>

</style>

{#if urlToken}
	<h1>{url}</h1>
	<p>{urlToken}</p>
{:else}
	<form on:submit|preventDefault={handleSubmit}>
		<input type="text" name="url" placeholder="url" alt="url" id="url">
		<input type="submit" value="Shorten URL">
	</form>
{/if}
