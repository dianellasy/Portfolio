<style> 
    /* Style block for component-specific styling */
    .header {   
        /* Define styles for the header container */
        display: flex;  /* Use flexbox layout to easily align children */
        justify-content: center;    /* Center content horizontally */
        align-items: center;    /* Center content vertically */
        padding-top: 20px;  /* Add top padding to create space from the top edge */
    }

    .header img {   
        /* Define styles for the image inside the header */
        max-width: 800px;   /* Limit the image's maximum width to 800px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
    }
</style>


<header class = "header">   <!-- Create a header element with the class "header" for centering the image -->
    <img src="home_page_name_banner.png" alt="Logo" />   <!-- Insert the home_page_name_banner image from the static folder with alternative text -->
</header>