<script>
    let cells = [0,1,2,3,4,5,6,7,8];
    let winningCombos = [[0,1,2], [3,4,5], [6,7,8,], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
    let turn = false;
    let playerOneColour = "#7203a5";
    let playerTwoColour = "#30c7a4";
    let cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
    let selected = ["no", "no", "no", "no", "no", "no", "no", "no", "no"];
    let playerOneCells = [];
    let playerTwoCells = [];
    let playerOneScore = 0;
    let playerTwoScore = 0;

    function change(cell){
        open = false
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
            selected[cell] = "yes";
        }
    }
    function clear(button){
        cellColours = ["white", "white", "white", "white", "white", "white", "white", "white", "white"];
        selected = ["no", "no", "no", "no", "no", "no", "no", "no", "no"];
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
        if(open == false){
            buttonText = "Change Colours";
        }else if(open == true){
            buttonText = "Close";
        }
        if(lightMode == true){
            modeButtonText = "Turn on dark mode"
        }else{
            modeButtonText = "Turn on light mode"
        }
    }

    let open = false;
    let buttonText = "Change Colours";
    function show(){
        open = !open;
    }
    let lightMode = true;
    let modeButtonText = "Turn on dark mode"
    function changeColourMode(){
        lightMode = !lightMode;
    }
</script>
<svelte:head>
    {#if lightMode == false}
        <link rel="stylesheet" href="/src/alternate-style.css">
    {:else if lightMode == true}
        <link rel="stylesheet" href="/src/style.css">
    {/if}
</svelte:head>

<title>Tic Tac Toe</title>
<h1>Tic Tac Toe</h1>
{#if turn == false}
    <h2 style="color:{playerOneColour};">Player One's Turn</h2>
{:else}
    <h2 style="color:{playerTwoColour};">Player Two's Turn</h2>
{/if}
<button on:click={() => clear(":)")}>Reset</button>
<div class="scores">
    <h2 style="color:{playerOneColour}">{playerOneScore}</h2>
    <h2 style="color:{playerTwoColour}">{playerTwoScore}</h2>
</div>
<div class="board">
    {#each cells as cell}
        <div class={selected[cell]} on:click={() => change(cell)} style="background-color:{cellColours[cell]}"></div>
    {/each}
</div>
{#if cellColours.includes(playerOneColour) == false && cellColours.includes(playerTwoColour) == false}
    <button id="colour-change" on:click={show}>{buttonText}</button>
    <button on:click={() => changeColourMode()}>{modeButtonText}</button>
{/if}
{#if open == true}
    <div class="colour-change-selectors">
        <h4>Player One Colour: <input type="color" bind:value={playerOneColour}></h4>
        <h4>Player Two Colour: <input type="color" bind:value={playerTwoColour}></h4>
    </div>
{/if}
