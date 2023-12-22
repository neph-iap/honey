<script lang="ts">
	export let text: string;
	export let subtext: string;
</script>

<section>
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
</style>
