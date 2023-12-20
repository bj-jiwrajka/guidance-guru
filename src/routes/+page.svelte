<script>
    import { goto } from "$app/navigation";
</script>

<main>
	<h1>Guidance Guru: Your Path To Wisdom</h1>
	<h3><span>" </span>Unlock the power of guidance for a fulfilled life <span>"</span></h3>
	<div class="desc">
		<p>
			At Guidance Guru, we understand that life is full of questions. Whether you seek wisdom for a
			specific situation or simply crave insightful advice, our platform is here for you. Connect
			with Guidance Gurus from diverse backgrounds offering personalized advice. Enter a keyword or
			receive a random nugget of wisdom. Your answers await.
		</p>
	</div>
	<button
		on:click={() => {
		goto('/advice');
		}}>Get Advice Now</button
	>
    
</main>

<style>
	@import './../../globals.css';
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
		justify-content: center;
		align-items: center;
	}
	h1 {
		font-size: 3rem;
		font-weight: 700;
		margin-bottom: 1rem;
	}
	h3 {
		font-size: 1.5rem;
		font-weight: 400;
		font-style: italic;
	}
	span {
		color: #ff6d6d;
		font-size: 2rem;
	}
	.desc {
		width: 80%;
	}
	@media (max-width:900px)
	{
		h1 {
		font-size: 1.5rem;
		text-align: center;
	}
	h3 {
		font-size: 1.2rem;
		width:90%;
	}
	span {
		color: #ff6d6d;
		font-size: 1rem;
	}
	.desc {
		width: 90%;
	}
	}
</style>
