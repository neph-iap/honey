<script lang="ts">
	export let text: string;
	export let onClick: () => void;

	let backgroundColor = text.match(/[0-9\.]/) ? "transparent" : text.match(/^=$/) ? "#FFCC33" : "rgba(255, 255, 255, 0.2)";
	let aspectRatio = text.match(/^=$/) ? 2 : 1;
	let equalClass= text.match(/^=$/) ? "equal" : "";
</script>

<button 
	on:click={onClick} 
	style:background-color={backgroundColor} 
	style:aspect-ratio={aspectRatio}
	class={equalClass}
>
{text}
</button>  

<style lang="scss">
	button {
		color: white;
		font-size: 2rem;
		font-family: "Segoe UI";
		position: relative;

		&:hover::after {
			content: "";
			position: absolute;
			width:100%;
			height: 100%;
			background: rgba(255, 255, 255, 0.2);
			top: 0px;
			left: 0px;
		}

		&:active::after {
			content: "";
			position: absolute;
			width:100%;
			height: 100%;
			background: rgba(255, 255, 255, 0.4);
			top: 0px;
			left: 0px;
		}
	}

	.equal {
		grid-column: 3 / span 2;
		box-shadow: 0 0 25px rgba(0, 0, 0, 0.15);
	}
</style>
