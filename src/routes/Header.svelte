<script>
	import { page } from '$app/stores';
</script>

<header>
	<nav class="navbar sticky-top navbar-expand-lg navbar-custom static-top">
		<div class="container">
			<!--Logo to the left-->
			<a class="navbar-brand" href="/">X
			</a>

			<button class="navbar-toggler" 
				type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
				aria-controls="navbarSupportedContent" aria-expanded="false" 
				aria-label="Toggle navigation">
				<span class="navbar-toggler-icon"></span>
			</button>

			<!--Links to the right-->
			<div class="navbar-collapse collapse" id="navbarSupportedContent">
				<ul class="navbar-nav ms-auto me-5">
					<li aria-current={$page.url.pathname === '/work' ? 'page' : undefined} class="nav-item">
						<a href="/work" class="nav-link">Work</a>
					</li>

					<li aria-current={$page.url.pathname === '/about' ? 'page' : undefined} class="nav-item">
						<a href="/about" class="nav-link">About</a>
					</li>

					<li aria-current={$page.url.pathname === '/inquire' ? 'page' : undefined} class="nav-item">
						<a href="/inquire" class="nav-link">Inquire</a>
					</li>
				</ul>
			</div>
		</div>
	</nav>
</header>

<style>
  .navbar-nav a {
    text-transform: uppercase;
  }
</style>
