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
	var win_state = false;
	var xxx = document.getElementById("ergebnis_floatp");
	
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
	
if (ergebnis_single >= targetnumber) {

    
	win_state = true;
	color_change_win();


}

else {
	
	win_state = false;
	color_change_lose();
}
	
	
	return {ergebnis_float, ergebnis_single, resultarray, win_state}}
	
	
//$: ergebnis_single, color_change(); 

function color_change_win() {

	
	
	//xxx.style.color = "#ffffff";
	console.log("win!") 
}


function color_change_lose() {


	//xxx.style.fontSize = "77px";
	console.log("fail!")


}	



	
	
	
	
	
	
	</script>
	
	<main class="container">
	 
	 <article> 
		<div>
	<span class="cell" class:selected="{win_state}">{$progress.toFixed(2)}
		<!-- <p2 id="ergebnis_floatp" style:text-align="center">{$progress.toFixed(2)}</p2> -->
	</span></div>
	<div>
	  <label for="range">
	  <input type="range" step="0.05" disabled min="0.00" max="100.00" value="{$progress}" id="range" name="range">
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

#ergebnis_floatp {
color: #ffffff;
transition: color 0.5s;

}
	  p {
	
	text-align: center;
	margin-right: 8px;
	
	  }
	
	  p2
	  {
		font-size: xx-large;
		color:#f0f8ff;

	  }

	  p3

	  {
color:aliceblue;
transition: color 0.5s;

	  }

	  ul li{
  display: inline;
}

span.cell {

text-align: center;
color: #f0f8ff;
font-size: 44px;
font-weight: bolder;

}
span.cell.selected {
	text-align: center;
    color: #72fe00;
    transition: color 0.5s; }
	</style>