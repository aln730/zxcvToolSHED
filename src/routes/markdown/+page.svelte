<script>
    import { marked } from "marked";
    import katex from "katex";
    import "katex/dist/katex.min.css";
  
    let markdown = `# Welcome to Markdown Editor!`;
    let html = "";
    let error = null;
  
    let debounceTimeout;
  
    $: markdown, debounceRender();
  
    function renderMarkdown(md) {
      try {
        error = null;

        md = md.replace(/\$\$([^$]+)\$\$/g, (_, math) => {
          return katex.renderToString(math, { displayMode: true });
        });
  
        md = md.replace(/\$([^$\n]+)\$/g, (_, math) => {
          return katex.renderToString(math, { displayMode: false });
        });
  
        return marked.parse(md);
      } catch (err) {
        error = err.message;
        return "";
      }
    }
  
    function debounceRender() {
      clearTimeout(debounceTimeout);
      debounceTimeout = setTimeout(() => {
        html = renderMarkdown(markdown);
      }, 100);
    }
  
    function exportToPDF() {
      alert("PDF export not implemented yet."); 
    }
  </script>
  
  <style>
    .container {
      display: flex;
      gap: 50px;
      margin-top: 1rem;
      flex-wrap: wrap;
      max-width: 1200px;
      margin-left: auto;
      margin-right: auto;
    }
  
    .box {
      flex: 1;
      min-width: 5
      50px;
      height: 750px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
  
    textarea {
      width: 800px;
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
      width: 800px;
      min-height: 700px;
      font-family: Arial, sans-serif;
      font-size: 1rem;
      overflow-wrap: break-word;
      word-break: break-word;
      white-space: normal;
      overflow-y: auto;
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
  
    nav {
      margin-bottom: 1rem;
    }
  </style>
  
  <nav>
    <h1><a href="/">Home</a> &gt; <span>Markdown Editor</span></h1>
  </nav>
  
  <div class="container">
    <div class="box">
      <textarea bind:value={markdown} spellcheck="false" placeholder="Enter Markdown here..."></textarea>
      <button on:click={exportToPDF}>Download PDF</button>
      {#if error}
        <p class="error">{error}</p>
      {/if}
    </div>
  
    <div class="box output">
      {@html html}
    </div>
  </div>
  