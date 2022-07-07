<script>

	import { tweened } from 'svelte/motion';
		import { cubicOut } from 'svelte/easing';
		import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import  { blur } from 'svelte/transition';
	import Chart from 'chart.js/auto';
import { getRelativePosition } from 'chart.js/helpers';


	
	
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
	var win_state_animation_lose = false;
	var balance = 100.00;
	var betsize = 0;
	var win_amount = 0;
	var balance_array = [];
	var nonce_array = [];
	var chart = undefined;
	var xxx = document.getElementById("ergebnis_floatp");
	var details_var = undefined;
	
	$: targetmultiplier = (100/(100-targetnumber)).toFixed(2);
	$: resultarray = resultarray;
	$: win_amount = (betsize*targetmultiplier).toFixed(2);
	$: balance = balance;
	//$: balance_array.push(balance), console.log(balance_array);
	//$: nonce_array.push(nonce), console.log(nonce_array);
	

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
	nonce_array.push(nonce);
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
	balance_array.push(balance);
	win_state = true;
	win_state_animation = true;
	color_change_win();
addData();

}

else {
	balance_array.push(balance);
	win_state_animation_lose = true;
	win_state = false;
	color_change_lose();
	addData();
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

function renderChart() {
var ctx = document.getElementById("myChart").getContext("2d");
  chart = new Chart(ctx, {
      type: "line",
      data: {
        labels: nonce_array,
        datasets: [
          {
            label: "Balance",
            backgroundColor: "rgb(255, 99, 132)",
            borderColor: "rgb(255, 99, 132)",
            data: balance_array
          }
        ]
      },
      options: {
		animations: {
x: {duration: 650},
y: {duration: 0},
easing: 'easeOutCubic',
		},
		transitions: {
easing: 'easeOutCubic',
duration: 150,

		}
		
    }})}
  


function addData() {
	chart.data.datasets.data = balance_array;
	chart.data.labels = nonce_array;
	if (balance > balance_array[0]) {
		
		chart.data.datasets[0].backgroundColor="#33ff05";
		chart.data.datasets[0].borderColor="#33ff05";
	}

	else {chart.data.datasets[0].backgroundColor="#ff4000";
		chart.data.datasets[0].borderColor="#ff4000";}
	
	chart.update()
	};


	
	
	
	
	
	</script>
	
	<main class="container">
	 
	 <article>
		<header>
			
			<div class="parent2">
				<div class="div4">{#if win_state_animation_lose == true }<span class="balance_lose" transition:blur="{{duration:350, easing: cubicOut,amount: 5,delay:0}}"
			on:introend="{() => {win_state_animation_lose = false}}">-{betsize.toFixed(2)}</span>{/if}</div>
				<div class="div5"><span class="balance">$ {balance.toFixed(2)}</span></div>
				<div class="div6">{#if win_state_animation == true }<span class="balance_win" transition:blur="{{duration:350, easing: cubicOut,amount: 5,delay:0}}"
			on:introend="{() => {win_state_animation = false}}"
				
				>+{((betsize*targetmultiplier)-betsize).toFixed(2)}</span>
				{/if}
</div>
			
			
			
			
			
			
				
		
		
		
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
	  <input type="range" id="range_result" step="0.05" disabled min="0.00" max="100.00" value="{$progress}" name="range">
	</label>
</div>
	
	
	
	 
	<div id="targetnumber">

	 
	<details id="settings">
		<!-- svelte-ignore a11y-no-redundant-roles -->
		<summary class="secondary" style:text-align="left" style:font-size="26px">SETTINGS</summary>
		
		
		   <div class="parent">
		<div class="div1"> <label for="range">
		<input type="range" min="2.00" max="99.00" list="ticks" bind:value={targetnumber} id="rangepicker" name="rangepicker" style:margin-bottom="1px">
	  </label>
	  
	  <datalist id="ticks">
<option value="0">0</option>
<option value="25">25</option>
<option value="50">50</option>
<option value="75">75</option>
<option value="100">100</option>
	  </datalist>
	  <p3 id="ergebnis_float" style:text-align="center" style:margin-top="1px">>{targetnumber} </p3> </div>
		<div class="div2">{100-targetnumber}% </div>
		<div class="div3"> {targetmultiplier}x </div>
		</div>
	  </details>

	
	  <footer>
		<input type="number" bind:value={betsize} style:width="75px"><p2>on win: {(win_amount-betsize).toFixed(2)}</p2>

		<button id="rollbutton" on:click="{roll}" on:click="{() => progress.set(parseFloat(ergebnis_single))}">ROLL</button></footer>
	
	
	</article>
	<article>
	
		<details id="details">
			<!-- svelte-ignore a11y-no-redundant-roles -->
			<summary role="button" on:click="{renderChart}">Chart</summary>
			
			<div>
				<canvas id="myChart"></canvas>
			</div>
			 
		  </details>
		  
		  
	
	
	</article>
	  
	</main>
	
	<style>
	


main{

text-align: center;
margin-top: -82px;

}


#range_result{}




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
	position: absolute;
font-size: 22px;
font-weight: lighter ;
color:#33ff05;

}

span.balance_lose {
	position: absolute;
font-size: 22px;
font-weight: lighter ;
color:#ff2f05;

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

.parent2 {
display: grid;
grid-template-columns: (1fr, 0.25fr, 1fr);
grid-template-rows: 0.5fr;
grid-column-gap: 0px;
grid-row-gap: 0px;
}
.div4 { grid-area: 1 / 1 / 2 / 2;text-align: right; }
.div5 { grid-area: 1 / 2 / 2 / 3;text-align: center; }
.div6 { grid-area: 1 / 3 / 2 / 4;text-align: left; }
	</style>