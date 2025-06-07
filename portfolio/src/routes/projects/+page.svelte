<script lang="ts">
    import { text } from "@sveltejs/kit";
    import { goto } from '$app/navigation'; // Import the SvelteKit navigation function to programatically route the user

    let video_element: HTMLVideoElement | null = null;  // Declare a variable named video_element with an explicit type; the element is HTMLVideoElement or null when not yet bound
    
    const messages = [
        "Thank you for visiting my portfolio! ❤️, Dianella Sy",
        '"If you chase your dreams, you can catch them" - Tadej Pogačar 👩🏻‍💻',
        '"Every single day, do something that makes your heart sing" - Marcia Wieder 🥰',
        `"Become the person you were meant to be, light your inner fire, and follow your heart's desire" - Leon Brown ❤️‍🔥`
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

    // Project data for six cards
    const projects = [
        {
            name: "Country Life Cafe",
            image: "/projects/country_life_cafe.png",
            text: `♡ Programmed a video game using C# and Unity to promote the idea of sustainable farming

♡ Produced ingredients on the farm and built the order in the half kitchen and half window scene in a specific amount of time for three days

♡ Obtained tokens if the order is successfully served, and the user wins if a certain number of tokens is reached`,
            technologies: ["C#", "Unity"],
            icons: [
                { type: "font", iconClass: "fab fa-github", link: "https://github.com/emilyytsai/CountryLifeCafe" },
                { type: "font", iconClass: "fab fa-slideshare", link: "https://www.canva.com/design/DAGmOZJheP0/E6IFtfqVpwVTka625psaVQ/view?utm_content=DAGmOZJheP0&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h5f121b982c#1" },
                { type: "font", iconClass: "fab fa-youtube", link: "https://youtu.be/Vb7xCwOkYAs?si=vch39ADE-2U_ct7m" }
            ]
        },

        {
            name: "Out of this World Cafe",
            image: "/projects/out_of_this_world_cafe.png",
            text: `♡ Developed during the 24-hour hackathon, FullyHacks 2025, with 250+ participants, and won Best Game Project 
            
♡ Implemented a restaurant tycoon video game utilizing C# and Unity, where a group of animals have been stranded in space for a period of time

♡ Served the animals ice cream, and if they are satisfied, they will go home with the cafe owner back to Earth`,
            technologies: ["C#", "Unity", "24-Hour Hackathon", "Best Game Project", "250+ Participants"],
            icons: [
                { type: "font", iconClass: "fab fa-github", link: "https://github.com/emilyytsai/OutOfThisWorldCafe" },
                { type: "font", iconClass: "fab fa-youtube", link: "https://youtu.be/ShiuO1t1tdo?si=QX4cMG3phMMwj-W_" },
                { type: "image", src: "/projects/devpost.png", link: "https://devpost.com/software/out-of-this-world-cafe?_gl=1*vopaxd*_gcl_au*NjQ1NTc5NTYzLjE3NDEzMDkyODk.*_ga*NDgxOTI4NjA2LjE3NDEzMDkyODk.*_ga_0YHJK3Y10M*czE3NDg0OTMxMjQkbzIzJGcxJHQxNzQ4NDkzMTI3JGo1NyRsMCRoMA.." }
            ]
        },

        {
            name: "Association for Computing Machinery CSUF Website (acmcsuf.com)",
            image: "/projects/acm_design_portfolio.png",
            text: `♡ Contribute to the Association for Computing Machinery CSUF’s website, the largest open-source project for the chapter club, by fixing issues listed on GitHub and creating pull requests

♡ Redesign a page that showcases portfolios utilizing Figma, JSON, and Svelte`,
            technologies: ["Figma", "JSON", "Svelte"],
            icons: [
                { type: "font", iconClass: "fab fa-github", link: "https://github.com/EthanThatOneKid/acmcsuf.com/pull/1178" },
                { type: "font", iconClass: "fas fa-globe", link: "https://acmcsuf.com/portfolios" }
            ]
        },

        {
            name: "Book Store (Doubly Linked List Adapter)",
            text: `♡ Implemented a custom doubly linked list class and a wrapper class, an adapter, in C++ that enables user code to interact directly with a simulation of a bookstore

♡ Maintained a list of books, sells books to a customer, and allows the user to add new books and view a list of all books in the inventory`,
            technologies: ["C++", "Data Structures"],
        },

        {
            name: "Food Wastage Tracker",
            text: `♡ Built a final Object-Oriented Programming course project, a web-based application utilizing C++, that empowers individuals to track, manage, and minimize their food waste`,
            technologies: ["C++", "Object-Oriented Programming"],
        },

        {
            name: "AP Computer Science Principles Create Performance Task",
            text: `♡ Utilized JavaScript to implement a web-based application that prompts the user with a few questions and then devises custom recommendations for their summer activities

♡ Personalized users’ interests to present a concrete, comprehensive list of activities to do in the summer`,
            technologies: ["JavaScript"],
        }
    ];
</script>


<svelte:head>
    <title>Projects - Dianella Sy's Portfolio</title>
    <link
        href="https://fonts.googleapis.com/css2?family=Open+Sans&display=swap"
        rel="stylesheet"
    />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
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

    .love-letter-badge {
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

    .title-container {
        /* Container for the title to center its content */
        text-align: center; /* Centers inline or inline-block children */
    }

    .projects-title {
        /* Style for the projects title at the top */
        font-size: 2.5rem;  /* Font size */
        font-weight: bold;  /* Bold font for impact */
        text-align: center; /* Center the title */
        margin: 1.5rem 0;   /* Vertical margins for spacing */
        background: linear-gradient(45deg, hotpink, yellow);    /* Gradient background from hotpink to yellow */
        -webkit-background-clip: text;  /* Clip the background to the text for WebKit browsers */
        -webkit-text-fill-color: transparent;   /* Make text fill transparent to reveal the gradient */
        background-clip: text;  /* Standard text clipping */
        color: transparent; /* Transparent text color so that the gradient shows */
        font-family: 'Open Sans', sans-serif;
    }

    .container {
        /* Container defines a grid layout for the project cards with three equal columns */
        display: grid;  /* Apply CSS Grid layout */
        grid-template-columns: repeat(3, 1fr);  /* Create 3 columns of equal width */
        gap: 1.5rem;    /* Set space between the grid items */
        max-width: 1200px;  /* Maximum width of the container */
        margin: 2rem auto;  /* Center the container and add vertical spacing */
        padding: 0 1rem;    /* Horizontal padding for the container */
    }

    .card {
        /* Each project card styling */
        position: relative; /* Required for positioning pseudo-elements */
        background: #111;   /* Dark background to enhance neon effects */
        border-radius: 12px;    /* Rounded corners for the card */
        overflow: hidden;   /* Hide any overflowing content */
        padding: 1rem;  /* Internal spacing inside the card */
        z-index: 1; /* Ensure the card content sits above the neon border */
        transition: transform 0.3s ease, box-shadow 0.3s ease;  /* Smooth transition on hover */
    }

    .card:hover {
        /* Hover effect for the card to raise it with a slight scale and shadow */
        transform: translateY(-10px) scale(1.02);   /* Moves the card up (-10px) and scales it up slightly */
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5); /* Adds a shadow to enhance the 3D lifted effect */
    }

    .card::before {
        /* Create a neon border effect using the ::before pseudo-element */
        content: "";    /* Empty content to display the pseudo-element */
        position: absolute; /* Position absolutely relative to the .card */
        top: -3px;  /* Extend above the card edge */
        left: -3px; /* Extend to the left of the card edge */
        right: -3px;    /* Extend beyond the right border */
        bottom: -3px;   /* Extend beyond the bottom border */
        background: linear-gradient(45deg,  
            yellow 0%,         /* Start with yellow from the beginning... */
            hotpink 49%,        /* ...continue yellow until 49% of the gradient length */
            yellow 49%,       /* At 49%, start the pink stripe */
            hotpink 51%,       /* End the pink stripe at 51% */
            hotpink 51%,        /* Resume yellow from 51% onwards */
            yellow 100%);        /* Continue yellow until the gradient ends */

        background-size: 200% 200%; /* Create a large background for animation */
        z-index: -2;    /* Place the gradient behind the card */
        filter: blur(8px);  /* Blur the gradient to simulate a glow */
        animation: borderAnim 5s linear infinite;    /* Animate the gradient for movement */
        border-radius: inherit; /* Inherit the border radius from the .card */
    }

    .card::after {
        /* Create an inset layer using the ::after pseudo-element to overlay the card content */
        content: "";    /* Empty content for the overlay */
        position: absolute; /* Position absolutely to cover the entire card */
        top: 0; /* Align with the top */
        left: 0;    /* Align with the left */
        right: 0;   /* Align with the right */
        bottom: 0;  /* Align with the bottom */
        background: #111;   /* Same as the card background to mask the neon glow */
        z-index: -1;    /* Layer this above ::before but below the content */
        border-radius: inherit; /*Keep the same rounded corners */
        margin: 3px;    /* Create spacing that reveals the neon border */
    }

    /* Define keyframes for the neon gradient animation */
    @keyframes borderAnim {
        0% {
            background-position: 0% 50%;    /* Start at initial background position */
        }

        50% {
            background-position: 100% 50%;  /* Move to the opposite end at midpoint */
        }

        100% {
            background-position: 0% 50%;    /* Return to initial position */
        }
    }

    .project-name {
        /* Style for the project name */
        font-size: 1.5rem;  /* Increase font size */
        font-weight: bold;  /* Bold text */
        color: #fff;    /* White color for readability against dark background */
        text-align: center; /* Center the project name */
        margin: 0.5rem 0 1rem 0; /* Consistent margins (top 0.5rem, bottom: 1rem, left/right: 0) */
        line-height: 1.2;   /* A slighly tighter line-height for short titles */
        font-family: 'Open Sans', sans-serif;
    }

    .project-image {
        /* Style for the project image */
        width: 100%;    /* The image spans the full width of the card */
        display: block; /* Display as a block-level element */
        border-radius: 8px; /* Rounded corners for the image */
        margin-bottom: 1rem;    /* Spacing between the image and text */
        object-fit: cover;  /* Ensure the image covers the area without distortion */
    }

    .technology-badges {
        /* Technology badges container */
        display: flex;  /* Use Flexbox for layout */
        justify-content: center;    /* Center badges horizontally */
        gap: 0.5rem;    /* Space between badges */
        margin-bottom: 1rem;    /* Space below the badges section */
        flex-wrap: wrap;
    }

    .badge {
        /* Styles for individual badges */
        /*background: linear-gradient(20deg, #efb7ce, #BA8E23); */
        background: linear-gradient(30deg,#BA8E23, hotpink);
        color: #fff;    /* White text */
        font-size: 0.8rem;  /* Smaller font size for badges */
        padding: 0.3rem 0.6rem; /* Padding to create the rectangle shape */
        border-radius: 4px; /* Slightly rounded corners */
        font-family: 'Open Sans', sans-serif;
        text-align: center;
    }

    .project-text {
        /* Style for the multi-line project text */
        color: #ccc;    /* Light gray color for the descriptive text */
        font-size: 1rem;    /* Standard font size for text */
        margin: 1rem 0;    /* Consistent top and bottom margins */
        line-height: 1.5;   /* Uniform line-height for readability */
        text-align: center; /* Center the text */
        white-space: pre-wrap;  /* Preserve whitespace and line breaks from the template literal */
        font-family: 'Open Sans', sans-serif;
    }

    .project-icons {
        /* Container styling for the project icons */
        display: flex;  /* Use Flexbox for layout of icons */
        justify-content: center;    /* Center the icons horizontally */
        gap: 1rem;  /* Set even spacing between each icon */
        margin-top: 0.5rem; /* Adds some breathing room above icons */
    }

    .project-icons a {
        /* Style for each icon link */
        color: #fff;    /* White icon color by default */
        font-size: 1.5rem;  /* Increase icon size for visibility */
        transition: color 0.3s; /* Smooth color change when hovered */
    }

    .project-icons a:hover {
        /* Hover effect for the icon links */
        color: #efb7ce; /* Change icon color to light pink when hovered */
    }

    /* Responsive tweaks for smaller screens */
    @media screen and (max-width: 600px) {
        .banner {
            flex-direction: column;
            padding: 0.5rem;
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


        .love-letter-container {
            display: none;
        }

        .container {
            margin-top: 90px;
            grid-template-columns: 1fr; /* Single column layout for small screens */
        }

        .badge {
            font-size: 0.7rem;  /* Reduce font size on mobile */
            padding: 0.2rem 0.4rem; /* Reduce padding on mobile */
        }
    }

    @media only screen and (min-width: 600px) and (max-width: 992px) {
        .banner-center video {
            display: none;
        }

        .love-letter-container {
            display: none;
        }
    }

    @media only screen and (min-width: 992px) and (max-width: 1280px) {
        .love-letter-container {
            display: none;
        }
    }
</style>


<div class="banner">    <!-- Main banner container that will always stay at the top of the viewport -->
    <div class="banner-left">   <!-- Left section contains a love letter icon with a tooltip using the title attribute -->
        <div class="love-letter-container" on:mouseenter={updateTooltip} role="button" tabindex="0"> <!-- The love letter container wraps both the love letter and tooltip -->
            <span class="love-letter">💌</span> <!-- This is the main love letter icon that remains visible -->
            <span class="love-letter-badge">{badge_count}</span>    <!-- Badge element positioned at the top-right of the love letter -->
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


<div class="title-container">   <!-- Wrap the title in a container that centers its content -->
    <h1 class="projects-title">Projects</h1>    <!-- Title for the projects section with a yellow to pink gradient -->
</div>


<div class="container"> <!-- Main container div holding all project cards -->
    {#each projects as project (project.name)}  <!-- Loop through each project in the projects array -->
        <div class="card">  <!-- Start of individual project card -->
            <div class="project-name">{project.name}</div>  <!-- Display the project name -->

            {#if project.image} <!-- Conditionally render the project image if it exists -->
                <img
                    class="project-image"
                    src={project.image}
                    alt="{project.name}"
                />
            {/if}

            {#if project.technologies}  <!-- Check if project.technologies exists -->
                <div class="technology-badges">
                    {#each project.technologies as tech}    <!-- Loop over each technology -->
                        <span class="badge">{tech}</span>   <!-- Render as a badge -->
                    {/each}
                </div>
            {/if}

            <div class="project-text">{project.text}</div>  <!-- Display the project text with multi-line support -->

            {#if project.icons && project.icons.length} <!-- Conditionally render project icons if they exist and have items -->
                <div class="project-icons">
                    {#each project.icons as icon}   <!-- Loop through each icon in the project's icons array -->
                        <a href={icon.link} target="_blank" rel="noopener noreferrer">  <!-- Each icon is wrapped in a link that opens in a new tab -->
                            {#if icon.type === 'image'}
                                <img src={icon.src} alt="Devpost Icon" style="width: 1.5rem; height: 1.5rem;" />
                            {:else}
                                <i class={icon.iconClass}></i>  <!-- Render the icon using the iconClass-->
                            {/if}
                        </a>
                    {/each}
                </div>
            {/if}
        </div>
    {/each}
</div>