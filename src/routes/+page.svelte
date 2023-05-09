<script>
    let cells = [0,1,2,3,4,5,6,7,8];
    let winningCombos = [[0,1,2], [3,4,5], [6,7,8,], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
    let turn = false;
    let playerOneColour = "#500472";
    let playerTwoColour = "#30c7a4";
    let cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
    let playerOneCells = [];
    let playerTwoCells = [];
    let playerOneScore = 0;
    let playerTwoScore = 0;

    function change(cell){
        if(cellColours[cell] == "white"){
            if(turn == false){
                cellColours[cell] = playerOneColour;
                playerOneCells.push(cell);
                turn = true;
            }else{
                cellColours[cell] = playerTwoColour;
                playerTwoCells.push(cell)
                turn = false;
            }
        }
    }
    function clear(button){
        cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
        playerOneCells = [];
        playerTwoCells = [];
        if(button != null){
            playerOneScore = 0;
            playerTwoScore = 0;
        }
    }
    function checkWin(playerCells){
        let points = 0;
        for(let f = 0; f < winningCombos.length; f++){
            for(let x = 0; x <= playerCells.length; x++){
                for(let a = 0; a <= 3; a++){
                    if(playerCells.includes(winningCombos[f][a]) == true){
                        points ++
                    }
                    if(points == 3){
                        if(playerCells == playerOneCells){
                            playerOneScore++;
                        }else if(playerCells == playerTwoCells){
                            playerTwoScore++;
                        }
                        clear();
                    }
                }
                points = 0;
            }
        }
    }
    $: {
        if(cellColours.includes("white") == false){
            clear()
        }
        if(turn == true){
            checkWin(playerOneCells);
        }else{
            checkWin(playerTwoCells);
        }
    }
</script>

<svelte:head>
    <link rel="stylesheet" href="/src/style.css">
</svelte:head>

<title>Tic Tac Toe</title>
<h1>Tic Tac Toe</h1>
{#if turn == false}
    <h2 style="color:{playerOneColour};">Player One's Turn</h2>
{:else}
    <h2 style="color:{playerTwoColour};">Player Two's Turn</h2>
{/if}
<!-- <input type="color" bind:value={playerOneColour}> -->
<button on:click={() => clear(":)")}>Clear</button>
<div class="scores">
    <h3 style="color:{playerOneColour}">{playerOneScore}</h3>
    <h3 style="color:{playerTwoColour}">{playerTwoScore}</h3>
</div>
<div class="board">
    {#each cells as cell}
        <div id={cell} on:click={() => change(cell)} style="background-color:{cellColours[cell]}"></div>
    {/each}
</div>
