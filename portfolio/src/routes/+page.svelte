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
        flex-direction: column; /* Stack children vertically, so the name banner GIF is on top and the three buttons are below */
        justify-content: center;    /* Center content horizontally */
        align-items: center;    /* Center content vertically */
        height: 100vh;  /* Make the container fill the entire viewport height */
        width: 100%;    /* Ensure the container spans the full width */
    }

    .middle-container video {
        /* Define styles for the name banner video element inside the middle container */
        max-width: 1000px;   /* Limit the image width to 1000px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
    }

    .button-container {
        /* Define a container for the three buttons placed below the image */
        margin-top: 20px;   /* Create some space between the image and the buttons */
        display: flex;  /* Use flexbox to line up the buttons next to each other */
        gap: 10px;  /* Add horizontal space between each button */
        transform: translateX(-34px);    /* Shift the entire button container 34px left */
    }

    .button-container button {
        /* Define styles for each button */
        padding: 10px 20px; /* Give the button some padding */
        font-size: 16px;    /* Set 16px as the text size for the buttons */
        border: none;   /* Remove the default button border */
        border-radius: 5px; /* Add rounded corners */
        background-color: pink; /* Set a pink background color */
        color: black;   /* Set black as the text color */
        cursor: pointer;    /* Change the mouse cursor when hovering over the button */
        transition: background-color 0.3s ease;  /* Smooth transition for hover effects */
    }

    .button-container button:hover {
        /* Hover effect to darken the background of the button */
        background-color: hotpink;  /* Hot Pink on hover */
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
     <!-- Container for the name banner video, positioned using the .middle-container class -->
     <video autoplay loop muted playsinline>
            <!-- Video element configured to autoplay, loop, be muted and play inline -->
            <source src="/home/name_banner.mp4" type="video/mp4">
            Your browser does not support the video tag.
         </video>

     <div class="button-container">
        <!-- Container for the three buttons placed underneath the image -->     
         <button>𐙚 About Me</button>
         <button>𐙚 Projects</button>
         <button>𐙚 Photo Gallery</button>
     </div>
</div>


<div class="bottom-right">
    <!-- Container for the GIF, positioned using the .bottom-right class -->
     <img src="/home/bottom_right_flicker.gif" alt="Bottom Right Flicker GIF" />
</div>