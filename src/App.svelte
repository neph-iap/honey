<script lang="ts">
	import Button from "./Button.svelte";
	import Screen from "./Screen.svelte";

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
</script> 

<main>
	{#key [screenText, screenSubtext]}
		<Screen text={screenText} subtext={screenSubtext}/>
	{/key}
	<Button key="c" text="C" onClick={() => {screenText = "0"; screenSubtext = "";}} />
	<Button key="Backspace" text="<" onClick={() => screenText = screenText.substring(0, screenText.length - 1)} />
	<Button text="^" onClick={() => addToScreen("^")} />
	<Button text="/" onClick={() => addToScreen("/")} />
	<Button text="7" onClick={() => addToScreen("7")} />
	<Button text="8" onClick={() => addToScreen("8")} />
	<Button text="9" onClick={() => addToScreen("9")} />
	<Button text="×" onClick={() => addToScreen("×")} />
	<Button text="4" onClick={() => addToScreen("4")} />
	<Button text="5" onClick={() => addToScreen("5")} />
	<Button text="6" onClick={() => addToScreen("6")} />
	<Button text="-" onClick={() => addToScreen("-")} />
	<Button text="1" onClick={() => addToScreen("1")} />
	<Button text="2" onClick={() => addToScreen("2")} />
	<Button text="3" onClick={() => addToScreen("3")} />
	<Button text="+" onClick={() => addToScreen("+")} />
	<Button text="0" onClick={() => addToScreen("0")} />
	<Button text="." onClick={() => addToScreen(".")} />
	<Button key="Enter" text="=" onClick={evaluate} />
</main>

<style lang="scss">
	main {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: 2fr repeat(5, 1fr);
		background: linear-gradient(#FF9900, #FFBB33);
		font-family: "Segoe UI";
		width: 100%;
		height: 100%;
	}
</style>
