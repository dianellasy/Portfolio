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
    </div>
</div>