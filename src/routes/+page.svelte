<script>
	import Square from '$lib/components/Square.svelte';
	import { writable } from 'svelte/store';

	$: xIsNext = true;
	$: squares = new Array(9).fill(null);
	$: status = writable("Next player: X")

	function handleClick(i) {
	if (squares[i] || calculateWinner(squares)) {
		return;
	}
	const nextSquares = squares.slice();
	xIsNext ? (nextSquares[i] = 'x') : (nextSquares[i] = 'o');
	squares = nextSquares;
	xIsNext = !xIsNext;

	const winner = calculateWinner(squares);
	if (winner) {
		$status = "Winner: " + winner;
	} else {
		$status = "Next player: " + (xIsNext ? "X" : "O");
	}
}

	function calculateWinner(squares) {
		const lines = [
			[0, 1, 2],
			[3, 4, 5],
			[6, 7, 8],
			[0, 3, 6],
			[1, 4, 7],
			[2, 5, 8],
			[0, 4, 8],
			[2, 4, 6]
		];
		for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}


	
</script>

<h1>The Tic Tac Toe game powered by Svelte</h1>
<div>{$status}</div> 
<div class="board">
	<Square value={squares[0]} onSquareClick={() => handleClick(0)} />
	<Square value={squares[1]} onSquareClick={() => handleClick(1)} />
	<Square value={squares[2]} onSquareClick={() => handleClick(2)} />

	<Square value={squares[3]} onSquareClick={() => handleClick(3)} />
	<Square value={squares[4]} onSquareClick={() => handleClick(4)} />
	<Square value={squares[5]} onSquareClick={() => handleClick(5)} />

	<Square value={squares[6]} onSquareClick={() => handleClick(6)} />
	<Square value={squares[7]} onSquareClick={() => handleClick(7)} />
	<Square value={squares[8]} onSquareClick={() => handleClick(8)} />
</div>

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	h1 {
		color: #278916;
		font-size: 3em;
	}

	.board {
		width: 300px;
		height: 300px;
		display: flex;
		flex-wrap: wrap;
	}

	/* div {
		grid-template-columns: repeat(3, 1fr);
		margin: 0%;
		padding: 0%;
	} */
</style>
