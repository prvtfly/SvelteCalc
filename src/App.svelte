<script>
  let currentDisplaying = "";
  let resetAfter = false;
  let formattedNumber = "";

  const operators = ["+", "-", "*", "/"];

  function formatString(str) {
    const separator = /\B(?=(\d{3})+(?!\d))/g;
    const formatted = str.replace(separator, ".");
    return formatted;
  }

  function clearScreen() {
    currentDisplaying = "";
  }

  function handleNumberClick(number) {
    if (resetAfter) {
      currentDisplaying = "";
      resetAfter = false;
    }

    const lastChar = currentDisplaying.charAt(currentDisplaying.length - 1);

    if (operators.includes(lastChar)) {
      currentDisplaying = `${currentDisplaying} ${number}`;
    } else {
      currentDisplaying += number;
    }
  }

  function handleOperatorClick(operator) {
    const lastChar = currentDisplaying.charAt(currentDisplaying.length - 1);

    if (operators.includes(lastChar)) {
      currentDisplaying = currentDisplaying.slice(0, -1);
    }

    currentDisplaying = `${currentDisplaying} ${operator}`;
  }

  function handleDotClick() {
    const lastChar = currentDisplaying.charAt(currentDisplaying.length - 1);
    if (lastChar == "") return;

    if (operators.includes(lastChar)) {
      currentDisplaying = `${currentDisplaying} 0.`;
    } else {
      currentDisplaying += ".";
    }
  }

  function handleCalc() {
    const lastChar = currentDisplaying.charAt(currentDisplaying.length - 1);

    if (operators.includes(lastChar)) {
      currentDisplaying = currentDisplaying.slice(0, -1);
    }

    const result = eval(currentDisplaying);
    if (result == currentDisplaying) return;

    resetAfter = true;
    const fixedResult = result.toFixed(2);

    if (fixedResult.endsWith("00")) {
      currentDisplaying = fixedResult.slice(0, -3);
    } else {
      currentDisplaying = fixedResult;
    }
  }

  function handleKeyPress(event) {
    switch (event.key) {
      case "0":
        handleNumberClick(0);
        break;
      case "1":
        handleNumberClick(1);
        break;
      case "2":
        handleNumberClick(2);
        break;
      case "3":
        handleNumberClick(3);
        break;
      case "4":
        handleNumberClick(4);
        break;
      case "5":
        handleNumberClick(5);
        break;
      case "6":
        handleNumberClick(6);
        break;
      case "7":
        handleNumberClick(7);
        break;
      case "8":
        handleNumberClick(8);
        break;
      case "9":
        handleNumberClick(9);
        break;
      case "+":
        handleOperatorClick("+");
        break;
      case "-":
        handleOperatorClick("-");
        break;
      case "*":
        handleOperatorClick("*");
        break;
      case "/":
        handleOperatorClick("/");
        break;
      case ".":
        handleDotClick();
        break;
      case "Enter":
        handleCalc();
        break;
      case "Escape":
        clearScreen();
        break;
      case "Backspace":
        currentDisplaying = currentDisplaying.slice(0, -1);
        break;
      default:
        break;
    }
  }

  document.addEventListener("keydown", handleKeyPress);
  $: formattedNumber = formatString(currentDisplaying);
</script>

<main>
  <div class="calculator">
    <div class="screen">
      <input type="text" placeholder="0" bind:value={formattedNumber} />
    </div>
    <div class="calculator-grid">
      <div class="calculator-buttons">
        <div class="row">
          <button on:click={() => handleNumberClick(7)}>7</button>
          <button on:click={() => handleNumberClick(8)}>8</button>
          <button on:click={() => handleNumberClick(9)}>9</button>
          <button on:click={() => handleOperatorClick("/")}>/</button>
        </div>
        <div class="row">
          <button on:click={() => handleNumberClick(4)}>4</button>
          <button on:click={() => handleNumberClick(5)}>5</button>
          <button on:click={() => handleNumberClick(6)}>6</button>
          <button on:click={() => handleOperatorClick("*")}>*</button>
        </div>
        <div class="row">
          <button on:click={() => handleNumberClick(1)}>1</button>
          <button on:click={() => handleNumberClick(2)}>2</button>
          <button on:click={() => handleNumberClick(3)}>3</button>
          <button on:click={() => handleOperatorClick("-")}>-</button>
        </div>
        <div class="row">
          <button on:click={() => handleNumberClick(0)}>0</button>
          <button on:click={handleDotClick}>.</button>
          <button on:click={handleCalc}>=</button>
          <button on:click={() => handleOperatorClick("+")}>+</button>
        </div>
        <div class="row">
          <button id="c-btn" on:click={clearScreen}>C</button>
        </div>
      </div>
    </div>
  </div>
</main>
