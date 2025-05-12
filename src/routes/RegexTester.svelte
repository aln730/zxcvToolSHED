<script>
  let pattern = ''; 
  let testString = '';
  let result = '';
  let errorMessage = '';

  // Function to test the regex
  function testRegex() {
    try {
      const regex = new RegExp(pattern);
      result = testString.match(regex) ? testString.match(regex).join(', ') : 'No matches found';
      errorMessage = '';  // Clear any previous error
    } catch (e) {
      errorMessage = 'Invalid Regex: ' + e.message;
      result = '';
    }
  }
</script>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
  }
  input, button {
    margin: 0.5rem;
    padding: 0.5rem;
    font-size: 1rem;
    width: 80%;
    max-width: 500px;
  }
  .result {
    margin-top: 1rem;
    font-size: 1.2rem;
    color: green;
  }
  .error {
    margin-top: 1rem;
    font-size: 1.2rem;
    color: red;
  }
</style>

<div class="container">
  <h2>Regex Tester</h2>

  <input
    type="text"
    placeholder="Enter Regex Pattern"
    bind:value={pattern}
    on:input={testRegex}
  />

  <input
    type="text"
    placeholder="Enter Test String"
    bind:value={testString}
    on:input={testRegex}
  />

  <button on:click={testRegex}>Test Regex</button>

  {#if result}
    <div class="result">Matches: {result}</div>
  {/if}

  {#if errorMessage}
    <div class="error">{errorMessage}</div>
  {/if}
</div>
