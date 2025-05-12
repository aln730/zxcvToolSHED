<script lang="ts">
	import katex from 'katex';
	import 'katex/dist/katex.min.css';

	let latexInput = '';
	let renderedLatex = '';
	let error: string | null = null;

	function renderLatex() {
		error = null;
		try {
			renderedLatex = katex.renderToString(latexInput, {
				throwOnError: true,
				displayMode: true
			});
		} catch (err: any) {
			error = err.message;
			renderedLatex = '';
		}
	}
</script>

<style>
	.container {
		display: flex;
		gap: 1rem;
		margin-top: 1rem;
		flex-wrap: wrap;
	}

	.box {
		flex: 1;
		min-width: 300px;
	}

	textarea {
		width: 100%;
		height: 200px;
		padding: 1rem;
		font-size: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
		font-family: monospace;
		box-sizing: border-box;
	}

	button {
		margin-top: 1rem;
		padding: 0.5rem 1rem;
		background-color: #017026;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}

	.output {
		padding: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
		background: #f9f9f9;
		color: #000;
		min-height: 200px;
		box-sizing: border-box;
	}

	.error {
		color: darkred;
		font-weight: bold;
		margin-top: 1rem;
	}

	nav a {
		color: #0830e2;
		text-decoration: none;
	}
</style>

<div>
    <img src="latex.png" alt="latex">

	<nav>
		<h1><a href="/">Home</a> &gt; <span>LaTeX Previewer</span></h1>
	</nav>

	<div class="container">
		<div class="box">
			<textarea bind:value={latexInput} placeholder="Enter LaTeX here..."></textarea>
			<button on:click={renderLatex}>Render</button>
			{#if error}
				<p class="error">{error}</p>
			{/if}
		</div>

		<div class="box output">
			{@html renderedLatex}
		</div>
	</div>
</div>
