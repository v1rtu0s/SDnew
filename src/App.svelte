<script>

	import { tweened } from 'svelte/motion';
		import { cubicOut } from 'svelte/easing';
		import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import  { blur } from 'svelte/transition';
	
	
	var result = 0;
	var resultarray = [];
	var ergebnis_single = [];
	var ergebnis_float = 0;
	var nonce = 0;
	var targetnumber = 50;
	var test = "xyz";
	var targetmultiplier = "2";
	var win_state = false;
	var win_state_animation = false;
	var balance = 100.00;
	var betsize = 0;
	var win_amount = 0;
	var xxx = document.getElementById("ergebnis_floatp");
	
	$: targetmultiplier = (100/(100-targetnumber)).toFixed(2);
	$: resultarray = resultarray;
	$: win_amount = (betsize*targetmultiplier).toFixed(2);
	$: balance = balance;
	

	const progress = tweened(0, {
			duration: 300,
		easing: cubicOut
	  
			});
	
	const balance_progress = tweened(0, {
			duration: 200,
			easing: cubicOut});
	
	
	
	function roll() {
		balance = balance-betsize;
		balance_progress.set(balance);
	nonce++;
	result = (Math.random()*100).toFixed(2);
	
	resultarray.push(result);
	console.log(resultarray);
	console.log(nonce);

	ergebnis_float = resultarray[resultarray.length-1];
	ergebnis_single = ergebnis_float;
	console.log(ergebnis_single);
	
if (ergebnis_single >= targetnumber) {

    balance = balance + (betsize*targetmultiplier);
	balance_progress.set(balance);
	win_state = true;
	win_state_animation = true;
	color_change_win();


}

else {
	
	win_state = false;
	color_change_lose();
}
	
	
	return {ergebnis_float, ergebnis_single, resultarray, win_state}}
	
	
//$: ergebnis_single, color_change(); 

function color_change_win() {

	

	//document.body.style.backgroundColor = "#72fe00";
	//xxx.style.color = "#ffffff";
	console.log("win!") 
}

// function blur_inandout(node, { duration }) {
// 		return {
// 			duration,
// 			css: timer => {
// 				return `
//           blur: rotateZ(${timer * 360}deg);
//           transform-origin: center center;
// 					color: rgb(
//             ${100 * timer},
//             ${100 * timer},
//             ${100 * timer}
// 					);`
// 			}
// 		};
// 	}
function color_change_lose() {

	//document.body.style.backgroundColor = "#000000";
	//xxx.style.fontSize = "77px";
	console.log("fail!")


}	



	
	
	
	
	
	
	</script>
	
	<main class="container">
	 
	 <article>
		<header><span class="balance">$ {balance.toFixed(2)}</span>
			{#if win_state_animation == true }<span class="balance_win" class:selected="{win_state}" transition:blur="{{duration:350, easing: cubicOut,amount: 5,delay:0}}"
			on:introend="{() => {win_state_animation = false}}"
				
				>+{((betsize*targetmultiplier)-betsize).toFixed(2)}</span>{/if}
		
		
		
		</header>
		<div> 
		{#if win_state == true } <div class="cell" class:selected="{win_state}" in:fly="{{delay: 0, duration: 250, x: 0, y: -500, opacity: 1, easing: cubicOut}}">WIN!</div>
		{:else} <div class="cell" class:selected="{win_state}" in:fly="{{delay: 0, duration: 300, x: 0, y: 250, opacity: 1, easing: cubicOut}}">LOSE!</div> {/if} </div>
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
	 
	  
	  <div class="parent">
		<div class="div1"> <label for="range">
		<input type="range" min="2.00" max="99.00" bind:value={targetnumber} id="rangepicker" name="rangepicker" style:margin-bottom="1px">
	  </label>
	  <p3 id="ergebnis_float" style:text-align="center" style:margin-top="1px">>{targetnumber} </p3> </div>
		<div class="div2">{100-targetnumber}% </div>
		<div class="div3"> {targetmultiplier}x </div>
		</div>
	  <footer>
		<input type="number" bind:value={betsize} style:width="350px"><p2>on win: {(win_amount-betsize).toFixed(2)}</p2>

		<button id="rollbutton" on:click="{roll}" on:click="{() => progress.set(parseFloat(ergebnis_single))}">ROLL</button></footer>
	
	
	</article>
	<article>
	

	
	
	</article>
	  
	</main>
	
	<style>
	


body{

text-align: center;

}

div{

text-align: center;
color:#f0f8ff;
font-size: large;

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
		
		color:#474747;
		margin-left: 8px;

	  }

	  p3

	  {
color:aliceblue;
font-size: 18px;
font-weight: bold;

	  }

	  ul li{
  display: inline;
}
div.cell{
color:#f0f8ff;


}
span.cell {

text-align: center;
color: #ff4000;
font-size: 44px;
font-weight: bolder;
}
span.balance {
text-align: left;
color:#dbdbdb;
font-size: 32px;
font-weight: lighter ;

}

span.balance_win {
font-size: 20px;
font-weight: lighter ;
color:#33ff05;

}
span.icon {

	
	opacity: 0.25;
	color: black;
	font-weight: bolder;
	font-size: 62px;
	font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

span.cell.selected {
	text-align: center;
    color: #72fe00;
    transition: color 0.5s; }

div.cell {

	color: #ff4000;

}

div.cell.selected {

	color: #72fe00;
    transition: color 0.5s;
}

.parent {
display: grid;
grid-template-columns: repeat(2, 1fr);
grid-template-rows: repeat(2, 1fr);
grid-column-gap: 5px;
grid-row-gap: 5px;
}

.div1 { grid-area: 1 / 1 / 2 / 3; }
.div2 { grid-area: 2 / 1 / 3 / 2; }
.div3 { grid-area: 2 / 2 / 3 / 3; }



	</style>