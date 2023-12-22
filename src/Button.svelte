<script lang="ts">
	import { onDestroy, onMount } from "svelte";

	export let text: string;
	export let onClick: () => void;
	export let key: string | null = null;
	export let baseColor: string;

	let backgroundColor = text.match(/[0-9\.]/) ? "transparent" : text.match(/=/) ? baseColor : "rgba(255, 255, 255, 0.2)";
	let aspectRatio = text.match(/^=$/) ? 2 : 1;
	let equalClass = text.match(/^=$/) ? "equal" : "";

	// on mount so that this only happens once
	onMount(() => {
		document.addEventListener("keydown", event => {
			if (event.key === (key ?? text)) {
				onClick();
				button.classList.add("active");
			}
		});

		document.addEventListener("keyup", event => {
			if (event.key === (key ?? text)) {
				button.classList.remove("active");
			}
		});
	});

	onDestroy(() => {
		document.removeEventListener("keydown", event => {
			if (event.key === (key ?? text)) {
				onClick();
				button.classList.add("active");
			}
		});

		document.removeEventListener("keyup", event => {
			if (event.key === (key ?? text)) {
				button.classList.remove("active");
			}
		});
	});

	let button: HTMLButtonElement;

</script>

<button 
	on:click={onClick} 
	style:background-color={backgroundColor} 
	style:aspect-ratio={aspectRatio}
	class={equalClass}
	bind:this={button}
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

		&:active::after, &.active::after {
			content: "";
			position: absolute;
			width:100%;
			height: 100%;
			background: rgba(255, 255, 255, 0.25);
			top: 0px;
			left: 0px;
		}
	}

	.equal {
		grid-column: 3 / span 2;
		box-shadow: 0 0 25px rgba(0, 0, 0, 0.15);
		filter: hue-rotate(10deg) brightness(1.1);
		font-weight: bold;
	}
</style>
