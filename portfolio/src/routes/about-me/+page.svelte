<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=Open+Sans&display=swap"
        rel="stylesheet"
    >
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
        margin-top: 30px;  /* Moves the image up a bit */
        margin-right: 400px; /* Space between the image and the text */
    }

    .content {
        /* Content container on the right side of the image */
        flex: 1;    /* Takes up the remaining space */
        font-family: 'Open Sans', sans-serif;
    }

    .bottom-text {
        margin-top: 40px;   /* Provides breathing room above the buttom text */
        margin-left: -940px;  /* Moves the entire bottom-text container -940px to the right */
        font-family: 'Open Sans', sans-serif;
        font-size: 30px;    /* Set the font size to 30 pixels */
        text-align: center; /* Center aligns the text within this container */
        color: #efb7ce;
    }
</style>


<div class="wrapper">
     <div class="top-container">
        <!-- Top container holds the image on the left and the content on the right -->
        <img class="left-side-image" src="/about-me/left-side-image.jpg" alt="Left Side" />
        <div class="content">
            <h1>Hello World!</h1>
        </div>
     </div>


    <div class="bottom-text">
        <!-- Bottom text holds the text that appears below the top container -->
        <p>
            Dianella Sy<br>
            (she/her)
        </p>
    </div>
</div>