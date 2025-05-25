<style> 
    /* Style block for component-specific styling */
    .top-left {
        /* Position its content at the top left of the viewport */
        position: absolute; /* Position it relative to the viewport */
        top: 0; /* Align to the top edge */
        left: 0;    /* Align to the left edge */
    }

    .top-left img {
        /* Define styles for the flicker GIF inside the top-left container */
        max-width: 466px;   /* Limit the image width to 466px */
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

    .middle-container {
        /* Define a container that will fill the entire viewport and center its content */
        display: flex;  /* Use flexbox to center content */
        justify-content: center;    /* Center content horizontally */
        align-items: center;    /* Center content vertically */
        height: 100vh;  /* Make the container fill the entire viewport height */
        width: 100%;    /* Ensure the container spans the full width */
    }

    .middle-container img {
        /* Define styles for the name banner GIF inside the middle container */
        max-width: 1000px;   /* Limit the image width to 1000px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
    }

    .bottom-right {
        /* Position its content at the bottom right of the viewport */
        position: absolute; /* Position it relative to the viewport */
        bottom: 0;  /* Align to the bottom edge */
        right: 0;   /* Align to the right edge */
    }

    .bottom-right img {
        /* Define styles for the flicker GIF inside the bottom-right container */
        max-width: 533px;   /* Limit the image width to 533px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
    }
</style>


<div class="top-left">
    <!-- Container for the GIF, positioned using the .top-left class -->
     <img src="/home/top_left_flicker.gif" alt="Top Left Flicker GIF" />
</div>


<div class="top-right">
    <!-- Container for the two clickable images in the top-right corner -->
    <a 
        href="https://www.linkedin.com/in/dianellasy/"
        target="_blank"
        rel="noopener noreferrer"
    >
        <img class="linkedin-icon" src="/home/linkedin_icon.jpg" alt="Linkedin Icon" />
    </a>

    <a 
        href="https://github.com/dianellasy"
        target="_blank"
        rel="noopener noreferrer"
    >
        <img class="github-icon" src="/home/github_icon.png" alt="GitHub Icon" />
    </a>
</div>


<div class="middle-container">
    <!-- Container for the GIF, positioned using the .middle-container class -->
     <img src="/home/name_banner.gif" alt="Name Banner GIF" />
</div>


<div class="bottom-right">
    <!-- Container for the GIF, positioned using the .bottom-right class -->
     <img src="/home/bottom_right_flicker.gif" alt="Bottom Right Flicker GIF" />
</div>