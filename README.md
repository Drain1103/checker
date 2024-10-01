<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Checkers Game</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
        }
        #board {
            display: grid;
            grid-template-columns: repeat(8, 50px);
            grid-template-rows: repeat(8, 50px);
            border: 2px solid #333;
        }
        .square {
            width: 50px;
            height: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }
        .white {
            background-color: #fff;
        }
        .black {
            background-color: #000;
        }
        .piece {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        .red {
            background-color: red; /* Player 1 pieces */
        }
        .green {
            background-color: green; /* Player 2 pieces */
        }
        .king {
            border: 3px solid gold;
        }
        button {
            margin: 20px;
            padding: 10px 20px;
            font-size: 16px;
        }
        .highlight {
            background-color: rgba(255, 255, 0, 0.5); /* Yellow highlight */
        }
        #message {
            font-size: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <button id="resetButton">Restart Game</button>
    <div id="board"></div>
    <div id="message"></div>

    <script>
        const board = document.getElementById('board');
        const resetButton = document.getElementById('resetButton');
        const message = document.getElementById('message');
        let turn = 'red'; // Starting player
        let selectedPiece = null;
        let selectedSquare = null;

        resetButton.addEventListener('click', resetGame);
        initializeBoard();

        function initializeBoard() {
            board.innerHTML = ''; // Clear the board
            for (let row = 0; row < 8; row++) {
                for (let col = 0; col < 8; col++) {
                    const square = document.createElement('div');
                    square.classList.add('square', (row + col) % 2 === 0 ? 'white' : 'black');
                    square.dataset.row = row;
                    square.dataset.col = col;

                    // Add pieces to the initial setup
                    if (row < 3 && (row + col) % 2 === 1) {
                        addPiece(square, 'red'); // Add red pieces
                    } else if (row > 4 && (row + col) % 2 === 1) {
                        addPiece(square, 'green'); // Add green pieces
                    }

                    square.addEventListener('click', handleSquareClick);
                    board.appendChild(square);
                }
            }
            updateMessage();
        }

        function addPiece(square, color) {
            const piece = document.createElement('div');
            piece.classList.add('piece', color);
            square.appendChild(piece);
        }

        function handleSquareClick(event) {
            const square = event.target.closest('.square');
            if (!square) return;

            if (selectedPiece) {
                // Attempt to move the selected piece
                if (isValidMove(selectedSquare, square)) {
                    movePiece(selectedSquare, square);
                    clearHighlights();
                    // Switch turns only if the move was successful
                    turn = turn === 'red' ? 'green' : 'red'; 
                } else {
                    alert('Invalid move!');
                }
                selectedPiece = null; // Deselect piece
                selectedSquare = null; // Clear selected square
            } else {
                // Select the piece if it's the player's turn
                const piece = square.querySelector('.piece.' + turn);
                if (piece) {
                    selectedPiece = piece;
                    selectedSquare = square;
                    highlightValidMoves(square); // Highlight valid moves for the selected piece
                }
            }
            checkWinCondition();
        }

        function highlightValidMoves(square) {
            const fromRow = parseInt(square.dataset.row);
            const fromCol = parseInt(square.dataset.col);
            const piece = square.querySelector('.piece');
            const isKing = piece && piece.classList.contains('king');

            // Check possible moves
            const directions = isKing ? [[1, 1], [1, -1], [-1, 1], [-1, -1]] : (turn === 'red' ? [[1, 1], [1, -1]] : [[-1, 1], [-1, -1]]);
            directions.forEach(([rowDir, colDir]) => {
                const toRow = fromRow + rowDir;
                const toCol = fromCol + colDir;
                const jumpRow = fromRow + 2 * rowDir;
                const jumpCol = fromCol + 2 * colDir;

                const toSquare = document.querySelector(`.square[data-row='${toRow}'][data-col='${toCol}']`);
                const jumpSquare = document.querySelector(`.square[data-row='${jumpRow}'][data-col='${jumpCol}']`);

                // Normal move
                if (toSquare && toSquare.children.length === 0 && isValidDirection(fromRow, fromCol, toRow, toCol)) {
                    toSquare.classList.add('highlight');
                }

                // Capture move
                if (jumpSquare && jumpSquare.children.length === 0 && isOpponentPiece(fromRow, fromCol, toRow, toCol)) {
                    jumpSquare.classList.add('highlight');
                }
            });
        }

        function clearHighlights() {
            const highlightedSquares = document.querySelectorAll('.highlight');
            highlightedSquares.forEach(square => square.classList.remove('highlight'));
        }

        function isValidMove(fromSquare, toSquare) {
            const fromRow = parseInt(fromSquare.dataset.row);
            const fromCol = parseInt(fromSquare.dataset.col);
            const toRow = parseInt(toSquare.dataset.row);
            const toCol = parseInt(toSquare.dataset.col);

            const destinationIsEmpty = toSquare.children.length === 0;

            // Check for simple moves
            if (destinationIsEmpty && Math.abs(toRow - fromRow) === 1 && Math.abs(toCol - fromCol) === 1) {
                return isValidDirection(fromRow, fromCol, toRow, toCol); // Validate direction
            }

            // Check for capture moves
            if (destinationIsEmpty && Math.abs(toRow - fromRow) === 2 && Math.abs(toCol - fromCol) === 2) {
                return isOpponentPiece(fromRow, fromCol, toRow, toCol); // Check if can capture
            }

            return false; // Invalid move
        }

        function isValidDirection(fromRow, fromCol, toRow, toCol) {
            // Red can only move downwards, green can only move upwards
            if (turn === 'red') {
                return toRow > fromRow; // Red pieces can only move forward
            } else if (turn === 'green') {
                return toRow < fromRow; // Green pieces can only move forward
            }
            return false; // Invalid direction
        }

        function movePiece(fromSquare, toSquare) {
            toSquare.appendChild(selectedPiece);
            fromSquare.removeChild(selectedPiece);
            const toRow = parseInt(toSquare.dataset.row);
            if ((turn === 'red' && toRow === 7) || (turn === 'green' && toRow === 0)) {
                selectedPiece.classList.add('king'); // Crown the piece
            }

            // Capture logic
            const midRow = (parseInt(fromSquare.dataset.row) + toRow) / 2;
            const midCol = (parseInt(fromSquare.dataset.col) + parseInt(toSquare.dataset.col)) / 2;
            const midSquare = document.querySelector(`.square[data-row='${midRow}'][data-col='${midCol}']`);

            if (midSquare) {
                const opponentPiece = midSquare.querySelector('.piece.' + (turn === 'red' ? 'green' : 'red'));
                if (opponentPiece) {
                    midSquare.removeChild(opponentPiece); // Remove captured piece
                }
            }
        }

        function isOpponentPiece(fromRow, fromCol, toRow, toCol) {
            const midRow = (fromRow + toRow) / 2;
            const midCol = (fromCol + toCol) / 2;
            const midSquare = document.querySelector(`.square[data-row='${midRow}'][data-col='${midCol}']`);

            if (midSquare) {
                const opponentColor = turn === 'red' ? 'green' : 'red';
                return midSquare.querySelector('.piece.' + opponentColor) !== null;
            }
            return false;
        }

        function checkWinCondition() {
            const redPieces = document.querySelectorAll('.piece.red');
            const greenPieces = document.querySelectorAll('.piece.green');
            if (redPieces.length === 0) {
                message.textContent = "Green Wins!";
                resetButton.style.display = 'block';
            } else if (greenPieces.length === 0) {
                message.textContent = "Red Wins!";
                resetButton.style.display = 'block';
            } else {
                updateMessage();
            }
        }

        function updateMessage() {
            message.textContent = turn.charAt(0).toUpperCase() + turn.slice(1) + "'s Turn";
            resetButton.style.display = 'none'; // Hide reset button during the game
        }

        function resetGame() {
            turn = 'red';
            selectedPiece = null;
            selectedSquare = null;
            message.textContent = "";
            initializeBoard();
        }
    </script>
</body>
</html>
