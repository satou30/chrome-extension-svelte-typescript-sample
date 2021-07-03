<script>
	export let title;
	export let url;

	async function handleClick() {
		try {
			await navigator.clipboard.writeText(`${title}\n${url}`);
		} catch (err) {
			console.error("Failed to copy: ", err);
		}
	}
</script>

<div class="button-content">
	<button class="button" on:click={handleClick}>Copy</button>
</div>

<style>
	.button-content {
		width: 100%;
		text-align: right;
	}
	.button {
		margin: 18px 10px 0 0;
		padding: 10px 18px;
		background-color: #dee7e6;
		color: #002227;
		border: none;
		border-radius: 4px;
	}
</style>