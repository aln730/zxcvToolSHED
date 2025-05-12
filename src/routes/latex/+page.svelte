<script lang="ts">
	import katex from 'katex';
	import 'katex/dist/katex.min.css';
	import jsPDF from 'jspdf';
	import html2canvas from 'html2canvas';

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

	async function exportToPDF() {
		const outputEl = document.getElementById('rendered-output');
		if (!outputEl) return;

		const canvas = await html2canvas(outputEl);
		const imgData = canvas.toDataURL('image/png');
		const pdf = new jsPDF();

		const imgWidth = 190;
		const imgHeight = (canvas.height * imgWidth) / canvas.width;

		pdf.addImage(imgData, 'PNG', 10, 10, imgWidth, imgHeight);
		pdf.save('latex-output.pdf');
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
	}

	textarea {
		width: 800px;
		height: 750px;
		padding: 1rem;
		font-size: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
		font-family: monospace; 
        resize: none;
	}


	button {
		margin-top: 1rem;
		padding: 0.75rem 1.5rem; /* Increased button size */
		background-color: #017026;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}

	.output {
		padding: 1.5rem; /* Increased padding in the output box */
		border: 1px solid #ccc;
		border-radius: 4px;
		background: #f9f9f9;
		color: #000;
		min-height: 300px; /* Increased height for the output box */
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


    h2 a{
        color: #0830e2;
		text-decoration: none;
        text-align: center;
    }

</style>

<h2><a href="https://quickref.me/latex">CLICK ME FOR QUICK REFERENCE!!</a></h2>
<div>
	<nav>
		<h1><a href="/">Home</a> &gt; <span>LaTeX Previewer</span></h1>
	</nav>

	<div class="container">
		<div class="box">
			<textarea bind:value={latexInput} placeholder="Enter LaTeX here..."></textarea>
			<button on:click={renderLatex}>Render</button>
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
