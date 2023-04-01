# Calculator

A basic calculator built with HTML, CSS, and JavaScript. This calculator allows users to perform simple arithmetic operations such as addition, subtraction, multiplication, and division. It also includes a decimal point and a clear button to reset the calculation.

## Usage

To use the calculator, simply click on the buttons on the screen or type on your keyboard. The following keys are supported:

- Numbers (0-9)
- Addition (+)
- Subtraction (-)
- Multiplication (*)
- Division (/)
- Decimal point (.)
- Enter key (=)
- Escape key (clear screen)
- Backspace key (delete the last entered character)

## Functionality

The calculator uses the `eval()` function to perform the calculations entered by the user. It also includes a `formatString()` function that adds separators to the numbers displayed on the screen for better readability.

The calculator is built with Svelte, a modern web framework that allows for reactive components and efficient DOM updates. The project uses the `$:` syntax to bind the formatted number to the input element on the screen.

## How to Run

To run the project, simply use the `npm install && npm run dev` commands in your console. Alternatively, you can build it with `npm run build` and then use a web server such as [live-server](https://www.npmjs.com/package/live-server) to serve the files locally.