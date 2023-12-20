<script>
	// @ts-nocheck

	import axios from 'axios';
	let word = '';
	let advices = [];
	let advice =
		"Loading brilliance... It won't be long before your mind is treated to some serious wisdom";
	function randomAdvice(word) {
		for (let i = 0; i < word; i++) {
			const randomNumber = Math.floor(Math.random() * 120) + 1;
			axios
				.get(`https://api.adviceslip.com/advice/${randomNumber}`)
				.then((response) => {
					advices = [...advices, response.data.slip];
				})
				.catch((error) => {
					console.error('Error fetching advice:', error);
					advices = ['Unable to fetch advice at the moment.'];
				});
		}
	}

	function advicebyWord() {
		if (word == '') {
			advice = 'Please enter a word';
			return;
		}
		axios
			.get('https://api.adviceslip.com/advice/search/' + word + '')
			.then((response) => {
				if (response.data.slips && response.data.slips.length > 0) {
					advices = response.data.slips;
				} else {
					advice = 'OOPS! No advice found! Try some other words';
				}
			})
			.catch((error) => {
				console.error('Error fetching advice:', error);
				advices = ['Unable to fetch advice at the moment.'];
			});
	}
	function adviceGenerator() {
		advices = [];
		if (!isNaN(word)) {
			randomAdvice(word);
		} else {
			advicebyWord();
		}
	}
	function handleEnterKey(event) {
		if (event.key === 'Enter') {
			adviceGenerator();
		}
	}
</script>

<main>
	<h1>GUIDANCE GURU</h1>
	{#if advices.length > 0}
		<div class="advice-box">
			{#each advices as advice, index}
				<p>{index + 1}. {advice.advice}</p>
			{/each}
		</div>
	{/if}
	<div class="mbl-responsive">
		<input
			type="text"
			bind:value={word}
			on:keydown={handleEnterKey}
			placeholder="Enter a number or word"
		/>

		<button class="btn" on:click={adviceGenerator}>GET ADViCE</button>
	</div>
</main>

<style>
	@import '../../../globals.css';
	:global(body) {
		font-family: 'Open Sans', sans-serif;
		background: radial-gradient(#ffddcc 0%, #ff8484 100%);
		color: #333;
		font-weight: 550;
	}
	main {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	input {
		padding: 1rem;
		width: 18rem;
		border-radius: 1rem;
		outline: none;
		border: none;
		font-size: 1rem;
		box-shadow: 7px 6px 28px 1px rgba(0, 0, 0, 0.24);
	}
	.btn {
		width: 20rem;
		text-transform: uppercase;
		margin-top: 1.2rem;
	}
	.advice-box {
		background-color: #ffffff;
		width: 60%;
		margin-bottom: 3rem;
		margin-top: 1rem;
		padding: 0 1rem;
		border: 4px solid rgb(255, 255, 255);
		box-shadow: 7px 6px 28px 1px rgba(0, 0, 0, 0.24);
	}
    @media (max-width:600px)
    {
        .mbl-responsive{
            display: flex;
            flex-direction: column;
        }
        .advice-box{
            width:80%;
            border-radius: 1rem;
        }
    }
</style>
