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
        <span class="love-letter" title="thank you for visiting my portfolio! ❤️, dianella sy">💌</span>   <!-- The love letter icon displays a tooltip on hover -->
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
    }

    .banner-left,
    .banner-center,
    .banner-right {
        flex: 1;    /* Each section takes an equal share of the available space */
    }

    .banner-left {
        text-align: left;   /* Align content to the left in the left section */
    }

    .banner-center {
        text-align: center; /* Center align content in the center section */
    }

    .banner-right {
        text-align: right;  /* Align content to the right in the right section */
        display: flex;  /* Uses flexbox for layout */
        justify-content: flex-end;  /* Aligns links to the right */
        flex-wrap: wrap;    /* Allows links to wrap to a new line if needed */
        gap: 0.5rem;    /* Adds space between links */
    }

    .love-letter {
        /* Styling for the love letter icon in the left section */
        font-size: 1.5rem;  /* Increase the love letter icon's size for better visibility */
        cursor: default;    /* Use the default cursor since the element is not clickable */
    }

    .nav-item {
        /* Styling for the navigation links in the right section */
        text-decoration: none;  /* Remove the default underline from links */
        color: #333;    /* Dark gray text color */
        font-weight: bold;  /* Bold font weight for emphasis */
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
        }
    }
</style>