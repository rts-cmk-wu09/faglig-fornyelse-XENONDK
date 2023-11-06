<script>
	
	export let value;
	export let onSquareClick;
	
	
</script>

<button on:click={onSquareClick}>{value}</button>


<style>
	button {
		width: 100px;
		height: 100px;
		border: 1px solid white;
		color: black;
		font-size: xx-large;
		margin: 0;
		padding: 0;
		vertical-align: middle;
		background-color: #494949;
	}
	button:disabled{
		border: 1px solid white;
		box-shadow: 0px 0px 4px 5px white;

	}
</style>
