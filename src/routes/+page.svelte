<script>
    let cells = [0,1,2,3,4,5,6,7,8];
    let winningCombos = [[0,1,2], [3,4,5], [6,7,8,], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
    let turn = false;
    let playerOneColour = "#7a2048";
    let playerTwoColour = "#1e2761"
    let cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
    let playerOneCells = [];
    let playerTwoCells = [];

    function change(cell){
        if(cellColours[cell] == "white"){
            if(turn == false){
                cellColours[cell] = playerOneColour;
                playerOneCells.push(cell);
                console.log(playerOneCells);
                turn = true;
            }else{
                cellColours[cell] = playerTwoColour;
                playerTwoCells.push(cell)
                console.log(playerTwoCells);
                turn = false;
            }
        }
    }
    function clear(){
        cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
    }
    $: {
        let winPoints = 0;
        for(let i = 0; i < 3; i++){
            if(playerOneCells.includes(winningCombos[0][i])){
                winPoints ++;
                console.log("win points:" + winPoints);
            }
            if(winPoints == 3){
                console.log("you won!");
            }
        }
        winPoints = 0;
    }
</script>

<title>Tic Tac Toe</title>
<h1>Tic Tac Toe</h1>
{#if turn == false}
    <h2 style="color:{playerOneColour};">Player One's Turn</h2>
{:else}
    <h2 style="color:{playerTwoColour};">Player Two's Turn</h2>
{/if}
<button on:click={clear}>Clear</button>
<div class="board">
    {#each cells as cell}
        <div id={cell} on:click={() => change(cell)} style="background-color:{cellColours[cell]}"></div>
    {/each}
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