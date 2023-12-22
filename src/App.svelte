<script lang="ts">
	import Button from "./Button.svelte";
	import Screen from "./Screen.svelte";
    import Settings from "./Settings.svelte";

	let screenText = "0";
	let screenSubtext = "";

	let primedToClear = false;

	function addToScreen(number: string) {  
	
		// User does an operation when there is already an operation; Evaluate the current one and then start the new one
		if (screenSubtext.length > 0 && !number.match(/\d/)) {
			evaluate();
			screenSubtext = screenText + number;
			primedToClear = true;
			return;
		}

		if (screenText === "0") {
			screenText = number;
		} else if (!number.match(/\d/)) {
			screenSubtext = screenText;
			screenSubtext += number;
			primedToClear = true;
		} else {
			if (primedToClear) {
				screenText = "";
				primedToClear = false;
			}
			screenText += number;
		}
	}

	function evaluate() {
		const result = eval((screenSubtext + screenText).replaceAll(/×/g, "*")); 
		screenSubtext = screenSubtext + screenText + " =";
		screenText = result.toString();
	}

	let settingsIsOpen = false;

	function openSettings() {
		settingsIsOpen = true;
	}

	function closeSettings() {
		settingsIsOpen = false;
	}

	let baseColor = "#FFCC55";
	let topColor = removeGreen(baseColor, 80);

	function setBaseColor(color: string) {
		baseColor = color;
		topColor = removeGreen(baseColor, 80);
	}

	function removeGreen(hexColor: string, percent: number) {
		const red = parseInt(hexColor.substring(1, 3), 16);
		const green = parseInt(hexColor.substring(3, 5), 16);
		const blue = parseInt(hexColor.substring(5, 7), 16);

		const newGreen = Math.max(0, green - percent);
		const newHex = "#" + red.toString(16) + newGreen.toString(16) + blue.toString(16);
		return newHex;
	}
</script> 

<main style:background={`linear-gradient(${topColor}, ${baseColor})`}>
	{#if settingsIsOpen}
		<Settings closeSettings={closeSettings} setBaseColor={setBaseColor} baseColor={baseColor}/>
	{:else}
		{#key [screenText, screenSubtext]}
			<Screen text={screenText} subtext={screenSubtext} openSettings={openSettings}/>
		{/key}

		<Button baseColor={baseColor} key="c" text="C" onClick={() => {screenText = "0"; screenSubtext = "";}} />
		<Button baseColor={baseColor} key="Backspace" text="<" onClick={() => screenText = screenText.substring(0, screenText.length - 1)} />
		<Button baseColor={baseColor} text="^" onClick={() => addToScreen("^")} />
		<Button baseColor={baseColor} text="/" onClick={() => addToScreen("/")} />
		<Button baseColor={baseColor} text="7" onClick={() => addToScreen("7")} />
		<Button baseColor={baseColor} text="8" onClick={() => addToScreen("8")} />
		<Button baseColor={baseColor} text="9" onClick={() => addToScreen("9")} />
		<Button baseColor={baseColor} text="×" onClick={() => addToScreen("×")} />
		<Button baseColor={baseColor} text="4" onClick={() => addToScreen("4")} />
		<Button baseColor={baseColor} text="5" onClick={() => addToScreen("5")} />
		<Button baseColor={baseColor} text="6" onClick={() => addToScreen("6")} />
		<Button baseColor={baseColor} text="-" onClick={() => addToScreen("-")} />
		<Button baseColor={baseColor} text="1" onClick={() => addToScreen("1")} />
		<Button baseColor={baseColor} text="2" onClick={() => addToScreen("2")} />
		<Button baseColor={baseColor} text="3" onClick={() => addToScreen("3")} />
		<Button baseColor={baseColor} text="+" onClick={() => addToScreen("+")} />
		<Button baseColor={baseColor} text="0" onClick={() => addToScreen("0")} />
		<Button baseColor={baseColor} text="." onClick={() => addToScreen(".")} />
		<Button baseColor={baseColor} key="Enter" text="=" onClick={evaluate} />
	{/if}
</main>

<style lang="scss">
	main {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: 2fr repeat(5, 1fr);
		font-family: "Segoe UI";
		width: 100vw;
		height: 100%;
		overflow: hidden;
	}
</style>
