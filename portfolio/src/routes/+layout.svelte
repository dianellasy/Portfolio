<script>
	// Import the page store from SvelteKit to access the current URL and route information
	import { page } from '$app/stores';
</script>

<!-- Render the content of the current page using the slot -->
<slot />

<!-- Conditionally render the footer only if the current page is not the home page -->
{#if $page.url.pathname !== '/'}
<!-- Container for the footer with the class 'footer' -->
<div class="footer">
	<!-- Paragraph element containing the copyright text -->
	<p>© 2026 Dianella Sy</p>
</div>
{/if}

<style>
	/* Styles for the footer container */
	.footer {
		/* Use flexbox for layout */
		display: flex;
		/* Center content horizontally */
		justify-content: center;
		/* Center content vertically */
		align-items: center;
		/* Add padding around the footer */
		padding: 20px;
		/* Set font size for the text */
		font-size: 16px;
		/* Set text color to white */
		color: white;
		/* Set background color to dark grey */
		background-color: #202020;
		/* Make the footer span the full width of the screen */
		width: 100%;
		/* Set the font family to Open Sans */
		font-family: 'Open Sans', sans-serif;
	}

	/* Styles for the paragraph inside the footer */
	.footer p {
		/* Remove default margin from the paragraph */
		margin: 0;
	}
</style>