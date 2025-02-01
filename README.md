<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Red iPhone-like Calculator</title>
  <style>
    /* Basic Reset */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    /* Body Styling */
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #000;
      font-family: Arial, sans-serif;
    }

    /* Calculator Container */
    .calculator {
      width: 300px;
      background-color: #ff3b30; /* Red Color */
      border-radius: 20px;
      box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.5);
      overflow: hidden;
    }

    /* Display Screen */
    .display {
      background-color: #1c1c1e;
      color: #fff;
      font-size: 2.5rem;
      text-align: right;
      padding: 20px;
      border-bottom: 1px solid #444;
    }

    /* Buttons Grid */
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
      padding: 20px;
    }

    /* Button Styling */
    .buttons button {
      background-color: #333;
      color: #fff;
      font-size: 1.5rem;
      border: none;
      border-radius: 50%;
      padding: 20px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .buttons button:active {
      background-color: #555;
    }

    /* Operator Buttons */
    .buttons .operator {
      background-color: #ff9500;
      color: #fff;
    }

    .buttons .operator:active {
      background-color: #ffaa33;
    }

    /* Zero Button */
    .buttons .zero {
      grid-column: span 2;
      border-radius: 50px;
    }

    /* Clear Button */
    .buttons .clear {
      background-color: #a6a6a6;
      color: #000;
    }

    .buttons .clear:active {
      background-color: #bfbfbf;
    }
  </style>
</head>
<body>

  <!-- Calculator Structure -->
  <div class="calculator">
    <!-- Display Screen -->
    <div class="display" id="display">0</div>

    <!-- Buttons -->
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button class="operator" onclick="appendOperator('/')">/</button>
      <button class="operator" onclick="appendOperator('*')">*</button>
      <button class="operator" onclick="deleteLast()">DEL</button>
      <button onclick="appendNumber(7)">7</button>
      <button onclick="appendNumber(8)">8</button>
      <button onclick="appendNumber(9)">9</button>
      <button class="operator" onclick="appendOperator('-')">-</button>
      <button onclick="appendNumber(4)">4</button>
      <button onclick="appendNumber(5)">5</button>
      <button onclick="appendNumber(6)">6</button>
      <button class="operator" onclick="appendOperator('+')">+</button>
      <button onclick="appendNumber(1)">1</button>
      <button onclick="appendNumber(2)">2</button>
      <button onclick="appendNumber(3)">3</button>
      <button class="operator" onclick="calculateResult()">=</button>
      <button class="zero" onclick="appendNumber(0)">0</button>
      <button onclick="appendNumber('.')">.</button>
    </div>
  </div>

  <!-- JavaScript for Calculator Functionality -->
  <script>
    let display = document.getElementById('display');
    let currentInput = '';
    let operator = null;
    let previousInput = '';

    // Append Number or Decimal
    function appendNumber(number) {
      if (currentInput.includes('.') && number === '.') return;
      currentInput += number;
      updateDisplay();
    }

    // Append Operator
    function appendOperator(op) {
      if (currentInput === '') return;
      if (previousInput !== '') calculateResult();
      operator = op;
      previousInput = currentInput;
      currentInput = '';
    }

    // Calculate Result
    function calculateResult() {
      if (operator === null || currentInput === '') return;
      let result;
      const prev = parseFloat(previousInput);
      const current = parseFloat(currentInput);

      switch (operator) {
        case '+':
          result = prev + current;
          break;
        case '-':
          result = prev - current;
          break;
        case '*':
          result = prev * current;
          break;
        case '/':
          result = prev / current;
          break;
        default:
          return;
      }

      currentInput = result.toString();
      operator = null;
      previousInput = '';
      updateDisplay();
    }

    // Clear Display
    function clearDisplay() {
      currentInput = '';
      operator = null;
      previousInput = '';
      updateDisplay();
    }

    // Delete Last Character
    function deleteLast() {
      currentInput = currentInput.slice(0, -1);
      updateDisplay();
    }

    // Update Display
    function updateDisplay() {
      display.textContent = currentInput || '0';
    }
  </script>

</body>
</html>
