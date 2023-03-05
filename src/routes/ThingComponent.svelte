
<script lang="ts" >
    import type { Thing } from "./entities/Thing";


    function parseNumber(number : number): string {
        if (number === 0) {
            return "∞";
        }
        if (number === -1)
            return "?";
        return number.toString();
    }
    export let givenTime = 12345;
    /*
    $: name = thing.name;
    $: description = thing.description;
    $: image = thing.image;
    $: time = thing.time;
    $: type = thing.type;
    $: string = thing.string;
    $: time_max = thing.time_max;
    */
    export let name = "Farting";
    export let description = "Farting is a great thing to do";
    export let image = "";
    export let time = 123;
    export let time_max = -1;
    export let type = "number";
    export let string = "?";



    $: console.log(time, time_max,givenTime);
    console.log(time_max, time);

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

    {#if type === "number" && time_max !== -1}
        <span>You can do it <b> {thingDoMaxCount}-{thingDoCount}</b> times</span>
    {/if}
    {#if type === "number" && time_max === -1}
        <span>You can do it <b> {thingDoCount}</b> times</span>
    {/if}


</div>


<style>
    .thing {
        display: flex;
        flex-direction: column;
        border: 1px solid black;
        border-radius: 10px;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding:1rem
    }
    span {
        display:block;
        font-size:1rem;
    }
    span.name {
        font-size: 1.5rem;
        font-weight: bold;
    }
</style>