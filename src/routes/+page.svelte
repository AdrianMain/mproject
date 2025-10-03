<script lang="ts">
let a = $state('');
let b = $state('');
let clicked = $state(false);
function hello() {
    clicked = true;
};
</script>

{#if !clicked}
<h2>Witaj użytowniku Medicover</h2>
<form action="" name="f">
    <p>Podaj nazwę ośrodka np nazwa siłowni</p>
    <input type="text" name="sport" autocomplete="on" bind:value={a}>
    <p>Podaj kod Medicover</p>
    <input type="text" name="code" autocomplete="on" bind:value={b}>
    <input type="submit" onclick={hello}>
    
</form>
{:else}
<h1>{a}</h1>
<p>{b}</p>
{/if}


<style>
</style>