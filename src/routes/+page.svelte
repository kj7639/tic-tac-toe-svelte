<script>
    let cells = [0,1,2,3,4,5,6,7,8];
    let turn = false;
    let playerOneColour = "#7a2048";
    let playerTwoColour = "#1e2761"
    let cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
    
    function change(cell){
        if(turn == false){
            cellColours[cell] = playerOneColour;
            turn = true;
        }else{
            cellColours[cell] = playerTwoColour;
            turn = false;
        }
    }
    function clear(){
        cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
    }
</script>

<title>Tic Tac Toe</title>
<h1>Tic Tac Toe</h1>
<button on:click={clear}>Clear</button>
<div class="board">
    {#each cells as cell}
        <div id={cell} on:click={() => change(cell)} style="background-color:{cellColours[cell]}"></div>
    {/each}
    <!-- <div id="1" on:click={() => change(1)} style="background-color:{playerOneColor};"></div>
    <div id="2" on:click={() => change(2)}></div>
    <div id="3" on:click={() => change(3)}></div>
    <div id="4" on:click={() => change(4)}></div>
    <div id="5" on:click={() => change(5)}></div>
    <div id="6" on:click={() => change(6)}></div>
    <div id="7" on:click={() => change(7)}></div>
    <div id="8" on:click={() => change(8)}></div>
    <div id="9" on:click={() => change(9)}></div> -->
</div>

<style>
    * {
        text-align: center;
    }
    .board > div {
        border: 2px solid black;
    }
    .board {
        display: grid;
        grid-gap: 10px;
        grid-template-columns: repeat(3, 150px);
        grid-template-rows: repeat(3, 150px);
        justify-content: center;
    }
</style>