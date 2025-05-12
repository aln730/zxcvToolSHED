<script>
	const tools = [
		{ name: 'Regex Tester', path: '/regex' },
		{ name: 'Base64 Encoder/Decoder', path: '/base64' },
		{ name: 'Markdown Previewer', path: '/markdown' },
		{ name: 'Password Generator', path: '/password' },
		{ name: 'Ping Tool', path: '/ping' }
	];
</script>

<h1>zxcvHQ Toolshed</h1>
<ul>
	{#each tools as tool}
		<li><a href={tool.path}>{tool.name}</a></li>
	{/each}
</ul>

<style>
    @font-face {
      font-family: 'DejaVu Sans Mono';
      src: url('/DejaVuSansMono.ttf') format('truetype');
    }
  
    :global(body) {
      margin: 0;
      padding: 20px;
      background-color: #000;
      color: #0ff000;
      font-family: 'DejaVu Sans Mono', monospace;
      font-size: 14px;
    }
  
    h1 {
      margin-bottom: 20px;
    }
  
    ul {
      list-style-type: none;
      padding: 0;
    }
  
    li {
      margin: 10px 0;
    }
  
    a {
      color: #2b63dd;
      text-decoration: none;
      font-size: 16px;
    }
  
    a:hover {
      background-color: #0ff000;
      color: #000;
      padding: 2px 6px;
    }
  </style>
  