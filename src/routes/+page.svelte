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
	<script>

		if (document) {
			if (localStorage.getItem("theme") === "dark") document.documentElement.classList.add('dark');
    	}
	</script>
</svelte:head>
<section>
	<h1>
		<span class="welcome">
			How much time do you have?
		</span>
	</h1>
	<section class="counters">
		<Counter counterName = {"Days"} bind:value={days}/>
		<Counter counterName = {"Hours"} bind:value={hours}/>
		<Counter counterName = {"Minutes"} bind:value={minutes}/>
	</section>

	<button class= "btn-grad" on:click={()=>calculateThings()}>
		Lemme Calculate
	</button>

</section>

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
	}

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		height: max-content;
		align-items: center;
		flex: 0.6;
	}

	section .counters {
		flex: 0.5;
	}

	.counters {
		flex-direction: row;
		align-self: center;
		margin-top: 1rem;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		margin-top: 5%;
	}
         
	.btn-grad {
		background-image: linear-gradient(to right, #4776E6 0%, #8E54E9  51%, #4776E6  100%);
		padding: 15px 45px;
		text-align: center;
		text-transform: uppercase;
		transition: 0.5s;
		color: white;
		box-shadow: 0 0 10px gray;
		border-radius: 10px;
		display: block;
	}

	.btn-grad:hover {
		background-position: right center;
		color: #fff;
		text-decoration: none;
		cursor:pointer;
	}
		
</style>
