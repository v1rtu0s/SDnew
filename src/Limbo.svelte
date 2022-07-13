<script>

var result_limbo = 0;
var result_limbo_consoli = 0;

export function limbo_roll(){

    result_limbo = 1000000/(Math.random()*1000000);
    result_limbo_consoli = Math.floor(result_limbo*100)/100
    console.log(result_limbo_consoli);




}


</script>

<main>

<div><button on:click={limbo_roll}>TEST</button></div>

</main>


<style>



</style>