<script lang="ts">
let ile = $state(0);
function los() {
    let a = Math.random();
    a = Math.floor((Math.random() * 10)+1)
    ile = a;
}
</script>

<nav>
<p>Strona główna</p>
</nav>
<div class="main-container">

    <h1>Medicover</h1>
    <table>
        <tbody>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </tbody>
    </table>
    <br>
    <button onclick={los}>Losuj liczbę</button>
    <p>{ile}</p>
</div>
<style>
    table, td {
        border: 1px solid black;
        border-collapse: collapse;
        padding: 10px;
    }
    nav {
        width: 100vw;
        background-color: blue;
        color: white;
        height: 7vh;
        overflow: hidden;
    }
    nav > p {
        text-align: center;
        font-family: 'Comic Sans MS';
    }
    :global(body) {
        margin: 0px;
    }
    .main-container {
        margin: 5px;
    }
</style>