<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Checker Game</title>
    <style>
        body {
            display: flex;
            justify-content: center;
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
            font-size: 24px;
        }
        .white {
            background-color: #fff;
        }
        .black {
            background-color: #000;
            color: #fff;
        }
    </style>
</head>
<body>
    <div id="board"></div>

    <script>
        const board = document.getElementById('board');
        let turn = 'X';

        // Create the checkerboard
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                const square = document.createElement('div');
                square.classList.add('square', (row + col) % 2 === 0 ? 'white' : 'black');
                square.dataset.row = row;
                square.dataset.col = col;
                square.addEventListener('click', handleSquareClick);
                board.appendChild(square);
            }
        }

        function handleSquareClick(event) {
            const square = event.target;
            if (square.classList.contains('white')) {
                square.textContent = turn;
                square.classList.remove('white');
                square.classList.add('black');
                turn = turn === 'X' ? 'O' : 'X';
            }
        }
    </script>
</body>
</html>
