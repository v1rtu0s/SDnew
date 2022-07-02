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
	$: resultarray = resultarray;
	
	const progress = tweened(0, {
			duration: 300,
		easing: cubicOut
	  
			});
	
	const progress_string = tweened("abc", {
			duration: 400,
			easing: cubicOut});
	
	
	
	function roll() {
	nonce++;
	result = (Math.random()*100).toFixed(2);
	
	resultarray.push(result);
	console.log(resultarray);
	console.log(nonce);

	ergebnis_float = resultarray[resultarray.length-1];
	ergebnis_single = ergebnis_float;
	console.log(ergebnis_single);
	

	
	return {ergebnis_float, ergebnis_single, resultarray}
	
	
	}
	
	
	
	
	
	
	
	
	</script>
	
	<main class="container">
	 
	 <article> 
		<div>

			<ul>
				{#each resultarray as ergebnisse}
					<li>{ergebnisse}</li>
				{/each}
			</ul>
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
	
	<button id="rollbutton" on:click="{roll}" on:click="{() => progress.set(parseFloat(ergebnis_single))}">ROLL</button>
	
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

	  ul li{
  display: inline;
}
	</style>