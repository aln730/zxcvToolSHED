<script lang="ts">
    let isEncoding = true; 
    let inputText = '';    
    let resultText = '';  
    let error: string | null = null; 
  

    function handleConversion() {
      error = null;  
      try {
        if (isEncoding) {
          resultText = btoa(inputText);
        } else {
          resultText = atob(inputText); 
        }
      } catch (err: any) {
        error = 'Invalid input for decoding.';
        resultText = '';
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
      color: #000;
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
  
    nav a {
      color: #0830e2;
      text-decoration: none;
    }

    .radio-group {
	display: flex;
	gap: 1rem;
	margin-bottom: 1rem;
}

.radio-group label {
	display: flex;
	align-items: center;
	gap: 0.25rem;
	font-weight: normal;
}

  </style>
  
  <div class="container">
    <img src="/base649.png" alt="base64">
    <nav>
        <h1>
        <a href="/">Home</a> &gt; <span>Base64 Encoder/Decoder</span>
    </h1>
    </nav>
  
    <form>
        <div class="radio-group">
            <label>
              <input 
                type="radio" 
                bind:group={isEncoding} 
                value={true}
              />
              Encode
            </label>
            <label>
              <input 
                type="radio" 
                bind:group={isEncoding} 
                value={false}
              />
              Decode
            </label>
          </div>
          
      <div>
        <label for="inputText">Input Text:</label>
        <textarea
          id="inputText"
          bind:value={inputText}
          placeholder="Enter text here..."
          rows="6"
        ></textarea>
      </div>
  
      <button type="button" on:click={handleConversion}>Convert</button>
    </form>
  

    {#if error}
      <p class="error">{error}</p>
    {/if}
  

    <div class="result">
      {#if resultText}
        <pre id="outputText" class="matches">{resultText}</pre>
      {:else}
        <p>No result yet.</p>
      {/if}
    </div>
  </div>
  