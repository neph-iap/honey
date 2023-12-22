<script lang="ts">
	import gearIcon from "./assets/images/gear.png";
	
	export let text: string;
	export let subtext: string;
	export let openSettings: () => void;
</script>

<section>
	<img src={gearIcon} class="settingsButton" alt="Settings gear" on:click={openSettings}/>
	<span class="subtext">{subtext}</span>
	<span class="maintext">{text}</span>
</section>

<style lang="scss">
	section {
		grid-column: 1 / 5;
		font-size: 4rem;
		display: flex;
		flex-direction: column;
		align-items: flex-end;
		justify-content: flex-end;
		color: white;
		font-family: "Segoe UI";
		padding-right: 1rem;
		padding-bottom: 1rem;
	}

	.subtext {
		font-size: 2rem;
		opacity: 0.6;
	}
	
	.maintext {
		height: 1lh;
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
