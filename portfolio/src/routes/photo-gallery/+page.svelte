<script lang="ts">
    import { goto } from '$app/navigation'; // Import the SvelteKit navigation function to programatically route the user

    let video_element: HTMLVideoElement | null = null;  // Declare a variable named video_element with an explicit type; the element is HTMLVideoElement or null when not yet bound

    function playVideo() {  // Function to start the video when the mouse hovers over it
        if (video_element) video_element.play() // Check that the video element exists before calling its play() method
    }

    function pauseVideo() { // Function to pause the video when the mouse leaves it, and reset its playback time
        if (video_element) {
            video_element.pause();  // Pause the video
            video_element.currentTime = 0;  // Reset the video's current time to 0 so it starts over
        }
    }

    function navigateToHome() { // Function to navigate to the home page when the video is clicked
        goto('/');  // Use the goto function to navigate to the root path
    }
</script>


<div class="banner">    <!-- Main banner container that will always stay at the top of the viewport -->
    <div class="banner-left">   <!-- Left section contains a love letter icon with a tooltip using the title attribute -->
        <div class="love-letter-container"> <!-- The love letter container wraps both the love letter and tooltip -->
            <span class="love-letter">💌</span> <!-- This is the main love letter icon that remains visible -->
            <div class="tooltip">   <!-- The tooltip appears when hovering over the love letter container -->
                <span class="tooltip-icon">💌</span>    <!-- The left side contains a small rectangle containing the love letter -->
                <span class="tooltip-text">Thank you for visiting my portfolio! ❤️, Dianella Sy</span>  <!-- The right side contains the textual message -->
            </div>
        </div>
    </div>

    <div class="banner-center"> <!-- Center section contains an interactive video element -->
        <video
            bind:this={video_element}
            src="/banner/name_banner.mp4"
            poster="/banner/name_banner.png"
            on:mouseover={playVideo}
            on:focus={playVideo}
            on:mouseout={pauseVideo}
            on:blur={pauseVideo}
            on:click={navigateToHome}
            muted
            loop
            tabindex="0"
        >
            Your browser does not support the video tag.
        </video>
    </div>

    <div class="banner-right">  <!-- Right section contains navigation links to different pages -->
        <a class="nav-item" href="/">Home</a>
        <a class="nav-item" href="/about-me">About Me</a>
        <a class="nav-item" href="/projects">Projects</a>
        <a class="nav-item" href="/photo-gallery">Photo Gallery</a>
    </div>
</div>


<style>
    .banner {
        /* Style for the banner container */
        position: fixed;    /* Fix the banner's position relative to the viewport so it does not scroll */
        top: 0; /* Position it at the very top of the page */
        left: 0;    /* Align it to the left edge of the viewport */
        width: 100%;    /* Make the banner span the entire width of the viewport */
        display: flex;  /* Use Flexbox for arranging child elements horizontally */
        justify-content: space-between; /* Evenly distribute the space between the left, center, and right sections */
        align-items: center;    /* Vertically center the content */
        padding: 1rem 2rem; /* Add padding inside the banner (1rem top/bottom, 2rem left/right) */
        background-color: #f0f0f0;  /* Light gray background color */
        z-index: 1000;  /* High z-index ensures the banner stays above other content */
        overflow: visible;  /* Allow overflowing content like tooltips */
    }

    .banner-left {
        flex: 0 1 auto; /* Only takes as much space as its content needs */
        text-align: left;   /* Align content to the left in the left section */
    }

    .banner-center {
        flex: 0 1 auto; /* Only as much width as needed by the video */
        text-align: center; /* Center align content in the center section */
        margin: 0 1rem;    /* Provides some horizontal spacing */
    }

    .banner-right {
        flex: 0 1 auto; /* Grow the right section if needed */
        margin-left: auto;  /* Push it to the far right */
        text-align: right;  /* Align content to the right in the right section */
        display: flex;  /* Uses flexbox for layout */
        align-items: center;    /* Center links vertically */
        gap: 1.6rem;    /* Adds space between links */
        min-width: 0;   /* Allows the section to shrink if needed  */
        transform: translateX(-50px);   /* This moves the links 20px to the left */
    }

    .love-letter-container {
        /* Love letter container to allow tooltip positioning */
        position: relative; /* Set to relative so that the tooltip can position absolutely within */
        display: inline-block;  /* Ensures the container fits the content size */
        overflow: visible;  /* Prevent clipping of tooltip */
    }

    .love-letter {
        /* Styling for the love letter icon in the left section */
        font-size: 1.5rem;  /* Increase the love letter icon's size for better visibility */
        cursor: default;    /* Use the default cursor since the element is not clickable */
    }

    .tooltip {
        /* Tooltip container styling */
        visibility: hidden; /* Hide the tooltip initially */
        opacity: 0; /* Fully transparent initially */
        background-color: #24292e;  /* Dark background */
        color: #fff;    /* White text */
        border-radius: 6px; /* Rounded corners for a smooth look */
        padding: 0.5rem 0.75rem;    /* Padding inside the tooltip */
        position: absolute; /* Position relative to the love-letter-container */
        bottom: 120%;   /* Position the tooltip above the heart */
        left: 50%;  /* Center the tooltip horizontally over the heart */
        transform: translateX(-50%);    /* Adjust centering by moving left 50% of its own width */
        transition: opacity 0.3s ease, visibility 0.3s ease;    /* Fade in/out transition for smooth appearance */
        display: flex;  /* Use flexbox to align tooltip icon and text */
        align-items: center;    /* Vertically center the tooltip content */
        white-space: nowrap;    /* Prevent text from wrapping */
        font-size: 0.85rem; /* Smaller font size for the tooltip text */
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);   /* Add subtle shadow for a raised effect */
        z-index: 10000; /* High z-index to ensure it sits above other elements */
    }

    .tooltip::after {
        /* Tooltip arrow styling using a pseudo-element */
        content: "";    /* Empty content - used purely for decoration */
        position: absolute; /* Position absolutely within the tooltip */
        top: 100%;  /* Place the arrow at the bottom of the tooltip */
        left: 50%;  /* Center the arrow horizontally */
        transform: translateX(-50%);    /* Adjust centering */
        border-width: 5px;  /* Define the size of the arrow */
        border-style: solid;    /* Use solid borders to create the triangle arrow */
        border-color: #24292e transparent transparent transparent;  /* Arrow color matches tooltip background */
    }

    .love-letter-container:hover .tooltip {
        /* Show the tooltip when the love-letter-container is hovered */
        visibility: visible;    /* Make the tooltip visible on hover */
        opacity: 1; /* Set opacity to fully opaque */
    }

    .tooltip-icon {
        /* Styling for the left rectangle inside the tooltip that contains a small love letter icon */
        display: flex;  /* Use flexbox to center the icon */
        align-items: center;    /* Vertically center the love letter icon */
        justify-content: center;    /* Horizontally center the love leter icon */
        background-color: #ff4d4d;  /* Red background to match the love letter theme */
        color: #fff;    /* White text color */
        width: 1.2rem;  /* Fixed width for the icon container */
        height: 1.2rem; /* Fixed height for the icon container */
        border-radius: 3px; /* Slightly rounded corners */
        margin-right: 0.5rem;   /* Margin to separate the icon from the text */
        font-size: 0.8rem;  /* Reduced font size for the icon */
    }

    .tooltip-text {
        /* Tooltip text styling */
        display: inline-block;  /* Display as inline block so it stays with the icon */
    }

    .nav-item {
        /* Styling for the navigation links in the right section */
        text-decoration: none;  /* Remove the default underline from links */
        color: #333;    /* Dark gray text color */
        font-weight: bold;  /* Bold font weight for emphasis */
        white-space: nowrap;    /* Prevent the text from wrapping */
    }

    .nav-item:hover {
        text-decoration: underline; /* Underline the navigation links on hover for a visual cue */
    }

    .banner-center video {
        /* Styling for the video element in the center section */
        height: 60px;   /* Set a fixed height for the video */
        cursor: pointer;    /* Change the cursor to a pointer to indicate it is clickable */
        transition: transform 0.2s ease; /* Add a smooth transition for scaling on hover */
    }

    .banner-center video:hover,
    .banner-center video:focus {
        transform: scale(1.05); /* On hover, scale the video element slightly to create a zoom effect */
    }

    /* Responsive tweaks for smaller screens */
    @media screen and (max-width: 600px) {
        .banner {
            flex-direction: column;
            padding: 0.5rem 1rem;
        }

        .banner-right {
            justify-content: center;
            margin-top: 0.5rem;
            gap: 1rem;
        }
    }
</style>