
<script>
    export let name = "Farting";
    export let description = "Farting is a great thing to do";
    export let image = "";
    export let givenTime = 12345;
    export let time = 123;

    let thingDoCount = Math.floor(givenTime / time);

</script>

<div class="thing">
    <span class="name">{name}</span>
    <span>{description}</span>
    {#if image}
    <span><img src={image} alt={name} /></span>
    {/if}

    <span>You can do it <b> {thingDoCount}</b> times</span>

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