<script>
	const tools = [
		{ name: '>Regex Tester<', path: '/regex' },
		{ name: '>Base64 Encoder/Decoder<', path: '/base64' },
		{ name: '>Latex Previewer<', path: '/latex' },
		{ name: '>Password Generator<', path: '/password' },
	];
</script>
<div id="axo">
<pre><a href="https://zxcvhq.dev/"><span>
⠀⠀⣠⣴⣶⣾⢷⣶⣶⣤⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣤⣶⣶⣾⣶⣶⣦⣀⠀
⣴⣾⣿⢫⠳⡜⣎⠶⣩⢝⡻⢿⣦⣄⠀⠀⠀⠀⠀⣀⣀⣤⣤⣤⣤⣤⣤⣤⣀⡀⠀⠀⠀⠀⠀⣠⣴⡿⣛⡝⢦⡓⢶⣘⢦⡛⢿⣦
⠘⣿⣯⢗⣫⠳⣜⢣⡓⢮⡜⣣⠝⣻⣷⣄⣠⣴⡾⠟⠛⠉⠉⠈⠁⠉⢈⠉⠛⠻⢿⣦⣀⣠⣾⢟⡣⢇⡳⣜⢣⡝⢦⡛⢦⣝⣹⣿
⠀⠈⠻⢿⣶⣽⣬⣧⣙⣦⡓⣥⢛⡴⣩⣿⠻⠀⠀⠠⠐⠈⠄⡁⠐⠈⠄⢠⠂⠄⡀⠬⠿⢿⣇⢮⡱⣋⢶⣩⣖⣹⣦⣽⣷⡾⠟⠁
⠀⠀⠀⠀⠀⠉⣉⣙⣹⣛⠻⢷⣿⣾⣿⠿⠶⢾⣶⣧⣄⠃⡐⢀⠂⡁⠢⠠⢜⣶⠞⠷⣶⣧⡹⢷⣷⣿⣟⣻⣿⣏⡉⠉⠀⠀⠀⠀
⠀⠀⠀⣤⣶⠿⡟⢿⡛⠿⢿⣿⢿⣿⡏⠀⢀⣼⣿⣿⡏⠠⠐⡀⠂⡄⠑⡀⢻⣇⡈⢀⣼⣿⣿⣌⢿⣿⢻⡛⣟⠻⠿⣿⣶⣄⠀⠀
⠀⠀⢼⣟⣣⢛⡜⣣⢍⡻⣼⡿⠘⣿⣿⣶⣿⣿⣿⠏⢰⡆⢁⠐⠡⢀⠁⢶⡅⠻⣿⣿⣿⣿⣿⣿⠊⣿⣦⠹⣌⢏⡳⢆⡻⣿⡆⠀
⠀⠀⠺⣿⣴⣫⣼⣷⠾⣿⣿⡇⡘⣍⠛⡛⢛⠋⡔⠠⠙⢷⣤⡼⠷⣦⣬⡾⠃⠰⡌⠛⡛⠛⢛⠳⡀⢼⣿⣿⢾⣮⣵⣯⣶⣿⠟⠀
⠀⠀⠀⠈⠉⠉⢉⣴⣾⠿⣛⣷⠐⡌⢆⠥⢎⠲⢁⢂⠡⡀⠄⡐⠠⢀⠡⡀⢌⡐⠬⡑⢆⢧⠨⠓⡐⣾⡟⣿⣶⣌⠉⠉⠉⠀⠀⠀
⠀⠀⠀⠀⠀⠀⣾⡿⣍⠞⣥⣿⣧⡐⠌⡒⠌⠦⣁⠎⡰⢁⠎⠰⡁⢎⡐⢡⠂⡜⠰⡈⢆⠢⣁⢃⣾⣿⡜⢦⡛⣿⣆⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⣿⣷⣮⠿⣿⣯⣿⣿⠷⣬⣜⡐⠤⢊⠔⡡⢊⠱⢈⠆⡘⢄⠣⠌⡑⢌⣰⣦⣾⣿⣿⣽⡿⠷⣽⣾⡿⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠈⢻⣇⠀⠀⠠⠉⣿⠠⣉⠹⣿⣶⣥⣶⣤⣡⣊⣔⣨⣴⣬⣴⣵⣾⣿⠉⡔⢸⡏⠉⢀⠀⠀⣼⣿⠁⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⢈⣿⠀⠈⡅⠂⣿⡇⣀⢺⡿⡍⢉⠡⣉⠙⣉⠋⡍⣉⢉⡉⡉⢜⣿⡖⡈⢾⡇⣁⠂⠌⢀⣿⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠈⣿⡆⠀⣁⠒⣸⣇⠤⢸⣷⡈⢆⠓⡄⢣⡐⢃⠲⣐⠊⡔⢉⠆⣿⠠⡁⢿⡃⠤⡘⠠⢸⡇⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⢹⣷⠀⠠⠒⡠⣿⠀⠄⣿⣷⠈⡜⣈⠆⡌⢣⠱⢠⠃⡔⢡⢚⣿⠀⡐⣿⡁⠢⣁⠂⣿⡇⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠘⣿⡀⠐⡡⢹⣟⡧⣬⣙⣿⡆⠔⡡⠚⡌⢆⡃⠧⡘⢀⢲⣿⢡⣤⢿⣿⡇⢡⠠⢤⣿⠃⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⢻⡆⢡⠐⣉⠙⡛⠾⠛⡋⠜⣨⠑⣣⠘⢆⠥⢣⡑⠨⠄⠛⠛⠷⢛⢋⠡⢂⠼⣸⡟⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⠠⡙⢄⡊⠔⣁⠣⢌⡱⢂⡍⢤⢋⡌⡚⠤⡌⡱⢨⠡⡉⢆⡡⢊⠔⡩⣘⣿⠁⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⣀⢀⣿⣇⠘⡤⡑⢪⠄⢣⠌⡒⢥⡘⠆⢎⠴⡉⢖⠡⢒⠡⣃⠜⠤⢒⡉⠦⡑⢼⡿⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢠⣴⠞⠛⠉⠉⠉⣿⡐⢢⠑⢣⡘⡡⢊⡕⢢⢌⡹⣈⠦⡙⢤⠋⡬⢑⡐⣊⠱⢊⠴⠡⢌⣿⣇⡀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⣿⠎⡐⠈⢂⠰⠀⠈⠻⢷⣬⣁⠆⡅⢣⠘⢆⠦⣑⢢⠒⡍⢢⠓⡐⢣⠘⡄⢃⢎⣤⡷⠟⠁⢉⣷⣄⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠘⠷⣭⣶⣭⣤⣤⣤⣐⠢⢌⢛⠻⢶⣧⣾⣤⣶⣐⣊⣱⣨⣁⣎⣘⣤⡷⠾⠞⡛⠁⢀⠴⡈⠆⣌⠙⣷⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠁⠈⠙⠻⠾⣮⣷⡶⢛⠚⡳⢛⡟⣛⠛⣛⠛⡛⢙⣻⢷⣯⣾⣤⡶⠟⣾⣷⣽⣶⡿⠛⠀⠀⠀⠀⠀⠀
</span></a></pre>
    </div>        
<div class="container">
	<h1>*zxcvHQ-ToolSHED*</h1>
	<ul>
		{#each tools as tool}
			<li><a href={tool.path}>{tool.name}</a></li>
		{/each}
	</ul>
</div>

<div style="position: fixed; bottom: 0; left: 0; right: 0; display: flex; flex-direction: column; align-items: center; z-index: 1;">
    <div style="display: flex; justify-content: center; flex-wrap: wrap;">
      <a href="https://github.com/ComputerScienceHouse"><img src="/gCSH.png" style="width:54px;"></a>
      <a href="https://fedoraproject.org/"><img src="/fedora.png" style="width:150px;"></a>
      <a href="http://www.openarena.ws"><img src="/quake.gif" style="width:150px;"></a>
      <a href="https://proxmox.com/en/"><img src="/proxmox.png" style="width:150px;"></a>
      <a href="https://nixos.org/"><img src="/nixos.png" style="width:146px;"></a>
      <a href="https://jellyfin.org/"><img src="/jellyfin.gif" style="width:150px;"></a>
      <a href="https://www.desmos.com/calculator"><img src="/something.gif" style="width:150px;"></a>
      <a href="https://www.intel.com/content/www/us/en/download-center/home.html"><img src="/driver.gif" style="width:150px;"></a>
      <a href="https://proton.me/mail"><img src="/mail.gif" style="width:150px;"></a>
      <a href="https://zxcv-homepage-git-zxvchomepage.apps.okd4.csh.rit.edu/"><img src="/search.gif" style="width:158px;"></a>
      <a href="https://github.com/aln730"><img src="/github.png" style="width:150px;"></a>
    </div>  
  </div>

<style>
  @font-face {
    font-family: 'DejaVu Sans Mono';
    src: url('/DejaVuSansMono.ttf') format('truetype');
  }

  :global(body) {
    margin: 0;
    padding: 0;
    background-color: #000;
    color: #0ff000;
    font-family: 'DejaVu Sans Mono', monospace;
    font-size: 14px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .container {
    text-align: center;
  }

  #axo a {
  color: #0ff000;
  text-decoration: none;
  font-size: 14px;
  text-shadow: 0 0 5px #0ff000, 0 0 10px #0ff000, 0 0 15px #0ff000;
}


h1 {
  margin-bottom: 10px;
  text-shadow: 0 0 1px #0ff000, 0 0 1.5px #0ff000, 0 0 2px #0ff000;
}


  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    margin: 10px 0;
  }

  .container ul a {
    color: #2b63dd;
    text-decoration: none;
    font-size: 16px;
  }

  .container ul a:hover {
    background-color: #0ff000;
    color: #000;
    padding: 2px 6px;
  }

</style>
