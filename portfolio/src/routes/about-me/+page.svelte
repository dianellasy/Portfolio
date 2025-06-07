<script lang="ts">
    import { goto } from '$app/navigation'; // Import the SvelteKit navigation function to programatically route the user
    import { onMount } from 'svelte';   // Import the onMount function from Svelte to run code after the component has been rendered 

    let width: number = 0;  // Declare a reactive variable width to store the current window width 

    onMount(() => { // The onMount lifecycle runs once the component is attached to the DOM
        width = window.innerWidth;  // Set the width to the current window width

        const updateWidth = () => { // A function to update the width variable whenever the window is resized
            width = window.innerWidth;  // Update the reactive variable width with the new window width
        };

        window.addEventListener('resize', updateWidth); // Add the event listener for the window "resize" event
        return () => window.removeEventListener('resize', updateWidth); // Return a cleanup function that removes the resize event listener when the component is unmounted
    });


    let video_element: HTMLVideoElement | null = null;  // Declare a variable named video_element with an explicit type; the element is HTMLVideoElement or null when not yet bound
    
    const messages = [
        "Thank you for visiting my portfolio! ❤️, Dianella Sy",
        `Two of my favorite songs are "You Oughta Know" by Alanis Morisette and "Sweet Talkin' Woman" by ELO 🎸🎤🎶`,
        "My favorite hobbies include watching true crime shows, walking and riding my road bike on a trail, and spending time with my family and friends 📺🚵🏻‍♀️🫂"
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
</script>


<svelte:head>
    <title>About Me - Dianella Sy's Portfolio</title>
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

    .wrapper {
        /* Overall two-column layout */
        display: flex;  /* Lays out children side by side */
        align-items: flex-start;    /* Aligns items to the top, so the image position can be tweaked */
        gap: 3rem;  /* Horizontal gap between columns */
        padding: 2rem;
    }

    .top-container {
        /* Left column stacks image -> text -> icons */
        width: 400px;   /* Fixed width of 400px so it does not take up the entire screen */
        display: flex;
        flex-direction: column;
        align-items: center;    /* Center them horizontally */
        margin-left: 20px;  /* Shift content to the right */
    }

    .top-container .left-side-image {
        width: 380px;
        margin-top: 80px;  /* Moves the image up a bit */
    }

    .bottom-text-underneath-picture-in-pink {
        /* Text block with pink color */
        margin-top: 1rem;   /* Provides breathing room above the buttom text */
        font-family: 'Open Sans', sans-serif;
        font-size: 30px;    /* Set the font size to 30 pixels */
        text-align: center; /* Center aligns the text within this container */
        color: #efb7ce; /* Pink text */
    }

    .bottom-text-underneath-picture-in-white {
        /* Text block with white color */
        margin-top: -1.4rem;   /* Provides breathing room above the buttom text */
        font-family: 'Open Sans', sans-serif;
        font-size: 20px;    /* Set the font size to 20 pixels */
        text-align: center; /* Center aligns the text within this container */
        color: white; /* White text */
    }

    .social-icons {
        /* Container for all social icons */
        display: inline-flex;  /* Inline flex so it does not take the full width */
        gap: 20px;  /* Space between the icons */
        margin-top: 0.9rem;   /* Space between the text and the icons */
    }

    .social-icons a {
        /* Common styling for icon links */
        display: inline-block;
        transition: transform 0.3s, fill 0.3s;    /* Smooth transition for the lift effect */
    }

    .social-icons a:hover {
        /* Lifts the icon up when hovered */
        transform: translateY(-5px);
    }

    .social-icons svg {
        /* Common SVG styling for icons */
        width: 33px;
        height: 40px;
        fill: white;    /* Default fill is white for clarity on a black background */
        transition: fill 0.3s ease;
    }

    .right-column {
        /* Right column holds text */
        flex: 1;    /* Takes up remaining space */
    }

    .linkedin-icon:hover svg path {
        fill: #efb7ce;  /* Icon turns pink when hovered */
    }

    .github-icon:hover svg path {
        fill: #efb7ce;  /* Icon turns pink when hovered */
    }

    .email-icon:hover svg path {
        fill: #efb7ce;  /* Icon turns pink when hovered */
    }

    .resume-icon:hover svg path {
        fill: #efb7ce;  /* Icon turns pink when hovered */
    }

    .content {
        /* Content container on the right side of the image */
        font-family: 'Open Sans', sans-serif;
        color: white;   /* Sets default text color to white */
    }

    .content h1 {
        /* Define title styles */
        font-size: 42px;    /* Title is 42 px */
        margin-top: 80px;   /* Move the title lower */
        margin-bottom: 10px;    /* Spacing between title abnd paragraph */
    }

    .content p {
        /* Define paragraph text styles */
        font-size: 21px;    /* Text underneath the title is 21px */
        margin: 0;
        line-height: 1.5;   /* Sets the line spacing to 1.5 */

    }

    .pink-word {
        /* Define a class for pink-colored text */
        color: #efb7ce;
        font-weight: bold;
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

        .wrapper {
            margin-top: 80px;   /* Prevent the fixed banner from overlapping the content */
            flex-direction: column;
            align-items: center;    /* Center all items horizontally */
            gap: 1rem;
            padding: 1rem;
        }

        .top-container {
            width: 100%;
            margin-left: 0; /* Remove any left offset */
            align-items: center;    /* Center its children */
            text-align: center; /* Center any text inside */
        }

        .top-container, .left-side-image {
            width: 100%;
            height: auto;   /* Maintain aspect ratio */
        }

        .bottom-text-underneath-picture-in-pink,
        .bottom-text-underneath-picture-in-white {
            width: 100%;
            text-align: center;
        }

        .social-icons {
            align-items: center;
        }

        .right-column,
        .content h1,
        .content p {
            width: 100%;
            text-align: center;
            align-items: center;
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


<div class="wrapper">
    <div class="top-container">
        <!-- Top container holds the image on the left and the content on the right -->
        <img class="left-side-image" src="/about-me/left-side-image.jpg" alt="Left Side" />
        <p class="bottom-text-underneath-picture-in-pink">
            <strong>Dianella Sy<br>
            (she/her)</strong>
        </p>

        <p class="bottom-text-underneath-picture-in-white">
            Aspiring Software Developer
        </p>

        <div class="social-icons">
            <!-- LinkedIn icon underneath the white text -->
            <a
                class="linkedin-icon"
                href="https://www.linkedin.com/in/dianellasy"
                target="_blank"
                rel="noopener noreferrer"
            >
                <svg
                    role="img"
                    viewBox="0 0 448 512"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <title>LinkedIn</title>
                    <path d="M100.28 448H7.4V148.9h92.88zm-46.44-295.2a53.79 53.79 0 1 1
                        53.79-53.79 53.79 53.79 0 0 1-53.79 53.79zm394.56 295.2h-92.68V302.4c0-34.7-12.43-58.4-43.55-58.4-23.74
                        0-37.87 16.02-44.12 31.49-2.27 5.59-2.82 13.41-2.82 21.28V448H171.09v-260h92.68v36.88c12.33-19
                        34.38-46.16 83.55-46.16 61 0 106.67 39.92 106.67 125.59v153.69z"/>
                </svg>
            </a>

            <!-- GitHub icon underneath the white text-->
            <a
                class="github-icon"
                href="https://github.com/dianellasy"
                target="_blank"
                rel="noopener noreferrer"
            >
                <svg
                    role="img"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <title>GitHub</title>
                    <!-- Typical GitHub SVG path icon -->
                    <path d="M12 .5C5.7.5.5 5.7.5 12c0 5.1 3.3 9.4 7.9 10.9.6.1.8-.3.8-.6v-2.3c-3.2.7-3.9-1.5-3.9-1.5-.5-1.3-1.2-1.7-1.2-1.7-1-.7.1-.7.1-.7
                        1.1.1 1.7 1.1 1.7 1.1 1 1.7 2.6 1.2 3.2.9.1-.7.4-1.2.7-1.5-2.6-.3-5.3-1.3-5.3-5.8 0-1.3.5-2.4 1.2-3.3-.1-.3-.5-1.4.1-2.9
                        0 0 1-.3 3.2 1.2 1-.3 2-.4 3-.4s2 .1 3 .4c2.2-1.6 3.2-1.2 3.2-1.2.6 1.5.2 2.6.1 2.9.8.9 1.2 2 1.2 3.3 0 4.5-2.7 5.5-5.3 5.8.4.3.8 1 .8 2v3c0 .3.2.8.8.6
                        4.6-1.5 7.9-5.8 7.9-10.9C23.5 5.7 18.3.5 12 .5z"/>
                </svg>
            </a>

            <!-- Email icon underneath the white text -->
            <a
                class="email-icon"
                href="mailto:dianellabsy@csu.fullerton.edu"
            >
                <svg
                    role="img"
                    viewBox="0 0 512 512"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <title>Email</title>
                    <!--Envelope icon path -->
                    <path d="M48 64C21.5 64 0 85.5 0 112c0 15.1 7.1 29.3 19.2 38.4L236.8 313.6c11.4 8.5 27 8.5 38.4 0L492.8 150.4c12.1-9.1 19.2-23.3 19.2-38.4c0-26.5-21.5-48-48-48L48 64zM0 176L0 384c0 35.3 28.7 64 64 64l384 0c35.3 0 64-28.7 64-64l0-208L294.4 339.2c-22.8 17.1-54 17.1-76.8 0L0 176z"/>
                </svg>
            </a>

            <a
                class="resume-icon"
                href="/about-me/resume.pdf"
                target="_blank"
                rel="noopener noreferrer"
            >
                <svg
                    role="img"
                    viewBox="0 0 384 512"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <title>Resume</title>
                    <!-- This is a file/document icon (similar to Font Awesome's file-alt icon) -->
                    <path d="M0 64C0 28.7 28.7 0 64 0L224 0l0 128c0 17.7 14.3 32 32 32l128 0 0 288c0 35.3-28.7 64-64 64L64 512c-35.3 0-64-28.7-64-64L0 64zm384 64l-128 0L256 0 384 128z"/>
                </svg>
            </a>
        </div>
    </div>

    <div class="right-column">
        <div class="content">
            <h1>Hello World!</h1>
            <p>
                My name is <span class="pink-word">Dianella Sy</span>, and I am a third-year
                undergraduate student majoring in <span class="pink-word">Computer Science </span>
                at <span class="pink-word">California State University, Fullerton (CSUF)</span>.<br><br>

                Before my dad retired, he was a Computer and Network Technician at the school district where 
                I attended elementary school, so from a young age, I was exposed to computers. I was introduced 
                to computer science in <span class="pink-word">fifth grade</span> and took coding lessons through 
                <span class="pink-word">Code.org’s Minecraft Hour of Code Tutorials</span> and created my own 
                <span class="pink-word">Flappy Bird Game</span>. Because of my long-term interest in computer 
                science, in my junior year of high school, I took <span class="pink-word">AP Computer Science 
                Principles</span>, an introductory college-level course, where I learned algorithms, programming, 
                computer systems, networks, and data analysis. I was interested in learning more about computer 
                science, so after taking the course and passing the AP exam, I chose to major in Computer Science 
                at CSUF, where my older brother also attended college.<br><br>
                
                During my second year at CSUF, I was the <span class="pink-word">Treasurer</span> for
                the chapter club, <span class="pink-word">Association for Computing Machinery-Women</span>, where I
                managed all financial affairs and budgeting, as well as maintained the agency accounts for the organization.
                I also encouraged and supported 15 women pursuing a computer science major and hosted 15+ technical 
                workshops. In addition to being Treasurer, in the spring semester, I attended my first hackathon, 
                <span class="pink-word">FullyHacks 2025</span>, where I won <span class="pink-word">Best Game Project</span>.<br><br> 

                This summer, I am participating in the <span class="pink-word">2025 CIC Summer Research Program</span> at CSUF. During this seven-week 
                research experience, I am exploring <span class="pink-word">Pairs Trading</span> by engaging in structured virtual lectures, 
                working on a research project, collaborating with faculty and peers, and gaining valuable experience applying computer science 
                concepts to real-world problems. In addition, I was also <span class="pink-word">1</span> out of the <span class="pink-word">50</span>, 
                from an applicant pool of nearly <span class="pink-word">900</span>, selected to attend the <span class="pink-word">CSU AI Summer Camp 2025</span>
                at Cal Poly San Luis Obispo, sponsored by <span class="pink-word">Amazon Web Services (AWS)</span>. I will be working with a team to solve pressing 
                challenges and opportunities in the CSU system, applying AI technologies through hands-on workshops and mentored projects, and pitching my team’s 
                ideas and prototypes to my peers and mentors in a 5-day <span class="pink-word">applied AI hackathon</span>.<br><br>

                For the upcoming year as a third-year student, I will be a <span class="pink-word">Computer Science Supplemental Instruction Leader</span>, where I 
                facilitate two group sessions weekly where students meet to improve their understanding of the course materials in a computer science class. I will
                also be the <span class="pink-word">Webmaster</span> and <span class="pink-word">Open Source Co-Team Lead</span> for the CSUF chapter club, 
                <span class="pink-word">Association for Computing Machinery</span>. As Webmaster, I will maintain the Association for Computing Machinery CSUF’s website, 
                <span class="pink-word">acmcsuf.com</span>, the largest open-source project for the chapter club, and update it with new information. I will also guide 
                students with issues listed on <span class="pink-word">GitHub</span> and mentor how to solve the issue, providing hands-on experience in contributing to 
                open-source projects. As Open Source Co-Team Lead, I will present and organize weekly technical workshops for students, such as instructing them to make a 
                first contribution to the acmcsufoss organization, hands-on coding, and real-world open source projects.<br><br>

                After I graduate, I plan to pursue a <span class="pink-word">master's degree</span> and a <span class="pink-word">PhD</span> while working as a software engineer. 
                I am excited and looking forward to working in the same field as my dad, applying all of the topics I learned in fifth grade through Code.org, AP Computer Science Principles, 
                and my college courses to the real world, expanding my technical skills, and gaining hands-on experience.
            </p>
        </div>
    </div>
</div>