<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=Open+Sans&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<style>
    .wrapper {
        /* Wrapper for the entire page content */
        padding: 20px;
    }

    .top-container {
        /* Top container holds the image and the adjacent content in a flex row */
        display: flex;  /* Lays out children side by side */
        align-items: flex-start;    /* Aligns items to the top, so the image position can be tweaked */
    }

    .left-side-image {
        /* Image that will appear on the left side */
        width: 380px;   /* Set a fixed width of 380px */
        margin-left: 250px;  /* Shifts the image a little to the right */
        margin-top: 50px;  /* Moves the image up a bit */
        margin-right: 200px; /* Space between the image and the text */
    }

    .bottom-text-underneath-picture-in-pink {
        /* Text block with pink color */
        margin-top: 30px;   /* Provides breathing room above the buttom text */
        margin-left: -940px;  /* Moves the entire bottom-text container -940px to the right */
        font-family: 'Open Sans', sans-serif;
        font-size: 30px;    /* Set the font size to 30 pixels */
        text-align: center; /* Center aligns the text within this container */
        color: #efb7ce; /* Pink text */
    }

    .bottom-text-underneath-picture-in-white {
        /* Text block with white color */
        margin-top: -20px;   /* Provides breathing room above the buttom text */
        margin-left: -940px;  /* Moves the entire bottom-text container -940px to the right */
        font-family: 'Open Sans', sans-serif;
        font-size: 20px;    /* Set the font size to 20 pixels */
        text-align: center; /* Center aligns the text within this container */
        color: white; /* White text */
    }

    .social-icons {
        display: inline-flex;  /* Inline flex so it does not take the full width */
        gap: 20px;  /* Space between the icons */
        margin-top: 10px;   /* Space between the text and the icons */
    }

    .linkedin-icon,
    .github-icon {
        /* Common styling for both icon links */
        display: inline-block;
        cursor: pointer;
    }

    .linkedin-icon svg,
    .github-icon svg {
        /* Common SVG styling for icons */
        width: 33px;
        height: 40px;
        fill: white;    /* Default fill is white for clarity on a black background */
        transition: fill 0.3s ease;
    }

    .linkedin-icon:hover svg path {
        fill: #efb7ce;  /* Icon turns pink when hovered */
    }

    .github-icon:hover svg path {
        fill: #efb7ce;  /* Icon turns pink when hovered */
    }

    .content {
        /* Content container on the right side of the image */
        flex: 1;    /* Takes up the remaining space */
        font-family: 'Open Sans', sans-serif;
        color: white;   /* Sets default text color to white */
    }

    .content h1 {
        /* Define title styles */
        font-size: 42px;    /* Title is 42 px */
        margin-top: 60px;   /* Move the title lower */
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
</style>


<div class="wrapper">
     <div class="top-container">
        <!-- Top container holds the image on the left and the content on the right -->
        <img class="left-side-image" src="/about-me/left-side-image.jpg" alt="Left Side" />
        <div class="content">
            <h1>Hello World!</h1>
            <p>
                My name is <span class="pink-word">Dianella Sy</span>, and I am a third-year
                undergraduate student majoring in <span class="pink-word">Computer Science </span>
                at <span class="pink-word">California State University, Fullerton (CSUF)</span>.<br><br>
                
                During my second year at CSUF, I was the <span class="pink-word">Treasurer</span> for
                the chapter club, <span class="pink-word">Association for Computing Machinery-Women</span>. 
                I also attended my first hackathon, <span class="pink-word">FullyHacks 2025</span>, where I 
                won <span class="pink-word">Best Game Project</span>.<br><br> 

                For the upcoming year as a third-year student, I will be a <span class="pink-word">Computer 
                Science Supplemental Instruction Leader</span> and the <span class="pink-word">Webmaster</span>
                and <span class="pink-word">Open Source Co-Team Lead</span> for the CSUF chapter club, 
                <span class="pink-word">Association for Computing Machinery</span>.<br><br>

                After I graduate, I plan to pursue a <span class="pink-word">master's degree</span> and a
                <span class="pink-word">PhD</span> while working as a software engineer. I am excited and looking
                forward to applying all of the topics I learned in my courses to the real world, expanding my
                technical skills, and gaining hands-on experience.
            </p>
        </div>
     </div>


    <div class="bottom-text-underneath-picture-in-pink">
        <!-- Holds the pink text that appears below the top container -->
        <p>
            <strong>Dianella Sy<br>
            (she/her)</strong>
        </p>
    </div>

    <div class="bottom-text-underneath-picture-in-white">
        <!-- Holds the white text that appears below the top container -->
        <p>
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
        </div>
    </div>
</div>