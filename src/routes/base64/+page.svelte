<script lang="ts">
	let inputText = '';
	let resultText = '';
	let errorMessage = '';
	let isEncoding = true;

	// Handle encoding and decoding
	function handleConversion() {
		errorMessage = ''; // Reset error
		try {
			if (isEncoding) {
				// Encoding
				resultText = btoa(inputText); // Base64 encoding
			} else {
				// Decoding
				resultText = atob(inputText); // Base64 decoding
			}
		} catch (e) {
			errorMessage = 'Invalid input for ' + (isEncoding ? 'encoding' : 'decoding');
			resultText = '';
		}
	}
</script>

<main class="container">
	<h1 class="title">Base64 Encoder/Decoder</h1>
	
	<!-- Radio buttons for choosing encode or decode -->
	<div class="operation">
		<label>
			<input type="radio" bind:checked={isEncoding} />
			Encode
		</label>
		<label>
			<input type="radio" bind:checked={!isEncoding} />
			Decode
		</label>
	</div>

	<!-- Textarea for input -->
	<div class="input-area">
		<label for="inputText">Input Text</label>
		<textarea
			id="inputText"
			bind:value={inputText}
			placeholder="Enter text to encode or decode"
			rows="4"
			class="textarea"
		></textarea>
	</div>

	<!-- Button to trigger conversion -->
	<button class="button" on:click={handleConversion}>Convert</button>

	<!-- Result area -->
	<div class="result">
		{#if errorMessage}
			<p class="error">{errorMessage}</p>
		{:else if resultText}
			<p class="result-text">
				<strong>Result:</strong>
				<pre>{resultText}</pre>
            </p>
            
		{:else}
			<p class="placeholder">No result yet.</p>
		{/if}
	</div>
</main>

<style>
	.container {
		width: 100%;
		max-width: 600px;
		margin: 0 auto;
		padding: 20px;
		font-family: Arial, sans-serif;
	}
	.title {
		text-align: center;
		font-size: 24px;
		margin-bottom: 20px;
	}
	.operation {
		display: flex;
		justify-content: space-evenly;
		margin-bottom: 10px;
	}
	.input-area {
		margin-bottom: 10px;
	}
	.textarea {
		width: 100%;
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 4px;
		resize: none;
	}
	.button {
		display: block;
		width: 100%;
		padding: 10px;
		background-color: #4caf50;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-size: 16px;
	}
	.button:hover {
		background-color: #45a049;
	}
	.result {
		margin-top: 20px;
	}
	.error {
		color: red;
	}
	.result-text {
		white-space: pre-wrap;
		background-color: #f4f4f4;
		padding: 10px;
		border-radius: 4px;
	}
	.placeholder {
		color: #888;
	}
</style>
