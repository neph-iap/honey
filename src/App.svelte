<script lang="ts">
	import Button from "./Button.svelte";
	import Screen from "./Screen.svelte";

	let screenText = "0";

	function addToScreen(number: string) {  
		if (screenText === "0") {
			screenText = number;
		} else {
			screenText += number;
		}
	}

	function evaluate() {
		const result = eval(screenText.replace(/×/g, "*"));
		screenText = result.toString();
	}

	document.addEventListener("keypress", event => {
		switch(event.key) {
			case "1": 
			case "2": 
			case "3": 
			case "4": 
			case "5": 
			case "6": 
			case "7": 
			case "8": 
			case "9": 
			case "0": addToScreen(event.key); break;
			case "+": addToScreen(" + "); break;
			case "-": addToScreen(" - "); break;
			case "*": addToScreen(" × "); break;
			case "/": addToScreen(" / "); break;
			case "^": addToScreen(" ^ "); break;
			case "(": addToScreen("("); break;
			case ")": addToScreen(")"); break;
			case "=": evaluate(); break;
			case "Enter": evaluate(); break;
			case "Backspace": screenText = screenText.substring(0, screenText.length - 1); break;
			case "c": screenText = "0"; break;
		}
	});
</script> <main>
	<Screen text={screenText}/>
	<Button text="C" onClick={() => screenText = "0"} />
	<Button text="<" onClick={() => screenText = screenText.substring(0, screenText.length)} />
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
	<Button text="=" onClick={evaluate} />
</main>

<style lang="scss">
	main {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: 2fr repeat(5, 1fr);
		background: linear-gradient(#FF9900, #FFBB33);
		font-family: "Segoe UI"
	}
</style>
