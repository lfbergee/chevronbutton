<style>
	button {
		border: 1px solid #3d3d3d;
		border-radius: 4px;
		background-color: #fafafa;
		color: #3d3d3d;
		position: relative;
		padding: 12px 32px 12px 12px;
		font-size: 1rem;
		transition: 150ms cubic-bezier(0.075, 0.82, 0.165, 1);
		transition-property: background-color, color;

	}

	button::after {
		content: ">";
		position: absolute;
		right: 12px;
		transition: 250ms cubic-bezier(0.075, 0.82, 0.165, 1) right;
	}

	button:hover::after {
		right: 8px;
	}

	button:active {
		background-color: #3d3d3d;
		color: #fafafa;
	}

</style>

<svelte:head>
	<title>Chevron button</title>
</svelte:head>

<h1>The home of the humble chevron button</h1>
<button>Chevron button</button>

