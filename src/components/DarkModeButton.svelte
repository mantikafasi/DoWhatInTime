<!--Thank https://github.com/Vendicated/ for code-->
<script lang="ts">

    function onClick(e: MouseEvent) {
        
        const newTheme = document.documentElement.classList.toggle("dark") ? "dark" : "light";
        localStorage.setItem("theme", newTheme);
        console.log("Switched theme to", newTheme);

        // do not blur if this press was keyboard triggered
        if (e instanceof PointerEvent && e.pointerType)
            (e.target as HTMLElement).blur();
    }
</script>
<svelte:head>
    <script>
		if (document) {
            let theme = localStorage.getItem("theme") || "system";
            if ((theme === "system" && window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) || theme === "dark") {
                document.documentElement.classList.add('dark');
            } 
    	}
	</script>
</svelte:head>

<button on:click={onClick} aria-label="toggle dark theme" tabindex="0" />

<style>
    button {
        all: unset;

        cursor: pointer;
        margin-left: 1em;
        width: 1.2em;
        height: 1.2em;
        background-image: url(/assets/sun.svg);
        background-repeat: no-repeat;
        background-size: cover;
        filter: var(--invert-svg);

        transition: transform 0.12s linear;
    }


    button:hover,
    button:focus {
        transform: scale(1.2) rotate(-5deg);
        outline: none;
    }

    button:focus:not(:hover)::after {
        position: absolute;
        content: "";
        height: 1px;
        bottom: -4px;
        width: 100%;
        background: var(--color);
        transform: scale(1.2) rotate(5deg);
    }
</style>
