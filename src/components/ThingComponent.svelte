<script lang="ts">
    export let givenTime = 12345;
    export let name = "Farting";
    export let description = "Farting is a great thing to do";
    export let image = "";
    export let time = 123;
    export let time_max = -1;
    export let type = "number";
    export let string = "?";

    $: console.log(time, time_max, givenTime);

    $: thingDoCount = Math.floor(givenTime / time);
    $: thingDoMaxCount = Math.floor(givenTime / time_max);
</script>

<div class="thing">
    <span class="name">{name}</span>
    <span>{description}</span>
    {#if image}
        <span><img src={image} alt={name} /></span>
    {/if}

    {#if type === "string" && string === "?"}
        <span>You can do it <b> ? </b> times</span>
    {/if}

    {#if type === "string" && string !== "?"}
        <span>You can do it <b> {string} </b> </span>
    {/if}

    {#if type === "number" && time_max != -1}
        <span>You can do it <b> {thingDoMaxCount}-{thingDoCount}</b> times</span
        >
    {/if}
    {#if type === "number" && time_max == -1}
        <span>You can do it <b> {thingDoCount}</b> times</span>
    {/if}
</div>

<style>
    .thing {
        display: flex;
        flex-direction: column;
        border: 1px solid var(--border-color);
        border-radius: 10px;
        display: flex;
        align-items: center;
        padding: 1rem;
    }

    span {
        display: block;
        font-size: 1rem;
        align-self: center;
        height: 100%;
    }
    span.name {
        font-size: 1.5rem;
        font-weight: bold;
        text-align: center;
    }
</style>
