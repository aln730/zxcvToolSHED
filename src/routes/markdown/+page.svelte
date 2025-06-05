<script>
  import { onMount } from "svelte";
  import { marked } from "marked";
  import katex from "katex";
  import "katex/dist/katex.min.css";

  let markdown = `# Welcome to Markdown Editor!`;
  let html = "";
  let error = null;
  let debounceTimeout;
  let html2pdf = null;
  let exporting = false;

  onMount(async () => {
    const mod = await import('html2pdf.js');
    html2pdf = mod.default || mod; 
  });

  $: markdown, debounceRender();

  function renderMarkdown(md) {
    try {
      error = null;

      let parsed = marked.parse(md, { gfm: true, breaks: true, sanitize: false });


      parsed = parsed.replace(/\$\$([^$]+)\$\$/g, (_, math) =>
        katex.renderToString(math, { displayMode: true })
      );

      parsed = parsed.replace(/\$([^$\n]+)\$/g, (_, math) =>
        katex.renderToString(math, { displayMode: false })
      );

      return parsed;
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

  async function exportToPDF() {
    if (!html2pdf) {
      alert("PDF export library is not loaded yet. Please try again in a moment.");
      return;
    }
    exporting = true;
    const outputElement = document.querySelector(".output");
    const clone = outputElement.cloneNode(true);
    clone.style.width = '800px';

    try {
      await html2pdf()
        .set({
          margin: 0.5,
          filename: 'markdown-output.pdf',
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
    max-width: 1200px;
    margin-left: auto;
    margin-right: auto;
  }

  .box {
    flex: 1;
    min-width: 550px;
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
    <textarea
      bind:value={markdown}
      spellcheck="false"
      placeholder="Enter Markdown here..."
    ></textarea>
    <button on:click={exportToPDF} disabled={exporting}>
      {exporting ? "Exporting..." : "Download PDF"}
    </button>
    {#if error}
      <p class="error">{error}</p>
    {/if}
  </div>

  <div class="box output">{@html html}</div>
</div>
