<script>
	import {setContext} from 'svelte';
	import {writable} from 'svelte/store';
    import {getContext} from 'svelte';

	var mines_amount = 3;
	var mines_array = [];
	var mines_set = new Set();
	var active_bet = false;
	var mines_classes = undefined;
    var boom_state = new Array(25);
    var passed = new Array(25);
    var mines_payout_multiplier = 0;
    var passed_mutiplier = 0;
    
    let betsize = getContext(0);  
    
	boom_state.fill(undefined);
    
  

  function ncr(n,r) { 
return Math.floor(factorialize(n))/Math.floor(factorialize(r))/Math.floor(factorialize(n-r))};

  function factorialize(num) {
  if (num < 0) 
        return -1;
  else if (num == 0) 
      return 1;
  else {
      return (num * factorialize(num - 1));
  }
}

$: mines_payout_multiplier = ncr(25, passed_mutiplier)/ncr(25-mines_amount, passed_mutiplier);
	

function press() {
		
        if (active_bet == true) {
	
        var mines_int = parseInt(this.id);
        var mines_array = Array.from(mines_set);
        if (mines_array.includes(mines_int) == true) {
            passed[mines_int] = false; 
            
            
            active_bet = false; 
            
            for (var i = 0; i < mines_array.length; i++)
           
            {boom_state[mines_array[i]-1] = true}
            
            //console.log(mines_int, "BOOM")
        }
        else {
            passed_mutiplier++;
            passed[mines_int] = true;
            boom_state[mines_int] = false;
             //console.log(boom_state[mines_int]); 
             //console.log(mines_int, "=safe")
            };

        } else {console.log("no active game")}
		
	}
	
	function start_bet(){

        if (active_bet == false)
         {
            boom_state.fill(undefined);
		active_bet = true;
        passed_mutiplier = 0;
        passed = new Array(25);
        mines_set = new Set();
		while (mines_set.size < mines_amount) {
		
			
		mines_set.add(Math.floor(Math.random() * (25 - 1 + 1) + 1));
			console.log(mines_set.size);
			console.log(mines_set);	
		                                      }
		
		 }
        else {console.log("there is an active game")}
    }
		 
		
	function pay_out() {console.log({$betsize});}
	
	
	
</script>

<main>{#if active_bet == false}
             <button class="button" id="start_bet" on:click="{start_bet}">BET</button>
      {:else}<button class="button" id="pay_out" on:click="{pay_out}">TAKE {(mines_payout_multiplier*$betsize).toFixed(2)} | {mines_payout_multiplier.toFixed(2)}x</button> {/if}
	

<input type="range" min="1" max="20" bind:value={mines_amount} style:margin-bottom="1px"><p>{mines_amount} mines</p>

<div class="parent">
<div class="div1"><button class="field"  class:selected={active_bet}  id="1" class:boomboom={boom_state[0]} class:passanimation={passed[1]} on:click="{press}">1</button></div>
<div class="div2"><button class="field" class:selected={active_bet}   id="2" class:boomboom={boom_state[1]} class:passanimation={passed[2]} on:click="{press}">2</button> </div>
<div class="div3"><button class="field" class:selected={active_bet}   id="3" class:boomboom={boom_state[2]} class:passanimation={passed[3]} on:click="{press}">3</button> </div>
<div class="div4"><button class="field" class:selected={active_bet}  id="4"  class:boomboom={boom_state[3]} class:passanimation={passed[4]} on:click="{press}">4</button> </div>
<div class="div5"><button class="field" class:selected={active_bet}  id="5"  class:boomboom={boom_state[4]} class:passanimation={passed[5]} on:click="{press}">5</button> </div>
<div class="div6"><button class="field"  class:selected={active_bet} id="6"  class:boomboom={boom_state[5]} class:passanimation={passed[6]} on:click="{press}">6</button> </div>
<div class="div7"><button class="field"  class:selected={active_bet} id="7"  class:boomboom={boom_state[6]} class:passanimation={passed[7]} on:click="{press}">7</button> </div>
<div class="div8"><button class="field" class:selected={active_bet}  id="8"  class:boomboom={boom_state[7]} class:passanimation={passed[8]} on:click="{press}">8</button> </div>
<div class="div9"> <button class="field" class:selected={active_bet}  id="9"  class:boomboom={boom_state[8]} class:passanimation={passed[9]} on:click="{press}">9</button></div>
<div class="div10"><button class="field" class:selected={active_bet}  id="10"  class:boomboom={boom_state[9]} class:passanimation={passed[10]} on:click="{press}">10</button> </div>
<div class="div11"><button class="field" class:selected={active_bet}  id="11"  class:boomboom={boom_state[10]} class:passanimation={passed[11]} on:click="{press}">11</button> </div>
<div class="div12"><button class="field" class:selected={active_bet}  id="12"  class:boomboom={boom_state[11]} class:passanimation={passed[12]} on:click="{press}">12</button> </div>
<div class="div13"><button class="field" class:selected={active_bet}  id="13"  class:boomboom={boom_state[12]} class:passanimation={passed[13]} on:click="{press}">13</button> </div>
<div class="div14"><button class="field" class:selected={active_bet}  id="14"  class:boomboom={boom_state[13]} class:passanimation={passed[14]} on:click="{press}">14</button> </div>
<div class="div15"><button class="field" class:selected={active_bet}  id="15"  class:boomboom={boom_state[14]} class:passanimation={passed[15]} on:click="{press}">15</button> </div>
<div class="div16"><button class="field" class:selected={active_bet}  id="16"  class:boomboom={boom_state[15]} class:passanimation={passed[16]} on:click="{press}">16</button> </div>
<div class="div17"><button class="field" class:selected={active_bet}  id="17" class:boomboom={boom_state[16]} class:passanimation={passed[17]} on:click="{press}">17</button> </div>
<div class="div18"><button class="field" class:selected={active_bet}  id="18" class:boomboom={boom_state[17]} class:passanimation={passed[18]} on:click="{press}">18</button> </div>
<div class="div19"><button class="field" class:selected={active_bet}  id="19" class:boomboom={boom_state[18]} class:passanimation={passed[19]} on:click="{press}">19</button> </div>
<div class="div20"><button class="field" class:selected={active_bet}  id="20" class:boomboom={boom_state[19]} class:passanimation={passed[20]} on:click="{press}">20</button> </div>
<div class="div21"><button class="field" class:selected={active_bet}  id="21" class:boomboom={boom_state[20]} class:passanimation={passed[21]} on:click="{press}">21</button> </div>
<div class="div22"><button class="field" class:selected={active_bet}  id="22" class:boomboom={boom_state[21]} class:passanimation={passed[22]} on:click="{press}">22</button> </div>
<div class="div23"><button class="field" class:selected={active_bet}  id="23" class:boomboom={boom_state[22]} class:passanimation={passed[23]} on:click="{press}">23</button> </div>
<div class="div24"><button class="field" class:selected={active_bet}  id="24" class:boomboom={boom_state[23]} class:passanimation={passed[24]} on:click="{press}">24</button> </div>
<div class="div25"><button class="field" class:selected={active_bet}  id="25" class:boomboom={boom_state[24]} class:passanimation={passed[25]} on:click="{press}">25</button> </div>
</div>
</main>
<style>

    p {

color: #d5d5d5;
opacity: 100%;
margin-top: 1px;


    }

.parent {
display: grid;
grid-template-columns: repeat(5, 0.2fr);
grid-template-rows: repeat(5, 0.2fr);
grid-column-gap: 3px;
grid-row-gap: 3px;
}

.div1 { grid-area: 1 / 1 / 2 / 2; }
.div2 { grid-area: 1 / 2 / 2 / 3; }
.div3 { grid-area: 1 / 3 / 2 / 4; }
.div4 { grid-area: 1 / 4 / 2 / 5; }
.div5 { grid-area: 1 / 5 / 2 / 6; }
.div6 { grid-area: 2 / 1 / 3 / 2; }
.div7 { grid-area: 2 / 2 / 3 / 3; }
.div8 { grid-area: 2 / 3 / 3 / 4; }
.div9 { grid-area: 2 / 4 / 3 / 5; }
.div10 { grid-area: 2 / 5 / 3 / 6; }
.div11 { grid-area: 3 / 1 / 4 / 2; }
.div12 { grid-area: 3 / 2 / 4 / 3; }
.div13 { grid-area: 3 / 3 / 4 / 4; }
.div14 { grid-area: 3 / 4 / 4 / 5; }
.div15 { grid-area: 3 / 5 / 4 / 6; }
.div16 { grid-area: 4 / 1 / 5 / 2; }
.div17 { grid-area: 4 / 2 / 5 / 3; }
.div18 { grid-area: 4 / 3 / 5 / 4; }
.div19 { grid-area: 4 / 4 / 5 / 5; }
.div20 { grid-area: 4 / 5 / 5 / 6; }
.div21 { grid-area: 5 / 1 / 6 / 2; }
.div22 { grid-area: 5 / 2 / 6 / 3; }
.div23 { grid-area: 5 / 3 / 6 / 4; }
.div24 { grid-area: 5 / 4 / 6 / 5; }
.div25 { grid-area: 5 / 5 / 6 / 6; }

.field.selected:hover {
 background:rgb(94, 145, 234);
}
	.field {
        background: transparent;
        border-color:#1f2f47;
  border-top-left-radius:7px;
  border-top-right-radius:7px;
  border-bottom-left-radius:7px;
  border-bottom-right-radius:7px;
  box-shadow:inset 0px 0px 15px -4px #16233a;
    width: 100%;
	height: 100%;
    transition: all 0.5s;
      
	}
	
		.field.selected {
            
            background:rgba(67, 109, 179, 1);
            border-color:#1f2f47;
  border-top-left-radius:7px;
  border-top-right-radius:7px;
  border-bottom-left-radius:7px;
  border-bottom-right-radius:7px;
  box-shadow:inset 0px 0px 8px -4px #18263e;
 
  
    
    width: 100%;
		height: 100%;
        transition: all 0.5s; 
	}
	
    .field.selected.passanimation {
        box-shadow:none;
		background-color: #00c61a;
        display: inline-block;
        width: 100%;
		height: 100%;
        animation: myAnim 0.2s cubic-bezier(0.32, 0, 0.67, 0) 0s 1 normal forwards;


    }


    .field.boomboom {
		background-color: #e42a00;
        display: inline-block;
        width: 100%;
		height: 100%;
        animation: myAnim2 0.2s cubic-bezier(0.32, 0, 0.67, 0) 0s 1 normal forwards;


    }
    @keyframes myAnim {
	0% {
		transform: scale(0);
	}

	100% {
		transform: scale(1);
	}
}

@keyframes myAnim2 {
	0% {
		transform: scale(0);
	}

	100% {
		transform: scale(1);
	}
}


</style>