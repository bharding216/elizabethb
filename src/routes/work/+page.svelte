<svelte:head>
	<title>Work</title>
	<meta name="description" content="Our portfolio" />
</svelte:head>

<script>

	let categories = ['greystone', 'hill_country', 'jrc', 'office'];
	let selectedImage = null;
	let selectedCategoryImages = [];
  	let currentIndex = 0;
  
	function openOverlay(category) {
		selectedCategoryImages = Array.from({ length: 5 }, (_, imageIndex) => `/${category}/${category}_${imageIndex}.jpg`);
		currentIndex = 0;
		selectedImage = selectedCategoryImages[currentIndex];
		document.body.classList.add('overlay-open');
	}

	function navigate(direction) {
		currentIndex = (currentIndex + direction + selectedCategoryImages.length) % selectedCategoryImages.length;
		selectedImage = selectedCategoryImages[currentIndex];
	}

	function closeOverlay() {
		selectedImage = null;
		document.body.classList.remove('overlay-open');
	}

	const nextImage = () => navigate(1);
	const prevImage = () => navigate(-1);

  </script>
  
  <div class="grid">
	{#each categories as category}
		<button on:click={() => openOverlay(category)} class="image-button">
			<img src={`/${category}/${category}_0.jpg`} alt="Portfolio" class="portfolio-image" />
			<p class="image-heading">{category.heading}</p>
		</button>
	{/each}
  </div>
  
  {#if selectedImage !== null}
	<div class="overlay">
		<button on:click={closeOverlay} class="close-button">✕</button>
		<button on:click={prevImage} class="prev">&#8249;</button>
		<div class="overlay-content">
			<img src={selectedImage} alt="Maximized" class="maximized-image" />
		</div>
		<button on:click={nextImage} class="next">&#8250;</button>
	</div>
	{/if}

<style>
	.grid {
	  display: grid;
	  grid-template-columns: repeat(2, 1fr);
	  gap: 16px;
	}

	@media screen and (max-width: 767px) {
		.grid {
			grid-template-columns: 1fr; /* Single column for small screens */
		}
	}
  
	.image-button {
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		border: none;
		padding: 0;
		margin: 0;
  }

	.portfolio-image {
	  width: 100%;
	  height: auto;
	}
  
	.overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.8);
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 1000;
		backdrop-filter: blur(10px);
	}
  
	.overlay-content {
		max-width: 80%;
		max-height: 80%;
		background-color: #fff; /* Set a background color for the content area */
		overflow: hidden; /* Hide content overflow */
		position: relative; /* Add relative positioning */
		border-radius: 8px; /* Optional: Add rounded corners */
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.5); /* Optional: Add box shadow for depth */
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.maximized-image {
	  width: 100%;
	  height: 100%;
	  object-fit: contain;
	}

    .prev, .next {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        font-size: 60px;
        cursor: pointer;
        border: none;
        background: none;
        color: rgb(255, 255, 255);
        outline: black;
        display: inline-block;
        background-color: none;
        padding: 8px;
    }

    .prev {
        left: 0;
    }

    .next {
        right: 0;
    }

	.close-button {
		position: absolute;
		top: 10px;
		right: 10px;
		font-size: 24px;
		cursor: pointer;
		background: none;
		border: none;
		color: white;
	}
  </style>