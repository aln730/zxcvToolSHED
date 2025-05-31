	<script>
		import katex from 'katex';
		import 'katex/dist/katex.min.css';

		let latexInput = '';
		let renderedLatex = '';
		let error = null;

		let debounceTimeout;

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


		function exportToPDF() {
			alert("PDF export not implemented yet."); // Placeholder
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
				<button on:click={exportToPDF}>Download PDF</button>
				{#if error}
					<p class="error">{error}</p>
				{/if}
			</div>

			<div class="box output" id="rendered-output">
				{@html renderedLatex}
			</div>
		</div>
	</div>
