<script>
	import katex from 'katex';
	import 'katex/dist/katex.min.css';
	import { onMount } from 'svelte';

	let latexInput = '';
	let renderedLatex = '';
	let error = null;

	let debounceTimeout;
	let html2pdf = null;
	let exporting = false;

	// Dynamically import html2pdf only on client side
	onMount(async () => {
		const mod = await import('html2pdf.js');
		html2pdf = mod.default;
	});

	$: latexInput, debounceRender();

	function debounceRender() {
		clearTimeout(debounceTimeout);
		debounceTimeout = setTimeout(() => {
			try {
				error = null;

				let inputToRender = latexInput.trim();

				if (!inputToRender.match(/\\[a-zA-Z]+|[\^\_\{\}]/)) {
					const escaped = inputToRender
						.replace(/&/g, '&amp;')
						.replace(/</g, '&lt;')
						.replace(/>/g, '&gt;');

					renderedLatex = `<pre style="white-space: pre-wrap; word-break: break-word; font-family: monospace;">${escaped}</pre>`;
				} else {
					renderedLatex = katex.renderToString(inputToRender, {
						throwOnError: true,
						displayMode: true
					});
				}
			} catch (err) {
				error = err.message;
				renderedLatex = '';
			}
		}, 50);
	}

	async function exportToPDF() {
		if (!html2pdf) {
			alert("PDF export library is not loaded yet. Please try again in a moment.");
			return;
		}
		exporting = true;
		const outputElement = document.getElementById("rendered-output");
		const clone = outputElement.cloneNode(true);
		clone.style.width = '800px';

		try {
			await html2pdf()
				.set({
					margin: 0.5,
					filename: 'latex-output.pdf',
					image: { type: 'jpeg', quality: 0.98 },
					html2canvas: { scale: 2 },
					jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
				})
				.from(clone)
				.save();
		} catch (e) {
			alert("Error exporting PDF: " + e.message);
		}
		exporting = false;
	}
</script>

<style>
	.container {
		display: flex;
		gap: 50px;
		margin-top: 1rem;
		flex-wrap: wrap;
	}

	.box {
		flex: 1;
		width: 800px;
		height: 750px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	textarea {
		width: 100%;
		height: 700px;
		padding: 1rem;
		font-size: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
		font-family: monospace;
		resize: none;
		box-sizing: border-box;
	}

	button {
		align-self: flex-start;
		padding: 0.5rem 1rem;
		font-size: 0.9rem;
		background-color: #017026;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		margin-top: 0.5rem;
	}

	button:disabled {
		background-color: #555;
		cursor: not-allowed;
	}

	.output {
		padding: 1.5rem;
		border: 1px solid #ccc;
		border-radius: 4px;
		background: #f9f9f9;
		color: #000;
		min-height: 700px;
		font-family: monospace;
		font-size: 1rem;
		box-sizing: border-box;
		overflow-wrap: break-word;
		word-break: break-word;
		white-space: normal;
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

	h2 a {
		color: #0830e2;
		text-decoration: none;
		text-align: center;
	}
</style>

<img src="LaTeX.png" width="150px" height="25px" alt="LaTeX logo" />
<h2><a href="https://quickref.me/latex" target="_blank">CLICK ME FOR QUICK REFERENCE!!</a></h2>

<div>
	<nav>
		<h1><a href="/">Home</a> &gt; <span>LaTeX Previewer</span></h1>
	</nav>

	<div class="container">
		<div class="box">
			<textarea bind:value={latexInput} placeholder="Enter LaTeX here..."></textarea>
			<button on:click={exportToPDF} disabled={exporting}>
				{exporting ? 'Exporting...' : 'Download PDF'}
			</button>
			{#if error}
				<p class="error">{error}</p>
			{/if}
		</div>

		<div class="box output" id="rendered-output">
			{@html renderedLatex}
		</div>
	</div>
</div>
