<script>
    let board = [
        [null, null, null],
        [null, null, null],
        [null, null, null]
    ];
    let currentPlayer = 'X';
    
    function handleCellClick(row, col) {
        if (!board[row][col]) {
            board[row][col] = currentPlayer;
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        }
    }
</script>

<section>
    <h1>Piškvorky</h1>
    <div id="board">
        {#each board as row, rowIndex}
            <div class="row">
                {#each row as cell, colIndex}
                    <div class="cell" on:click={() => handleCellClick(rowIndex, colIndex)}>
                        {#if cell === 'X'}
                            <span class="symbol">X</span>
                        {:else if cell === 'O'}
                            <span class="symbol">O</span>
                        {/if}
                    </div>
                {/each}
            </div>
        {/each}
    </div>
</section>
