<script>
    let board = [
        [null, null, null],
        [null, null, null],
        [null, null, null]
    ];
    let currentPlayer = 'X';
    let scores = { X: 0, O: 0 }; // Skóre hráčů

    async function handleCellClick(row, col) {
        if (!board[row][col]) {
            board[row][col] = currentPlayer;
            const winner = checkWinner(board);
            if (winner) {
                board[row][col] = winner;
                scores[winner]++; // Zvýšení skóre vítěze
                updateScores(); // Aktualizace zobrazení skóre
                await new Promise(resolve => setTimeout(resolve, 100));
                alert(`Hráč ${winner} vyhrál! Skóre: X(${scores.X}) - O(${scores.O}). Klikněte na OK pro restart hry.`);
                restartGame(); // Restart hry
            } else {
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            }
        }
    }

    function checkWinner(board) {
        const lines = [
            // Vodorovné řádky
            [[0, 0], [0, 1], [0, 2]],
            [[1, 0], [1, 1], [1, 2]],
            [[2, 0], [2, 1], [2, 2]],
            // Svislé řádky
            [[0, 0], [1, 0], [2, 0]],
            [[0, 1], [1, 1], [2, 1]],
            [[0, 2], [1, 2], [2, 2]],
            // Diagonální řádky
            [[0, 0], [1, 1], [2, 2]],
            [[0, 2], [1, 1], [2, 0]]
        ];

        for (let line of lines) {
            const [a, b, c] = line;
            if (board[a[0]][a[1]] && board[a[0]][a[1]] === board[b[0]][b[1]] && board[a[0]][a[1]] === board[c[0]][c[1]]) {
                return board[a[0]][a[1]]; 
            }
        }

        return null; 
    }

    function restartGame() {
        board = [
            [null, null, null],
            [null, null, null],
            [null, null, null]
        ];
        currentPlayer = 'X';
    }

    function updateScores() {
        document.getElementById('scoreX').textContent = scores.X;
        document.getElementById('scoreO').textContent = scores.O;
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
    <div>
        <p>Skóre:</p>
        <p>Hráč X: <span id="scoreX">0</span></p>
        <p>Hráč O: <span id="scoreO">0</span></p>
    </div>
</section>



