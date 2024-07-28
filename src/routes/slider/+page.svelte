<script>
	import { browser } from '$app/environment';

	if (browser) {
		const slideShow = document.querySelector('.slide-show');
		slideShow?.addEventListener('scroll', updateActiveIndicator);
		function updateActiveIndicator() {
			if (!slideShow) {
				return;
			}

			const { scrollLeft, clientWidth } = slideShow;
			const activeIndex = Math.round(scrollLeft / clientWidth);
			console.log({ scrollLeft, clientWidth, activeIndex });
		}
		updateActiveIndicator();
	}
</script>

<div class="slide-container">
	<div class="slide-show">
		<figure id="slide1" class="slide">
			<img src="/1.jpg" alt="first slide" />
		</figure>
		<figure id="slide2" class="slide">
			<img src="/2.jpg" alt="second slide" />
		</figure>
		<figure id="slide3" class="slide">
			<img src="/3.jpg" alt="third slide" />
		</figure>
	</div>
</div>

<style>
	.slide-container {
		--slide-width: 256px;
		--slide-height: 512px;
		--corner-radius: 16px;

		margin-inline: auto;
		border-radius: var(--corner-radius);
		width: var(--slide-width);
		height: var(--slide-height);
	}

	.slide-show {
		display: flex;
		overflow-x: scroll;
		scroll-snap-type: x mandatory;
		overscroll-behavior-x: contain;
	}

	.slide {
		flex-shrink: 0;
		margin: 0;
		scroll-snap-align: end;

		border-radius: var(--corner-radius);
		width: var(--slide-width);
		height: var(--slide-height);

		/* centering the content removes the vertical scrollbar */
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.slide > img {
		max-width: 100%;
		height: 100%;
		object-fit: cover;
	}
</style>
