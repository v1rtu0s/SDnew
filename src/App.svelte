<script>

	import { tweened } from 'svelte/motion';
		import { cubicOut } from 'svelte/easing';
		import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import  { blur } from 'svelte/transition';
	import Chart from 'chart.js/auto';
import { getRelativePosition } from 'chart.js/helpers';
import Limbo from './Limbo.svelte';
// import {limbo_roll} from './Limbo.svelte';
import Dice from './Dice.svelte';
import Mines from './Mines.svelte';
import {writable} from 'svelte/store';
import {setContext} from 'svelte';



	
	
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
	var balance_start = 100.00;
	//var $betsize = 0;
	var win_amount = 0;
	var balance_array = [];
	var nonce_array = [];
	var bet_totalamount = 0;
	export let menu = 1;
	var chart = undefined;
	var render_chart_value = false;
	var xxx = document.getElementById("ergebnis_floatp");
	var details_var = undefined;
	
	$: targetmultiplier = (100/(100-targetnumber)).toFixed(2);
	$: resultarray = resultarray;
	$: win_amount = ($betsize*targetmultiplier).toFixed(2);
	$: balance = balance;
	$: bet_totalamount = bet_totalamount;
	//$: balance_array.push(balance), console.log(balance_array);
	//$: nonce_array.push(nonce), console.log(nonce_array);

	let betsize = writable(0);
	setContext(0,betsize);
	$betsize = 0;

	const progress = tweened(0, {
			duration: 300,
		easing: cubicOut
	  
			});
	
	const balance_progress = tweened(0, {
			duration: 200,
			easing: cubicOut});
	
function autoroll() {for (var i = 0; i < bet_totalamount; i++) {


  roll();

}}

	
	function roll() {
		
		if (render_chart_value == false) { render_chart_value = true; renderChart();}
	if (bet_totalamount > 0) {autoroll()} else {	
	balance = balance-$betsize;
	balance_progress.set(balance);
	nonce++;
	nonce_array.push(nonce);
	result = (Math.random()*100).toFixed(2);
	resultarray.push(result);
	resultarray = resultarray;
	console.log(resultarray);
	console.log(nonce);
	ergebnis_float = resultarray[resultarray.length-1];
	ergebnis_single = ergebnis_float;
	console.log(ergebnis_single);
	

	evaluate_roll();

	
	}
	}

function evaluate_roll() {
	
	if (ergebnis_single >= targetnumber) {

balance = balance + ($betsize*targetmultiplier);
balance_progress.set(balance);
balance_array.push(balance);
win_state = true;
win_state_animation = true;

addData();

}

else {
balance_array.push(balance);
win_state_animation_lose = true;
win_state = false;

addData();
}}


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
		responsive: true,
		maintainAspectRatio: false,
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
	
	
	
	if (balance >= balance_start) {


		if (balance <= balance_start*1.5) {

        chart.data.datasets[0].backgroundColor="#058c00";
		chart.data.datasets[0].borderColor="#058c00";

		}
		
		else { 
		chart.data.datasets[0].backgroundColor="#33ff05";
		chart.data.datasets[0].borderColor="#33ff05";}




	}

	else {
		
		if (balance > balance_start*0.5) {
			chart.data.datasets[0].backgroundColor="#ff4000";
		    chart.data.datasets[0].borderColor="#ff4000";}
	else {
		chart.data.datasets[0].backgroundColor="#9e0000";
		    chart.data.datasets[0].borderColor="#9e0000";
		
	}
	
	}
		
		
		
	
	chart.update()
	};


	

	
	
	
	</script>
	
	<main class="container">


		<ul id="menu" style:text-align="left">
			<li><a href="/" on:click|preventDefault={() => (menu = 1)}>Dice</a></li> |
			<li><a href="/" on:click|preventDefault={() => (menu = 2)}>Limbo</a></li> |
			<li><a href="/" on:click|preventDefault={() => (menu = 3)}>Mines</a></li>
		</ul>
	<div class="parent">
		<div class="div1">
			
			
	<div class="container_balance">
 {#if win_state_animation == true }
           <div class="balance_div_win" in:fly="{{delay: 0, duration: 5, x: 0, y: 0, opacity: 0.2, easing: cubicOut}}" 
		                            out:fly="{{delay: 0, duration: 1100, x: 0, y: -50, opacity: 0.05, easing: cubicOut}}"
			                        on:introend="{() => {win_state_animation = false}}">
			             +{(($betsize*targetmultiplier)-$betsize).toFixed(2)}</div>
 {/if}

		   <div class="balance_div_mitte">$ {balance.toFixed(2)}</div>
 {#if win_state_animation_lose == true }
           <div class="balance_div_lose" in:fly="{{delay: 0, duration: 5, x: 0, y: 0, opacity: 0.2, easing: cubicOut}}"
		                             out:fly="{{delay: 0, duration: 1100, x: 0, y: 50, opacity: 0.05, easing: cubicOut}}"
			                         on:introend="{() => {win_state_animation_lose = false}}">
						-{$betsize.toFixed(2)}</div>
 {/if}
           <div class="div_links"></div>
           <div class="div_rechts"></div>	
	</div>
				
				
</div>






		
		<div class="div2">

			

	 
				
					
					
					   
					 
					<div class="divleft"><input type="number" bind:value={$betsize} style:width="100px" style:align="left"><p2>on win: {(win_amount-$betsize).toFixed(2)}  </p2><br><input type="number" style:align="left" bind:value={bet_totalamount} style:width="100px"><p2>autobet</p2></div>
					 <!-- {#if bet_totalamount > 0 }<div><button id="autorollbutton" on:click="{autoroll}" on:click="{() => progress.set(parseFloat(ergebnis_single))}">AUTOROLL</button></div> -->
					 <!-- {:else if bet_totalamount == 0 }<div><button id="rollbutton" on:click="{roll}" on:click="{() => progress.set(parseFloat(ergebnis_single))}">ROLL</button></div>{/if} -->
					 <button id="rollbutton" on:click="{roll}" on:click="{() => progress.set(parseFloat(ergebnis_single))}">ROLL</button>

		</div>

		
		<div class="div3">

			<div> 
				{#if win_state == true } <div class="cell" class:selected="{win_state}" in:blur="{{delay: 0, duration: 500, x: 0, y: 0, opacity: 0.1, easing: cubicOut}}">WIN!</div>
				{:else} <div class="cell" class:selected="{win_state}" in:blur="{{delay: 0, duration: 500, x: 0, y: 0, opacity: 0.1, easing: cubicOut}}">LOSE!</div> {/if} </div>
				
				
                
<!--RESULT BIG  -->
<div><div style:text-align="right">{#if resultarray[nonce-4] != undefined}<span class="divright" style:opacity="25%"> {resultarray[nonce-4]}</span>  <span class="divright" style:opacity="50%"> {resultarray[nonce-3]}</span>  <span class="divright" style:opacity="75%">  {resultarray[nonce-2]}</span>  <span class="divright" style:opacity="100%"> {resultarray[nonce-1]}</span>{/if}</div>
			<span class="cell" class:selected="{win_state}">{$progress.toFixed(2)}</span>
			<div>
			  <!-- <label for="range">
			  <input type="range" id="range_result" step="0.05" disabled min="0.00" max="100.00" value="{$progress}" name="range">
			</label> -->
			<progress id="progressbar" min="0.00" max="100.00" value="{$progress}" style:height="10px">{progress}</progress>
		</div>
		<label for="range">
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
			
		 <div class="parent2">
		  <div class="div7">
			<p2>Chance</p2><br>
			{100-targetnumber}% </div>
			<div class="div8"><p2>Multiplier</p2><br> {targetmultiplier}x </div>
		

		


		</div></div>

		

		<div class="div4">

	{#if menu === 1}
		<Dice />
		{:else if menu === 2}
		<Limbo /> 
		{:else if menu === 3}
		<Mines />
		
		
		
		{/if}

			
				
		        

		</div>
		<div class="div5" style:height="fit-content">
			
<div>
	<canvas id="myChart"></canvas>

</div>
			

		</div>
		
		
	
			
			
			
			
			
			
				
		
		
		
		
		
	
	
	
	 
	

	
	  
		
	
	
	
	
	
	
	
	  
	</main>
	
	<style>
	


main{

text-align: center;


}


body {

	min-height: 100%;

}

@media only screen and (prefers-color-scheme: dark) {
  :root:not([data-theme=light]) {

	--progress-background-color: #24333e !important;
  --progress-color: rgb(67, 99, 180) !important;
}  }



div{

text-align: center;
color:#f0f8ff;
font-size: large;

}	
.divright {
text-align: right;
color: #dbdbdb;


}
.divleft {

	text-align: left;
}

.display_balance {
text-align: center;
width: 250px;
height: 50px;
background-color: #151d25;


}


#targetnumber {

	margin-top: 8px;
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
grid-template-columns: 1fr repeat(2, 2fr);
grid-template-rows: 75px 400px repeat(2, 75px);
grid-column-gap: 15px;
grid-row-gap: 15px;


}

.div1 { grid-area: 1 / 1 / 2 / 4; 
	box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  background-color: #151d25;
  border-radius: 8px;
  padding: 2px;
  text-align: center;



}



.div2 { grid-area: 2 / 1 / 3 / 2; 

	box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  background-color: #151d25;
  border-radius: 8px;
padding: 1rem;
text-align: left;



}

.div3 { grid-area: 2 / 2 / 3 / 3; 

	box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  background-color: #151d25;
  border-radius: 8px;
  padding: 1rem;


}

.div4 { grid-area: 2 / 3 / 3 / 4; 

	box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  background-color: #151d25;
  border-radius: 8px;
  padding: 1rem;


}

.div5 { grid-area: 3 / 1 / 4 / 4;

	box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  background-color: #151d25;
  border-radius: 8px;
  padding: 1rem;


}



.div6 { grid-area: 4 / 1 / 5 / 4;

	box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12);
  background-color: #151d25;
  border-radius: 8px;
  padding: 1rem;


}

.parent2 {
display: grid;
grid-template-columns: repeat(2, 1fr);
grid-template-rows: 1fr;
grid-column-gap: 0px;
grid-row-gap: 0px;
}


.div9 {
position:relative;

height:22px;
text-align: center;


}


.div10_background {
width: 120px;
height: auto;
background-color: #0e1418;
margin-left: 50%;
border-radius: 6px;
box-shadow: rgba(0, 0, 0, 0.16) 0px 10px 36px 0px, rgba(0, 0, 0, 0.06) 0px 0px 0px 1px;


}
.div11 { 
	
position:relative;
margin-left: 50%;
height:18px;

}

.container_balance {  display: grid;
  grid-template-columns: 1fr 0.5fr 1fr;
  grid-template-rows: 22px 32px 22px;
  gap: 0px 0px;
  grid-auto-flow: row;
  justify-content: center;
  align-content: center;
  justify-items: center;
  align-items: center;
  grid-template-areas:
    "div_links balance_div_win div_rechts"
    "div_links balance_div_mitte div_rechts"
    "div_links balance_div_lose div_rechts";
}

.balance_div_mitte { grid-area: balance_div_mitte; }

.div_links { grid-area: div_links; }

.div_rechts { grid-area: div_rechts; }

.balance_div_win { 
    color:#72fe00;
	transition:all 0.5s;
	font-weight: lighter;


	grid-area: balance_div_win; }

.balance_div_lose { 
	color:#fc2200;
	transition:all 0.5s;
	font-weight: lighter;
	
	grid-area: balance_div_lose; }



</style>