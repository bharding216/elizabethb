<script>
	import Slideshow from '/src/components/Slideshow.svelte';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<Slideshow />
</section>

<div>
	<p class="home-page-quote">Beauty and comfort is what we keep in mind as we collaborate together to design a space that is personal and distinct for you and your home.</p>
</div>

<style>
	.home-page-quote {
		font: 1.5em 'Lato', sans-serif;
		font-size: 2.0em;
		text-align: center;
		padding: 100px 100px 0px;
	}
</style>
