<script>
    let board = Array.from({ length: 10 }, () => Array.from({ length: 10 }, () => null)); // 10x10 pole s hodnotami null
    let currentPlayer = 'X';

    async function handleCellClick(row, col) {
        if (!board[row][col]) {
            board[row][col] = currentPlayer;
            const winner = checkWinner(board);
            if (winner) {
                board[row][col] = winner;
                await new Promise(resolve => setTimeout(resolve, 100));
                alert(`Hráč ${winner} vyhrál!`);
            } else {
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            }
        }
    }

    function checkWinner(board) {
        const lines = [];
        for (let i = 0; i < 10; i++) {
            // Vodorovné řádky
            lines.push([[i, 0], [i, 1], [i, 2]]);
            // Svislé řádky
            lines.push([[0, i], [1, i], [2, i]]);
        }
        // Diagonální řádky
        lines.push([[0, 0], [1, 1], [2, 2]]);
        lines.push([[0, 2], [1, 1], [2, 0]]);

        for (let line of lines) {
            const [a, b, c] = line;
            if (board[a[0]][a[1]] && board[a[0]][a[1]] === board[b[0]][b[1]] && board[a[0]][a[1]] === board[c[0]][c[1]]) {
                return board[a[0]][a[1]]; 
            }
        }

        return null; 
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
