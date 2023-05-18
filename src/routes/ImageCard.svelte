<script lang="ts">
	export let imageSrc: string;
	export let imageTitle: string;
	export let imageText: string;
</script>

<div class="image-card" draggable="false">
	<img class="image" src={imageSrc} alt="" draggable="false" />
	<div class="image-details">
		<h3 class="image-title">{imageTitle}</h3>
		<p class="image-text">{imageText}</p>
	</div>
</div>

<style>
	.image-card:hover .image-details {
		top: 50%;
		left: 50%;
		opacity: 1;
	}

	.image {
		width: 40vmin;
		height: 62vmin;
		object-fit: cover;
		object-position: center;
	}

	.image-details {
		bottom: 0;
		text-align: center;
		padding-left: 1em;
		padding-right: 1em;
		width: 100%;
		opacity: 0;
		transition: opacity 350ms ease;
	}

	.image-details h3 {
		color: rgb(0, 0, 0);
		font-weight: 500;
		font-size: x-large;
		font-family: monospace;
		letter-spacing: 0.15em;
		margin-bottom: 0.2em;
	}

	.image-details p {
		color: rgb(3, 12, 19);
		font-size: large;
		font-family: monospace;
	}
</style>
