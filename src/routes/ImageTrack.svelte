<script lang="ts">
	import ImageCard from './ImageCard.svelte';

	import image_fallback from '$lib/images/IMG_3004.jpg';
	import { track_cards } from './track_cards';

	const imageTitle = 'Ionic Scroll';
	const imageText = 'The ionic scroll is cool';

	let track: HTMLElement;

	const handleMouseDown = (event: MouseEvent): void => {
		track.dataset.mouseDownAt = event.clientX.toString();
	};

	const handleMouseUp = (): void => {
		track.dataset.mouseDownAt = '0';
		track.dataset.prevPercentage = track.dataset.percentage ?? '';
	};

	const handleMouseMove = (event: MouseEvent): void => {
		if (track.dataset.mouseDownAt === '0') return;

		const mouseDelta = parseFloat(track.dataset.mouseDownAt ?? '0') - event.clientX;
		const maxDelta = window.innerWidth / 0.5;

		const percentage = (mouseDelta / maxDelta) * -100;
		const nextPercentageRaw = parseFloat(track.dataset.prevPercentage ?? '0') + percentage;
		const nextPercentage = Math.max(Math.min(nextPercentageRaw, 0), -100);

		track.dataset.percentage = nextPercentage.toString();

		track.animate(
			{ transform: `translate(${nextPercentage}%, -50%)` },
			{ duration: 1200, fill: 'forwards' }
		);

		const images = track.getElementsByClassName('image');
		for (let i = 0; i < images.length; i++) {
			const image = images[i] as HTMLElement;
			image.animate(
				{ objectPosition: `${100 + nextPercentage}% center` },
				{ duration: 1200, fill: 'forwards' }
			);
		}
	};
</script>

<div
	class="image-track"
	draggable="false"
	data-mouse-down-at="0"
	data-prev-percentage="0"
	on:mousemove={handleMouseMove}
	on:mousedown={handleMouseDown}
	on:mouseup={handleMouseUp}
	bind:this={track}
>
	{#each track_cards as card}
		<ImageCard imageSrc={card.image_source} imageTitle={card.title} imageText={card.text} />
	{/each}
	<ImageCard imageSrc={image_fallback} {imageTitle} {imageText} />

</div>

<style>
	.image-track {
    display: flex;
    gap: 4vmin;
    position: absolute; 
    left: 50%;
    top: 50%;
    transform: translate(0%, -50%);
    transition: opacity 400ms ease;
}

</style>
