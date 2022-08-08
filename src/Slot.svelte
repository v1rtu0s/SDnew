



<script>

import { draw, fade } from 'svelte/transition';
import { bounceOut, cubicOut } from 'svelte/easing';
import { fly } from 'svelte/transition';
		import { blur } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
import { onMount } from 'svelte';
	
    $: rng = rng;
    $: rng2 = rng2;
    $: rng3 = rng3;

    $: spin_end_class = spin_end_class;
    $: spin_end_class2 = spin_end_class2;
   


    
    const Bing = '/Bing.png';
    
    const Calculator = "/Calculator.png";
  
    const Access = "/Access.png";

    const graphic_array = [Bing, Calculator, Access];
    const graphic_array2 = [Bing, Calculator, Access];

var interval_duration = 250;

    var blur_function = false;
    var blur_function2 = false;


var spin_end_class = false;
var spin_end_class2 = false;

var graphic = "";
var graphic2 = "";

var k = undefined;

var interval = undefined;
var interval = undefined;

var i = 0;
var i2 = 0;

    var rng = undefined;
    var rng2 = undefined;
    var rng3 = undefined;
var interval_duration = 200;

  onMount(() => {k = document.getElementById("K");});



function generateRandomIntegerInRange(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

function spin() {

console.log("spin");
interval = setInterval(rngfunction, interval_duration);
}
function spin2() {

console.log("spin");
interval = setInterval(rngfunction2, interval_duration);
}
function spin3() {

console.log("spin");
interval = setInterval(rngfunction3, interval_duration);
}

///////////////////////////////////////////// REEL 1

function rngfunction() {
    blur_function = true;
spin_end_class = false;
    i++;
    rng = generateRandomIntegerInRange(1, 3);
 
    

    if (rng == 1) {

        graphic = graphic_array[0];

}

else if (rng == 2) {
   
    graphic = graphic_array[1];

}

else if (rng == 3) {
    
    graphic = graphic_array[2];
    

}


    if (i > Math.random()*10+5) {
        clearInterval(interval);
    i = 0;
    spin_end_class = true;
    blur_function = false; 
   
    };}

///////////////////////////////////////////// REEL 2

function rngfunction2() {
    blur_function2 = true;
spin_end_class2 = false;
    i2++;
    
    rng2 = generateRandomIntegerInRange(1, 3);
    
    

    if (rng2 == 1) {

        graphic2 = graphic_array2[0];

}

else if (rng2 == 2) {
   
    graphic2 = graphic_array2[1];

}

else if (rng2 == 3) {
    
    graphic2 = graphic_array2[2];
    

}


    if (i2 > Math.random()*10+5) {
        clearInterval(interval2);
    i2 = 0;
    spin_end_class2 = true;
    blur_function2 = false; 
  
    };


}


</script>

<!-- HTML -->
<main>

    <div id="app">
        <div class="doors">
          <div class="door"  class:spin_end_class={spin_end_class}>
            <div class="box" >
             

{#key graphic}
<div id="K" class:blur={blur_function} in:fly="{{delay: 0, duration: 300, x: 0, y: -50, easing: bounceOut}}"><img src={graphic} class:blur={blur_function} alt=""></div>
 {/key}
          
          </div></div>
      
          <div class="door" class:spin_end_class={spin_end_class2}>
            <div class="box">
                {#key graphic2}
<div id="K" class:blur={blur_function} in:fly="{{delay: 0, duration: 300, x: 0, y: -50, easing: bounceOut}}"><img src={graphic2} class:blur={blur_function2} alt=""></div>
 {/key}
                
              <!-- <div class="box">?</div> -->
            </div>
          </div>
      
          <div class="door" class:spin_end_class={spin_end_class}>
            <div class="box">
                {#key graphic}
<div id="K" class:blur={blur_function} in:fly="{{delay: 0, duration: 300, x: 0, y: -50, easing: bounceOut}}"><img src={graphic} class:blur={blur_function} alt=""></div>
 {/key}
              <!-- <div class="box">?</div> -->
            </div>
          </div>
        </div>
      
        <div class="buttons">
          <button id="spinner" on:click={spin} on:click={spin2} on:click={spin3}>Play</button>
          <button id="reseter">Reset</button>
        </div>
      </div>


</main>

<style>

body {
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
}

.door.spin_end_class {
    background-color: #0c303d;
    

    border: 3px solid #ffffff;
transition: all 0.4s ease-in-out;



}

.doors {
  display: flex;
}

.door {
  
  width: 100px;
  height: 110px;
  overflow: hidden;
  border-radius: 5px;
  margin: 5px;
  border: 3px solid #7a7a7a;
  
  align-items: center;
  padding: 4px;
  transition: all 0.2s;
}

.boxes {

}

.box {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3rem;
  color: aliceblue;
  
  
}


#K {

    
}

.blur {

filter:blur(3px);
transition: all 0.1s;

}

#S {

}
#A {


}










</style>