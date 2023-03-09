<script lang="ts">
	const API_URL = "https://dowhatintime.mantikafasi.dev/";
	//const API_URL = "http://localhost:8081/";
	import Counter from '../components/Counter.svelte';
    import ThingComponent from '../components/ThingComponent.svelte';
	import type { Thing } from './entities/Thing';

	let days = 0;
	let hours = 0;
	let minutes = 0;

	let thingsToDo : Thing[] = [{"name":"Enter a time to see what you can do","description":"","image":"","time":0,"time_max":-1,"type":"string","string":""}];

	$: givenTime = 0;

	function calculateThings() {

		givenTime = 86400 * days + hours * 3600 + minutes * 60 ;
		fetch(API_URL + "api/get/things?time=" + givenTime, {
			method: "GET",
			headers: {
				"Content-Type": "application/json"
			}
		}).then((response) => {
			return response.json();
		}).then((data) => {
			
			(data as Thing[]).forEach((element) => {
				element.time_max ??= -1
			});
			
			thingsToDo = data;

		});
	}


</script>

<svelte:head>
	<title>Do What In Time</title>
	<meta name="description" content="Do What In Time" />
</svelte:head>
<h1>
	<span class="headertext">
		How much time do you have?
	</span>
</h1>

<div class="counters">
	<Counter counterName = {"Days"} bind:value={days} limit={30}/>
	<Counter counterName = {"Hours"} bind:value={hours} limit = {24}/>
	<Counter counterName = {"Minutes"} bind:value={minutes} limit = {60}/>
</div>

<button class= "btn-grad" on:click={()=>calculateThings()}>
	Lemme Calculate
</button>

<div class="things">
	{#each thingsToDo as thing }
		<ThingComponent {...thing} givenTime = {givenTime} />
	{/each}
</div>


<style>
	.things {
		display: grid;
		grid-template-columns: auto auto auto;
		column-gap: 1rem;
		row-gap: 1rem;
		padding-top: 1rem;
		align-self: center;
		grid-template-columns: repeat(auto-fit, minmax(15rem, 1fr));
		width: 100%;
		max-width: 50rem;
		margin: 0 auto;
		box-sizing: border-box;
		margin-top: 2rem;
	}

	.counters {
		flex-direction: row;
		align-self: center;
		display: flex;

	}

	h1 {
		width: 100%;
	}

	.headertext {
		display: block;
		width: 100%;
		margin-top: 10%;
	}
         
	.btn-grad {
		background-image: linear-gradient(to right, #4776E6 0%, #8E54E9  51%, #4776E6  100%);
		padding: 15px 45px;
		text-align: center;
		text-transform: uppercase;
		transition: 0.5s;
		color: white;
		box-shadow: 0 0 10px var(--color-bg-1);
		border-radius: 10px;
		display: block;
		align-self: center;
		width: 16rem;
		margin-top: 1rem;
	}

	.btn-grad:hover {
		background-position: right center;
		color: #fff;
		text-decoration: none;
		cursor:pointer;
	}
		
</style>
