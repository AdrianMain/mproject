<script lang="ts">
import { toDataURL } from "qrcode";

let a = '';
let b = '';
let qrImg = '';
let clicked = false;

async function handleSubmit(event: Event) {
    event.preventDefault();
    clicked = true;
    qrImg = await toDataURL(b);
}
</script>

{#if !clicked}
<h2>Witaj użytkowniku Medicover</h2>
<form on:submit={handleSubmit} autocomplete="on" name="medicoverForm">
    <p>Podaj nazwę ośrodka (np. nazwa siłowni)</p>
    <input
        name="sport"
        type="text"
        autocomplete="on"
        bind:value={a}
        placeholder="Nazwa ośrodka"
        required
    >

    <p>Podaj kod Medicover</p>
    <input
        name="code"
        type="text"
        autocomplete="off"
        bind:value={b}
        placeholder="Kod Medicover"
        required
    >

    <button type="submit">Wygeneruj</button>
</form>
{:else}
<h1>{a}</h1>
<p>{b}</p>
<img alt="qr" src={qrImg} id="qrIMG">
{/if}
