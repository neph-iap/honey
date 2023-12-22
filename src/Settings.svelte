<script lang="ts">
	import backIcon from "./assets/images/back.png";

	export let closeSettings: () => void;
	export let setBaseColor: (color: string) => void;
	export let baseColor: string;

	function handleColorChange(event: Event) {
		baseColor = (event.target as HTMLInputElement).value;
		setBaseColor(baseColor);
	} </script>

<section>
	<img src={backIcon} class="settingsButton" alt="Settings gear" on:click={closeSettings}/>
	<span>Base color</span>
	<input type="color" bind:value={baseColor} on:change={handleColorChange} style="width: 100%; color: white;"/>
</section>

<style lang="scss">
	section {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		height: 100%;
		grid-column: 1 / span 4;
		padding: 1rem;
		color: white;
		font-size: 2rem;

		input {
			height: 3rem;
		}
	}

	.settingsButton {
		position: absolute;
		top: 0.5rem;
		left: 0.5rem;
		filter: invert(100%);
		width: 2rem;
		height: 2rem;
		opacity: 0.5;
		cursor: pointer;
	}
</style>
