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

    .top-right {
        /* Define styles for the clickable image positioned at the top right */
        position: absolute; /* Position it relative to the viewport */
        top: 0; /* Align to the top edge */
        right: 0;    /* Align to the right edge */
        margin: 10px;   /* Add spacing from the top and left edges */
        display: flex;  /* Use flexbox layout to arrange items horizontally */
        align-items: center;    /* Vertically align the images inside the container */
    }

    .github-icon {
        /* Define styles for the GitHub icon */
        max-width: 45px;   /* Limit the image width to 45px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
        cursor: pointer;    /* Change the cursor on hover to indicate clickability */
        margin-left: 15px;  /* Add a left margin of 15px */
    }

    .linkedin-icon {
        /* Define styles for the LinkedIn icon */
        max-width: 65px;   /* Limit the image width to 65px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
        cursor: pointer;    /* Change the cursor on hover to indicate clickability */
    }
</style>


<div class="top-right">
    <!-- Container for the two clickable images in the top-right corner -->
    <a 
        href="https://www.linkedin.com/in/dianellasy/"
        target="_blank"
        rel="noopener noreferrer"
    >
        <img class="linkedin-icon" src="linkedin_icon.jpg" alt="Linkedin Icon" />
    </a>

    <a 
        href="https://github.com/dianellasy"
        target="_blank"
        rel="noopener noreferrer"
    >
        <img class="github-icon" src="github_icon.png" alt="GitHub Icon" />
    </a>
</div>

<header class = "header">   <!-- Create a header element with the class "header" for centering the image -->
    <img src="home_page_name_banner.png" alt="Logo" />   <!-- Insert the home_page_name_banner image from the static folder with alternative text -->
</header>