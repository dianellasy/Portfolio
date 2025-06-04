<script lang="ts">
    import { goto } from '$app/navigation'; // Import the SvelteKit navigation function to programatically route the user

    let video_element: HTMLVideoElement | null = null;  // Declare a variable named video_element with an explicit type; the element is HTMLVideoElement or null when not yet bound
    
    const messages = [
        "Thank you for visiting my portfolio! ❤️, Dianella Sy",
        'One quote I live by is, "If you chase your dreams, you can catch them" - Tadej Pogačar 👩🏻‍💻📝🎧❤️‍🔥',
        `Two of my favorite songs are "You Oughta Know" by Alanis Morisette and "Sweet Talkin' Woman" by ELO 🎸🎤🎶`,
        "My favorite hobbies include walking and riding my road bike on a trail, watching true crime shows, and spending time with my family and friends 🚵🏻‍♀️📺🫂"
    ];

    let tooltip_text = messages[0]; // Initialize the tooltip content with the first message
    let message_index = 0;  // A counter to track which message to show next
    let badge_count = messages.length;  // A badge count, initially the total number of messages

    function playVideo() {  // Function to start the video when the mouse hovers over it
        if (video_element) video_element.play() // Check that the video element exists before calling its play() method
    }

    function pauseVideo() { // Function to pause the video when the mouse leaves it, and reset its playback time
        if (video_element) {
            video_element.pause();  // Pause the video
            video_element.currentTime = 0;  // Reset the video's current time to 0 so it starts over
            video_element.load();   // Reset the video to its initial state
        }
    }

    function navigateToHome() { // Function to navigate to the home page when the video is clicked
        goto('/');  // Use the goto function to navigate to the root path
    }

    function updateTooltip() {  // Function sets the tooltip text to the message at the current index, then increments the index so that the next time the pointer enters, the next message in order is shown
        tooltip_text = messages[message_index]; // Set the tooltip text using the current index
        message_index = (message_index + 1) % messages.length;  // Increment the index and wrap around to 0 when reaching the end

        if (badge_count > 0) {
            badge_count = badge_count - 1;  // Decrement the badge count
        } else {
            badge_count = 0;    // Set to 0 if it reaches 0
        }
    }

    // Define an array of photo objects for the gallery
    // Each object contains data for one photo - source path, date, description, and optional stickers
    let photos = [
        {
            id: 1,  // Unique identifier for the photo
            src: '/photo-gallery/google_office_field_trip.jpg', // Source path for the image
            date: 'December 1, 2023',   // Date to display below the image
            description: 'Google Office Field Trip @ Irvine, California',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 2,  // Unique identifier for the photo
            src: '/photo-gallery/last_day_with_piyush.jpg', // Source path for the image
            date: 'December 7, 2023',   // Date to display below the image
            description: 'Last Office Hours with Piyush, a Senior Software Engineer at Google', // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 3,  // Unique identifier for the photo
            src: '/photo-gallery/summer_night_with_lea_and_celine.jpg', // Source path for the image
            date: 'August 23, 2024',   // Date to display below the image
            description: 'Touring my High School Friends, Lea and Celine, CSUF',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 4,  // Unique identifier for the photo
            src: '/photo-gallery/first_acmw_meeting.jpg', // Source path for the image
            date: 'September 25, 2024',   // Date to display below the image
            description: 'First Association for Computing Machinery-Women (ACM-W) Meeting',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 5,  // Unique identifier for the photo
            src: '/photo-gallery/fall_open_source_commencement.jpg', // Source path for the image
            date: 'December 5, 2024',   // Date to display below the image
            description: 'Fall Open Source Software Team Commencement',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 6,  // Unique identifier for the photo
            src: '/photo-gallery/discoverfest.jpg', // Source path for the image
            date: 'January 29, 2025',   // Date to display below the image
            description: 'Discover Fest',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 7,  // Unique identifier for the photo
            src: '/photo-gallery/selfie_after_intro_to_sveltekit_workshop.jpg', // Source path for the image
            date: 'February 27, 2025',   // Date to display below the image
            description: 'Selfie After Intro to SvelteKit Workshop',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 8,  // Unique identifier for the photo
            src: '/photo-gallery/working_on_project_at_fullyhacks.png', // Source path for the image
            date: 'April 12, 2025',   // Date to display below the image
            description: 'Working on our Video Game, Out of this World Cafe, @ FullyHacks 2025',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 9,  // Unique identifier for the photo
            src: '/photo-gallery/waiting_for_judging_at_fullyhacks.jpg', // Source path for the image
            date: 'April 13, 2025',   // Date to display below the image
            description: 'Waiting for Judging of our Video Game, Out of this World Cafe, @ FullyHacks 2025',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 10,  // Unique identifier for the photo
            src: '/photo-gallery/announcement_winning_best_game_project.png', // Source path for the image
            date: 'April 13, 2025',   // Date to display below the image
            description: 'Announcement that my Partner, Emily, and I Won Best Game Project',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 11,  // Unique identifier for the photo
            src: '/photo-gallery/spring_open_source_commencement.jpg', // Source path for the image
            date: 'May 1, 2025',   // Date to display below the image
            description: 'Spring Open Source Software Team Commencement',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 12,  // Unique identifier for the photo
            src: '/photo-gallery/whos_that_tuffy_keychain_blind_box.jpg', // Source path for the image
            date: 'May 8, 2025',   // Date to display below the image
            description: 'Redeemed Different Keychains of our School Mascot: Scholar Tuffy, Sanrio-Inspired Tuffy, Sporty Tuffy',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        },

        {
            id: 13,  // Unique identifier for the photo
            src: '/photo-gallery/senpais_and_team_leads.jpg', // Source path for the image
            date: 'May 8, 2025',   // Date to display below the image
            description: 'Former Team Leads and New Team Leads for ACM CSUF Open Source Team',  // Short description of the image
            leftSticker: '',    // Sticker that will appear on the top-left of the photo
            rightSticker: ''    // Sticker that will appear on the bottom-right of the photo
        }
    ];
</script>


<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=Open+Sans&display=swap"
        rel="stylesheet"
    />
</svelte:head>


<style>
    .banner {
        /* Style for the banner container */
        position: fixed;    /* Fix the banner's position relative to the viewport so it does not scroll */
        top: 0; /* Position it at the very top of the page */
        left: 0;    /* Align it to the left edge of the viewport */
        width: 100%;    /* Make the banner span the entire width of the viewport */
        height: 80px;   /* Fixed height */
        display: flex;  /* Use Flexbox for arranging child elements horizontally */
        justify-content: space-between; /* Evenly distribute the space between the left, center, and right sections */
        align-items: center;    /* Vertically center the content */
        /* background-color: #efb7ce;  /* Light gray background color */ 
        background-color: #202020;  /* Light gray background color */
        z-index: 1000;  /* High z-index ensures the banner stays above other content */
        overflow: visible;  /* Allow overflowing content like tooltips */
    }

    .banner-left {
        flex: 0 1 auto; /* Only takes as much space as its content needs */
        margin-left: 2rem;  /* Adds left spacing */
        z-index: 1010;
    }

    .banner-center {
        position: absolute; /* Remove from the flex flow */
        left: 50%;  /* Position left edge at 50% of the banner */
        transform: translateX(-50%);    /* Shift left half of the container's width to center it */
        z-index: 1005;  /* Ensure it appears between the left and right sections if needed */
    }

    .banner-right {
        flex: 0 1 auto; /* Grow the right section if needed */
        margin-right: 2rem;  /* Adds right spacing */
        z-index: 1010;
        text-align: right;  /* Align content to the right in the right section */
        display: flex;  /* Uses flexbox for layout */
        gap: 1.6rem;    /* Adds space between links */
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
        font-family: 'Open Sans', sans-serif;
    }

    .badge {
        /* Styling for the badge in the top right of the love letter */
        position: absolute; /* Position relative to the love letter container */
        top: -5px;  /* Move badge slightly above the love letter */
        right: -5px;    /* Move badge slightly to the right of the love letter */
        background-color: #ff3d7f; /* Pink background color */
        color: white;   /* White text color */
        width: 20px;    /* Fixed width for the circle */
        height: 20px;   /* Fixed height to make it a circle */
        border-radius: 50%; /* Fully round shape */
        display: flex;  /* Use flexbox for centering text */
        align-items: center;    /* Vertically center text */
        justify-content: center;    /* Horizontally center text */
        font-size: 12px;    /* Set font size for badge text */
        font-family: 'Open Sans', sans-serif;   /* Apply Open Sans font */
        pointer-events: none;   /* Ignore pointer events to let hover work on the container */
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
        left: 120%;  /* Position tooltip to the right of the love letter */
        top: 50%;   /* Center vertically relative to the love letter */
        transform: translateY(-50%);    /* Adjust vertical centering */
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
        top: 50%;  /* Center vertically on tooltip */
        left: -5px;  /* Place arrow on the left edge */
        transform: translateY(-50%);    /* Adjust vertical centering */
        border-width: 5px;  /* Define the size of the arrow */
        border-style: solid;    /* Use solid borders to create the triangle arrow */
        border-color: transparent #24292e transparent transparent;  /* Arrow color matches tooltip background */
    }

    .love-letter-container:hover .tooltip {
        /* Show the tooltip when the love-letter-container is hovered */
        visibility: visible;    /* Make the tooltip visible on hover */
        opacity: 1; /* Set opacity to fully opaque */
    }

    .tooltip-text {
        /* Tooltip text styling */
        display: inline-block;  /* Display as inline block so it stays with the icon */
        font-family: 'Open Sans', sans-serif;
    }

    .nav-item {
        /* Styling for the navigation links in the right section */
        text-decoration: none;  /* Remove the default underline from links */
        color: white;    /* Dark gray text color */
        font-weight: bold;  /* Bold font weight for emphasis */
        white-space: nowrap;    /* Prevent the text from wrapping */
        font-family: 'Open Sans', sans-serif;
    }

    .nav-item:hover {
        text-decoration: underline; /* Underline the navigation links on hover for a visual cue */
        color: #efb7ce;
    }

    .banner-center video {
        /* Styling for the video element in the center section */
        height: 78px;   /* Set a fixed height for the video */
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
            height: auto;   /* Let height adjust */
            font-family: 'Open Sans', sans-serif;
        }

        .banner-center {
            position: relative;
            left: 0;
            transform: none;
            margin: 0.5rem 0;
        }

        .banner-right {
            justify-content: center;
            margin: 0;
            gap: 1rem;
        }
    }

    .gallery {
        margin-top: 80px;   /* Push gallery 80px down to avoid the banner */
        display: grid;  /* Use CSS Grid for layout */
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));    /* Responsive grid columns */
        gap: 1.5rem;    /* Space between photo cards */
        padding: 1rem;  /* Padding around the gallery */
    }

    .photo-card {
        background: #222;   /* Dark background for contrast */
        border-radius: 8px; /* Rounded corners for a sleek look */
        overflow: hidden;   /* Hide any overflow content */
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);   /* Add a subtle shadow for depth */
        transition: transform 0.3s ease, box-shadow 0.3s ease;  /* Smooth transition for hover effect */
    }

    .photo-card:hover { /* Hover effect for the photo card */
        transform: translateY(-10px);   /* Move the card up by 10px */
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);  /* Enhance shadow for depth effect */
    }

    .photo-wrapper {
        position: relative; /* Relative position sets the context for absolute children */
    }

    img {
        width: 100%;    /* Make image fill the width of its container */
        display: block; /* Remove inline spacing below the image */
    }

    .sticker {
        position: absolute; /* Absolutely position the sticker on the image */
        font-size: 2rem;    /* Large font size for visibility */
    }

    .sticker.left {
        top: 8px;   /* 8px distance from the top edge */
        left: 8px;  /* 8px distance from the left edge */
    }

    .sticker.right {
        bottom: 8px;    /* 8px distance from the bottom edge */
        right: 8px; /* 8px distance from the right edge */
    }

    .photo-info {
        text-align: center; /* Center-align text within the container */
        padding: 1rem;  /* Padding around the text for spacing */
    }

    .date {
        color: pink;    /* Pink color for the date text */
        font-family: 'Open Sans', sans-serif;
        font-weight: bold;  /* Bold font for emphasis */
        margin: 0.5rem 0;   /* Vertical margin around the date */
    }

    .description {
        color: white;   /* White color for the description text */
        font-family: 'Open Sans', sans-serif;
        margin: 0;  /* Remove default margins for a clean layout */
    }
</style>


<div class="banner">    <!-- Main banner container that will always stay at the top of the viewport -->
    <div class="banner-left">   <!-- Left section contains a love letter icon with a tooltip using the title attribute -->
        <div class="love-letter-container" on:mouseenter={updateTooltip} role="button" tabindex="0"> <!-- The love letter container wraps both the love letter and tooltip -->
            <span class="love-letter">💌</span> <!-- This is the main love letter icon that remains visible -->
            <span class="badge">{badge_count}</span>    <!-- Badge element positioned at the top-right of the love letter -->
            <div class="tooltip">   <!-- The tooltip appears when hovering over the love letter container -->
                <span class="tooltip-text">{@html tooltip_text}</span>  <!-- The right side contains the textual message -->
            </div>
        </div>
    </div>

    <div class="banner-center"> <!-- Center section contains an interactive video element -->
        <video
            disablepictureinpicture
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


<div class="gallery">   <!-- Gallery container with a top margin of 80px to avoid overlap with the fixed banner -->
    {#each photos as photo} <!-- Loop through each photo in the photos array -->
        <div class="photo-card">    <!-- Photo card container for each image and its information -->
            <div class="photo-wrapper"> <!-- Wrapper for the photo used to enable absolute positioning for stickers -->
                <img src={photo.src} alt="College" />   <!-- Display the image using its source from the photo object -->
                {#if photo.leftSticker} <!-- If a left sticker is defined -->
                    <span class="sticker left">{photo.leftSticker}</span>   <!-- Display it in the top-left corner-->
                {/if}

                {#if photo.rightSticker}    <!-- If a right sticker is defined -->
                    <span class="sticker right">{photo.rightSticker}</span> <!-- Display it in the bottom-right corner -->
                {/if}
            </div>

            <div class="photo-info">    <!-- Container for the photo's date and description -->
                <p class="date">{photo.date}</p>    <!-- Display the date in pink text -->
                <p class="description">{photo.description}</p>  <!-- Display the description in white text -->
            </div>
        </div>
    {/each}
</div>