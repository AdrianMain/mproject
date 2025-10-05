<script lang="ts">
import { toDataURL } from "qrcode";

let placeName = '';
let secretCode = '';
let personFullName = 'Adrian Jakubek';
let enterType = 'Wejście open';
let qrImg = '';
let clicked = false;
let leftTime = '10 min 5 sek';
//for test

function xyz(s:string) {
  return s.replace(/\b\w/g, c => c.toUpperCase());
}


function move() {
    let elem = document.getElementById("timeBar");
    let width = 100;
    let inter = setInterval(frame, 1000);
    function frame() {
        if (width <= 0) {
            clearInterval(inter);
        }
        else {
            width --;
            console.log((width/12)*10);
            elem!.style.width = ((width/12)*10) + "%";
            calcInfo(width);
        }
    }
}
function calcInfo(seconds:number) {
    let minut = 0
    while (seconds>60) {
        minut++;
        seconds-=60;
    }
    if (minut>0) {
        leftTime = String(minut + ' min ' + seconds + ' sek')
    }
    else {
        leftTime = String(seconds + ' sek')
    }
}

async function handleSubmit(event: Event) {
    event.preventDefault();
    clicked = true;
    qrImg = await toDataURL(secretCode);
    move();
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
        bind:value={placeName}
        placeholder="Nazwa ośrodka"
        required
    >
    <p>Podaj typ wejścia</p>
    <input
        name="resort type"
        type="text"
        autocomplete="on"
        bind:value={enterType}
        required
        placeholder="Typ wejścia"
    >
    <p>Podaj kod Medicover</p>
    <input
        name="code"
        type="text"
        autocomplete="off"
        bind:value={secretCode}
        placeholder="Kod Medicover"
        required
    ><br><br>
    <input
        name="personal"
        type="text"
        autocomplete="off"
        bind:value={personFullName}
        required
        placeholder="Imie Nazwisko"
    ><br><br>

    <button type="submit">Wygeneruj</button>
</form>

<!-- Prawdziwa podruba -->
{:else}
<div class="strzalka">
    <img src="arrow.svg" alt="strzałka" width="24" height="24">
</div>
<h3>{xyz(placeName)}</h3>
<div class="main">
<div class="container">
    <div class="nwm">
        <p class="poka">POKAŻ KOD QR</p>
        <p class="poka">DO ZESKANOWANIA</p>
    </div>
    <img alt="qr" src={qrImg} id="qrIMG">

    <!-- To do!!!!! -->
    <p class="jeszcze">Kod ważny jeszcze {leftTime}.</p>
    <div id='timeProgress'>
        <div id="timeBar"></div>
    </div>

    <p class="imie">{personFullName.toUpperCase()}</p>
    <p class="small-print">{enterType}</p>
</div>
</div>
{/if}

<style>
@font-face {
    font-family: Roboto;
    src: url('roboto-font.ttf');
}
@font-face {
    src: url('pixel-font.ttf');
    font-family: Pixel;
}

:global(body) {
    background-color: #111111;
    color: white;
    font-family: Roboto, Pixel;
    font-weight: bold;
    margin: 0;
} 
h3 {
    text-align: center;
    margin-top: 1.5vh;
    font-size: 17px;
}
.main{
    width: 100%;
    display: flex;
    justify-content: center;
}
.container {
    background-color: #36353A;
    width: 80vw;
    padding: 0.5vh 5vw;
    border-radius: 8px;
    margin-top: 2vh;
    display: flex;
    align-items: center;
    flex-direction: column;
}
.nwm {
    margin-top: 0.5vh;
}
.poka {
    line-height: 0.5;
    text-align: center;
}
#qrIMG {
    width: 55vw;
    height: 55vw;
}
.jeszcze {
    margin-top: 3vh;
    font-size: 12px;
    color: #78e710;
}
#timeProgress {
    margin-top: -0.5vh;
    width: 70vw;
    background-color: grey;
    border-radius: 10px;
}
#timeBar {
    width: 83%;/*for start position of timer*/
    height: 1vh;
    border-radius: 10px;
    background-color: #78e710;
}
.imie {
    margin-top: 5vh;
    margin-bottom: 0.5vh;
}
.small-print {
    margin-bottom: 2vh;
    margin-top: 0;
    font-size: 10px;
    font-weight: 400;
}
.strzalka {
    position: absolute;
    top: 5px;
    left: 5px;
    width: 35px;
    height: 35px;
    border-radius: 35px;
    background-color: white;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>