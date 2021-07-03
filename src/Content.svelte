<script lang="ts">
	import ButtonContent from "./ButtonContent.svelte";
	let url: string | undefined = "";
	let title: string | undefined = "";
	type ContentItem = {
		title: string;
		text: string | undefined;
	};
	let contentItems: Array<ContentItem> = [];

	chrome.tabs.query({ active: true, lastFocusedWindow: true }, tabs => {
		const currentTab = tabs[0];
		url = currentTab.url;
		title = currentTab.title;
		contentItems = [
			{
				title: "Title",
				text: title,
			},
			{
				title: "Url",
				text: url,
			},
			{
				title: "Text to be copied",
				text: `${title}<br />${url}`,
			},
		];
	});
</script>

<div class="content">
	{#each contentItems as contentItem}
		<div class="content-section">
			<h2 class="content-title">{contentItem.title}</h2>
			<p class="content-text">{@html contentItem.text}</p>
		</div>
	{/each}
	<ButtonContent {title} {url} />
</div>

<style>
	.content {
		font-size: 18px;
		padding: 16px 8px;
	}
	.content-section:not(:last-child) {
		margin-bottom: 14px;
	}
	.content-title {
		font-size: 20px;
		margin: 8px;
	}
	.content-text {
		font-size: 14px;
		margin-left: 8px;
		margin-top: 4px;
		margin-bottom: 0px;
	}
</style>