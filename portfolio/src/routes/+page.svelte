<svelte:head>   <!-- The <svelte:head> block allows insertion of elements into the document head -->
    <title>Home - Dianella Sy's Portfolio</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />    <!-- Meta tag to ensure proper responsive scaling on mobile devices -->
</svelte:head>


<style> 
    /* Style block for component-specific styling */
    .top-left {
        /* Position its content at the top left of the viewport */
        position: absolute; /* Position it relative to the viewport */
        top: 0; /* Align to the top edge */
        left: 0;    /* Align to the left edge */
    }

    .top-left video {
        /* Define styles for the flicker GIF inside the top-left container */
        max-width: 270px;   /* Limit the image width to 466px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
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
        max-width: 1000px;   /* Limit the video width to 1000px */
        width: 100%;    /* Make the video responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the video's aspect ratio automatically */
    }

    a {
        text-decoration: none;  /* Remove default text decoration from links */
        margin-right: 10px; /* Adds space between the buttons */
    }

    .button-container {
        /* Define a container for the three buttons placed below the video */
        margin-top: 20px;   /* Create some space between the image and the buttons */
        display: flex;  /* Use flexbox to line up the buttons next to each other */
        gap: 10px;  /* Add horizontal space between each button */
        transform: translateX(-34px);    /* Shift the entire button container 34px left */
    }

    button {
        /* Define styles for each button */
        padding: 10px 20px; /* Give the button some padding */
        font-size: 16px;    /* Set 16px as the text size for the buttons */
        border: none;   /* Remove the default button border */
        border-radius: 5px; /* Add rounded corners */
        background-color: pink; /* Set a pink background color */
        color: black;   /* Set black as the text color */
        cursor: pointer;    /* Change the mouse cursor when hovering over the button */
    }

    button:hover {
        /* Hover effect to darken the background of the button */
        background-color: hotpink;  /* Hot Pink on hover */
    }

    .bottom-right {
        /* Position its content at the bottom right of the viewport */
        position: absolute; /* Position it relative to the viewport */
        bottom: 0;  /* Align to the bottom edge */
        right: 0;   /* Align to the right edge */
    }

    .bottom-right video {
        /* Define styles for the flicker GIF inside the bottom-right container */
        max-width: 270px;   /* Limit the image width to 533px */
        width: 100%;    /* Make the image responsive by scaling to 100% of its container */
        height: auto;   /* Preserve the image's aspect ratio automatically */
    }

    @media (max-width: 768px) {
        /* Responsive adjustments for screens up to 768px wide */
        .button-container {
            transform: none;    /* Remove the left shift on smaller screens */
            flex-direction: column; /* Stack buttons vertically instead of horizontally */
            align-items: center;    /* Center buttons horizontally */
            gap: 8px;   /* Decrease spacing between buttons */
        }

        button {
            font-size: 14px;    /* Reduce font size to suit smaller screens */
            padding: 8px 16px;  /* Adjust padding for better fit on small devices */
        }

        .top-left video,
        .bottom-right video {
            max-width: 100%;    /* Allow images to scale down fully on smaller screens */
        }

        .top-left, 
        .bottom-right {
            display: none;  /* Hides these elements on screens up to 768px */
        }
    }

    @media (max-width: 480px) {
        /* Further adjustments for very small screens up to 480px wide */
        .top-left,
        .bottom-right {
            display: none;  /* Ensures these elements remain hidden on very small screens */
        }
    }
</style>


<div class="top-left">
    <video 
        autoplay 
        loop 
        muted 
        playsinline
        disablepictureinpicture
        controlslist="nopictureinpicture noremoteplayback"
    >
        <!-- Container for the video, positioned using the .top-left class -->
        <source src="/home/top_left_flicker.mp4" type="video/mp4" />
        Your browser does not support the video tag.
    </video>
</div>


<div class="middle-container">
     <!-- Container for the name banner video, positioned using the .middle-container class -->
     <video 
        autoplay 
        loop 
        muted 
        playsinline
        disablepictureinpicture
        controlslist="nopictureinpicture noremoteplayback"
    >
        <!-- Video element configured to autoplay, loop, be muted and play inline -->
        <source src="/home/name_banner.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    
    <div class="button-container">
        <!-- Each button is wrapped in an <a> tag pointing to a different page route -->
        <a href="/about-me">
            <button>𐙚 About Me</button>
        </a>
        <a href="/projects">
            <button>𐙚 Projects</button>
        </a>
        <a href="/photo-gallery">
            <button>𐙚 Photo Gallery</button>
        </a>
    </div>
</div>


<div class="bottom-right">
    <!-- Container for the video, positioned using the .bottom-right class -->
    <video 
        autoplay 
        loop 
        muted 
        playsinline
        disablepictureinpicture
        controlslist="nopictureinpicture noremoteplayback"
    >
        <!-- Container for the video, positioned using the .top-left class -->
        <source src="/home/bottom_right_flicker.mp4" type="video/mp4" />
        Your browser does not support the video tag.
    </video>
</div>