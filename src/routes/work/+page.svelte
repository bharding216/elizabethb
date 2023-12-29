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
	}

	function navigate(direction) {
		currentIndex = (currentIndex + direction + selectedCategoryImages.length) % selectedCategoryImages.length;
		selectedImage = selectedCategoryImages[currentIndex];
	}

	const nextImage = () => navigate(1);
	const prevImage = () => navigate(-1);

  </script>
  
  <div class="grid">
	{#each categories as category}
		<button on:click={() => openOverlay(category)} class="image-button">
			<img src={`/${category}/${category}_0.jpg`} alt="Portfolio" class="portfolio-image" />
		</button>
	{/each}
  </div>
  
  {#if selectedImage !== null}
	<div class="overlay">
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
	}
  
	.overlay-content {
	  max-width: 80%;
	  max-height: 80%;
	}
  
	.maximized-image {
	  width: 100%;
	  height: auto;
	}

    .prev, .next {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        font-size: 40px;
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
  </style>