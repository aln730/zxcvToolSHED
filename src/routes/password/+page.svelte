<script>
	const UPPERCASE = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
	const LOWERCASE = 'abcdefghijklmnopqrstuvwxyz';
	const NUMBERS = '0123456789';
	const SYMBOLS = '!@#$%^&*()-_=+[]{}|;:,.<>?';
	const AMBIGUOUS = 'O0l1';

	let length = 16;
	let includeUppercase = true;
	let includeLowercase = true;
	let includeNumbers = true;
	let includeSymbols = true;
	let avoidAmbiguous = true;
	let generatedPassword = '';
	let passwordStrength = '';

	function generatePassword() {
		let charset = '';
		if (includeUppercase) charset += UPPERCASE;
		if (includeLowercase) charset += LOWERCASE;
		if (includeNumbers) charset += NUMBERS;
		if (includeSymbols) charset += SYMBOLS;

		if (avoidAmbiguous) {
			charset = charset.split('').filter(c => !AMBIGUOUS.includes(c)).join('');
		}

		if (!charset.length) {
			generatedPassword = 'Please select at least one character set';
			return;
		}

		generatedPassword = Array.from({ length }, () => charset[Math.floor(Math.random() * charset.length)]).join('');
		calculateStrength();
	}

	function copyToClipboard() {
		navigator.clipboard.writeText(generatedPassword).then(() => {
			alert('Password copied to clipboard!');
		});
	}

	function calculateStrength() {
		let strengthPoints = 0;
		if (includeUppercase) strengthPoints++;
		if (includeLowercase) strengthPoints++;
		if (includeNumbers) strengthPoints++;
		if (includeSymbols) strengthPoints++;
		if (length >= 12) strengthPoints++;

		if (strengthPoints <= 2) passwordStrength = 'Weak';
		else if (strengthPoints === 3 || strengthPoints === 4) passwordStrength = 'Moderate';
		else passwordStrength = 'Strong';
	}
</script>

<style>
	.container {
		max-width: 600px;
		margin: 2rem auto;
		font-family: sans-serif;
	}
	input[type="range"] {
		width: 100%;
	}
	.output {
		background: #f4f4f4;
		padding: 1rem;
		border-radius: 8px;
		margin-top: 1rem;
		font-family: monospace;
		word-break: break-all;
        color:#000;
	}
	button {
		margin-top: 1rem;
		padding: 0.5rem 1rem;
		background: #0d7e02;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
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

<div class="container">
    <img src="/password.png" alt="password">
    <nav>
		<h1><a href="/">Home</a> &gt; <span>Password Generator  </span></h1>
	</nav>

	<input type="range" min="4" max="64" bind:value={length} />

	<label><input type="checkbox" bind:checked={includeUppercase} /> Include Uppercase</label><br>
	<label><input type="checkbox" bind:checked={includeLowercase} /> Include Lowercase</label><br>
	<label><input type="checkbox" bind:checked={includeNumbers} /> Include Numbers</label><br>
	<label><input type="checkbox" bind:checked={includeSymbols} /> Include Symbols</label><br>
	<label><input type="checkbox" bind:checked={avoidAmbiguous} /> Avoid Ambiguous Characters (O, 0, l, 1)</label>

	<br>
	<button on:click={generatePassword}>Generate Password</button>
	{#if generatedPassword}
		<div class="output">{generatedPassword}</div>
		<p>Strength: <strong>{passwordStrength}</strong></p>
		<button on:click={copyToClipboard}>Copy to Clipboard</button>
	{/if}
</div>
