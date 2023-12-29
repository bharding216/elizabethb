<svelte:head>
	<title>Work</title>
	<meta name="description" content="Our portfolio" />
</svelte:head>

<script>
	let images = [
	  '/greystone/_DSC3010.jpg',
	  '/greystone/_DSC2912.jpg',
	  '/greystone/_DSC2979.jpg',
	  '/greystone/_DSC3284.jpg'
	];
  
	let selectedImage = null;
  
	function openOverlay(image) {
	  selectedImage = image;
	}
  
	function closeOverlay() {
	  selectedImage = null;
	}
  </script>
  
  <div class="grid">
	{#each images as image}
    <button on:click={() => openOverlay(image)} class="image-button">
		<img src={image} alt="Portfolio" class="portfolio-image" />
	</button>
	{/each}
  </div>
  
  {#if selectedImage !== null}
  <button class="overlay" on:click={closeOverlay}>
    <div class="overlay-content">
      <img src={selectedImage} alt="Maximized" class="maximized-image" />
    </div>
  </button>
{/if}

<style>
	.grid {
	  display: grid;
	  grid-template-columns: repeat(2, 1fr);
	  gap: 16px;
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
  </style>