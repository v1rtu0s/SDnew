<script>

	import { tweened } from 'svelte/motion';
		import { cubicOut } from 'svelte/easing';
	
	
	var result = 0;
	var resultarray = [];
	var ergebnis_single = [];
	var ergebnis_float = 0;
	var nonce = 0;
	var targetnumber = 50;
	var test = "xyz";
	var targetmultiplier = "2";
	
	
	$: targetmultiplier = (100/(100-targetnumber)).toFixed(2);
	
	const progress = tweened(0, {
			duration: 300,
		easing: cubicOut
	  
			});
	
	const progress_string = tweened("abc", {
			duration: 400,
			easing: cubicOut});
	
	
	
	function roll() {
	nonce++;
	result = Math.random()*100;
	
	resultarray.push(result);
	console.log(resultarray);
	
	ergebnis_single = resultarray.splice(-1);
	ergebnis_float = ergebnis_single[0].toFixed(2);
	
	
	return {ergebnis_float, resultarray}
	
	
	}
	
	
	
	
	
	
	
	
	</script>
	
	<main class="container">
	  <h1>SHITTY-DICE</h1>
	 <article> 

		<div>
			{#each resultarray as element, i (element)}
<div class="element">{element}</div>
{/each}

</div>
	<div>
		<p2 id="ergebnis_float" style:text-align="center">{$progress.toFixed(2)}</p2>
	
	  <label for="range">
	  <input type="range" disabled min="0.00" max="100.00" value="{$progress}" id="range" name="range">
	</label>
</div>
	
	
	
	 
	<div id="targetnumber">
<p>_________________________________</p>
	<p>SETTINGS</p>
	  <label for="range">
		<input type="range" min="2.00" max="99.00" bind:value={targetnumber} id="rangepicker" name="rangepicker">
	  </label>
	  <p id="ergebnis_float" style:text-align="center" style:margin-right="4px">>{targetnumber} </p><p>{targetmultiplier}x {100-targetnumber}%</p>
	
	</div>
	</article>
	<article>
	
	<button id="rollbutton" on:click="{roll}" on:click="{() => progress.set(ergebnis_single[0])}">ROLL</button>
	
	</article>
	  
	</main>
	
	<style>
	

div{

text-align: center;

}	

#targetnumber {

	margin-top: 24px;


}
	  p {
	
	text-align: center;
	margin-right: 8px;
	
	  }
	
	  p2
	  {
		font-size: xx-large;
		color:aliceblue;



	  }
	</style>