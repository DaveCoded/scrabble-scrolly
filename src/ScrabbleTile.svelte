<script>
    import { gsap } from 'gsap'
    import { ScrollTrigger } from 'gsap/ScrollTrigger'

    import { onMount } from 'svelte'

    gsap.registerPlugin(ScrollTrigger)

    // Variables for binding DOM elements
    let section
    let bigLetter
    let definitionRef
    let scoreRef
    let dictionaryRef

    // Props to expose to parent
    export let heading
    export let definition
    export let score
    export let dictionary

    const fadeUpAnimation = {
        opacity: 0,
        y: 30,
        duration: 1
    }

    onMount(() => {
        const timeline = gsap.timeline();
        timeline.to(bigLetter, {
            scale: 2,
            duration: 2
        })
        .from(definitionRef, fadeUpAnimation)
        .from(scoreRef, fadeUpAnimation)
        .from(dictionaryRef, fadeUpAnimation)

        ScrollTrigger.create({
            trigger: section,
            animation: timeline,
            markers: true,
            scrub: 1,
            pin: true
        })
    })
</script>

<style>
    .section {
        height: 100vh;
        display: flex;
        border: 1px solid rgb(168, 168, 168);
    }

    .column {
        width: 50%;
        padding: 5em;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .two-letter {
        font-size: 18em;
    }
</style>

<section
    id={heading}
    class="section"
    bind:this={section}
>
    <div class="column">
        <h2 class="two-letter" bind:this={bigLetter}>{heading}</h2>
    </div>
    <div class="column">
        <p class="definition" bind:this={definitionRef}>{definition}</p>
        <p class="score" bind:this={scoreRef}>{score}</p>
        <p class="dictionary" bind:this={dictionaryRef}>{dictionary}</p>
    </div>
</section>