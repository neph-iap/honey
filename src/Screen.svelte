<script lang="ts">
	export let text: string;
</script>

<section>{text}</section>

<style lang="scss">
	section {
		grid-column: 1 / 5;
		font-size: 4rem;
		display: flex;
		align-items: flex-end;
		justify-content: flex-end;
		color: white;
		font-family: "Segoe UI";
		padding-right: 1rem;
		padding-bottom: 1rem;
	}
</style>
