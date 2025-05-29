<script>
    import { text } from "@sveltejs/kit";

    // Project data for six cards
    const projects = [
        {
            name: "Country Life Cafe",
            image: "/projects/country_life_cafe.png",
            text: `𐙚 Programmed a video game using Unity and C# to promote the idea of sustainable farming
                   𐙚 Produced ingredients on the farm and built the order in the half kitchen and half window scene in a specific amount of time for three days
                   𐙚 Obtained tokens if the order is successfully served, and the user wins if a certain number of tokens is reached`,
            icons: [
                { iconClass: "fab fa-github", link: "https://github.com/emilyytsai/CountryLifeCafe" }
            ]
        },

        {
            name: "Out of this World Cafe",
            image: "/projects/out_of_this_world_cafe.png",
            text: `𐙚 Developed during the 24-hour hackathon, FullyHacks 2025, with 250+ participants, and won Best Game Project 
                   𐙚 Implemented a restaurant tycoon video game utilizing C# and Unity, where a group of animals have been stranded in space for a period of time
                   𐙚 Served the animals ice cream, and if they are satisfied, they will go home with the cafe owner back to Earth`,
            icons: [
                { iconClass: "fab fa-github", link: "https://github.com/emilyytsai/OutOfThisWorldCafe" }
            ]
        },

        {
            name: "Association for Computing Machinery CSUF Website (acmcsuf.com)",
            image: "/projects/acm_design_portfolio.png",
            text: `𐙚 Contribute to the Association for Computing Machinery CSUF’s website, the largest open-source project for the chapter club, by fixing issues listed on GitHub and creating pull requests
                   𐙚 Redesign a page that showcases portfolios utilizing Figma, JSON, and Svelte`,
            icons: [
                { iconClass: "fab fa-github", link: "https://github.com/EthanThatOneKid/acmcsuf.com/pull/1178" }
            ]
        },

        {
            name: "Book Store (Doubly Linked List Adapter)",
            text: `𐙚 Implemented a custom doubly linked list class and a wrapper class, an adapter, in C++ that enables user code to interact directly with a simulation of a bookstore
                   𐙚 Maintained a list of books, sells books to a customer, and allows the user to add new books and view a list of all books in the inventory`,
        },

        {
            name: "Food Wastage Tracker",
            text: `𐙚 Built a final Object-Oriented Programming course project, a web-based application utilizing C++, that empowers individuals to track, manage, and minimize their food waste`,
        },

        {
            name: "AP Computer Science Principles Create Performance Task",
            text: `𐙚 Utilized JavaScript to implement a web-based application that prompts the user with a few questions and then devises custom recommendations for their summer activities
                   𐙚 Personalized users’ interests to present a concrete, comprehensive list of activities to do in the summer`,
        }
    ];
</script>

<style>
    .title-container {
        /* Container for the title to center its content */
        text-align: center; /* Centers inline or inline-block children */
    }

    .projects-title {
        /* Style for the projects title at the top */
        font-size: 2.5rem;  /* Font size */
        font-weight: bold;  /* Bold font for impact */
        margin: 1.5rem auto;   /* Automatic horizontal margins center the element */
        background: linear-gradient(1550deg, yellow, hotpink);    /* Gradient background from hotpink to yellow */
        background-clip: text; /* Clip the background to the text (standard) */
        -webkit-background-clip: text;  /* Clip the background to the text for WebKit browsers */
        color: transparent; /* Transparent text color so that the gradient shows */
        -webkit-text-fill-color: transparent;   /* Make text fill transparent to reveal the gradient */
        display: inline-block;  /* Helps ensure proper clipping in some browsers */
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
        animation: borderAnim 6s linear infinite;    /* Animate the gradient for movement */
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
        margin-bottom: 1rem;    /* Spacing below the project name */
    }

    .project-image {
        /* Style for the project image */
        width: 100%;    /* The image spans the full width of the card */
        display: block; /* Display as a block-level element */
        border-radius: 8px; /* Rounded corners for the image */
        margin-bottom: 1rem;    /* Spacing between the image and text */
        object-fit: cover;  /* Ensure the image covers the area without distortion */
    }

    .project-text {
        /* Style for the multi-line project text */
        color: #ccc;    /* Light gray color for the descriptive text */
        font-size: 1rem;    /* Standard font size for text */
        margin-bottom: 1rem;    /* Spacing below the text block */
        text-align: center; /* Center the text */
        white-space: pre-wrap;  /* Preserve whitespace and line breaks from the template literal */
    }

    .project-icons {
        /* Container styling for the project icons */
        display: flex;  /* Use Flexbox for layout of icons */
        justify-content: center;    /* Center the icons horizontally */
        gap: 1rem;  /* Set even spacing between each icon */
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
</style>


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

            <div class="project-text">{project.text}</div>  <!-- Display the project text with multi-line support -->

            {#if project.icons && project.icons.length} <!-- Conditionally render project icons if they exist and have items -->
                <div class="project-icons">
                    {#each project.icons as icon}   <!-- Loop through each icon in the project's icons array -->
                        <a href={icon.link} target="_blank" rel="noopener noreferrer">  <!-- Each icon is wrapped in a link that opens in a new tab -->
                            <i class={icon.iconClass}></i>  <!-- Render the icon using the iconClass-->
                        </a>
                    {/each}
                </div>
            {/if}
        </div>
    {/each}
</div>