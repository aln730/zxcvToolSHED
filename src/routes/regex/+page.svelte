<script lang="ts">
	let pattern = '';
	let flags = '';
	let testString = '';
	let result: RegExpMatchArray | null = null;
	let error: string | null = null;

	function runTest() {
		error = null;
		try {
			const regex = new RegExp(pattern, flags);
			result = testString.match(regex);
		} catch (err: any) {
			error = err.message;
			result = null;
		}
	}
</script>

<style>
	form > div {
		margin-bottom: 1rem;
	}

	label {
		display: block;
		margin-bottom: 0.25rem;
		font-weight: 500;
	}

	input,
	textarea {
		width: 100%;
		padding: 0.5rem;
		font-size: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
	}

	button {
		padding: 0.5rem 1rem;
		font-size: 1rem;
		background-color: #017026;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}

	button:hover {
		background-color: #00470f;
	}

	.result {
		margin-top: 1rem;
	}

	.error {
		color: darkred;
		font-weight: bold;
	}

	.matches {
		background-color: #f2f2f2;
		padding: 0.5rem;
		border-radius: 4px;
		font-family: monospace;
	}
    nav a{
        color: #0830e2;
        text-decoration: none;
    }
</style>

<main>
    <img src="/regex.png" alt="regex">
    <nav>
        <h1>
        <a href="/">Home</a> &gt; <span>Regex Tester</span>
    </h1>
    </nav>
	<form on:submit|preventDefault={runTest}>
		<div>
			<label for="pattern">Regex Pattern</label>
			<input
				id="pattern"
				type="text"
				bind:value={pattern}
				placeholder="e.g. \\bword\\b"
			/>
		</div>

		<div>
			<label for="flags">Flags</label>
			<input
				id="flags"
				type="text"
				bind:value={flags}
				placeholder="e.g. gi"
			/>
		</div>

		<div>
			<label for="test">Test String</label>
			<textarea
				id="test"
				rows="5"
				bind:value={testString}
				placeholder="Text to test..."
			></textarea>
		</div>

		<button type="submit">Test Regex</button>
	</form>

	<div class="result">
		{#if error}
			<p class="error">Error: {error}</p>
		{:else if result}
			<p>
				<strong>Matches:</strong>
				{#if result.length > 0}
					<pre class="matches">{JSON.stringify(result, null, 2)}</pre>
				{:else}
					<em>No matches found.</em>
				{/if}
			</p>
		{:else}
			<p><em>No result yet.</em></p>
		{/if}
	</div>
</main>
