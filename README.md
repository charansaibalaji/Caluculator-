# Caluculator-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Smart Calculator</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      background: #282c34;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .calculator {
      background: #1e1e2f;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 8px 16px rgba(0,0,0,0.4);
      width: 320px;
    }

    .display {
      background: #000;
      color: #0f0;
      font-size: 2rem;
      padding: 15px;
      border-radius: 10px;
      text-align: right;
      margin-bottom: 20px;
      word-wrap: break-word;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      font-size: 1.4rem;
      padding: 20px;
      border: none;
      border-radius: 10px;
      background: #3c3f4e;
      color: white;
      cursor: pointer;
      transition: background 0.2s;
    }

    button:hover {
      background: #5c5f6e;
    }

    .operator {
      background: #ff9500;
      color: white;
    }

    .operator:hover {
      background: #e08600;
    }

    .equals {
      background: #34c759;
      grid-column: span 2;
    }

    .equals:hover {
      background: #28a745;
    }

    @media (max-width: 400px) {
      .calculator {
        width: 95%;
      }
    }
  </style>
</head>
<body>

  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button onclick="clearDisplay()">C</button>
      <button onclick="deleteLast()">⌫</button>
      <button onclick="append('%')">%</button>
      <button class="operator" onclick="append('/')">÷</button>

      <button onclick="append('7')">7</button>
      <button onclick="append('8')">8</button>
      <button onclick="append('9')">9</button>
      <button class="operator" onclick="append('*')">×</button>

      <button onclick="append('4')">4</button>
      <button onclick="append('5')">5</button>
      <button onclick="append('6')">6</button>
      <button class="operator" onclick="append('-')">−</button>

      <button onclick="append('1')">1</button>
      <button onclick="append('2')">2</button>
      <button onclick="append('3')">3</button>
      <button class="operator" onclick="append('+')">+</button>

      <button onclick="append('0')">0</button>
      <button onclick="append('.')">.</button>
      <button class="equals" onclick="calculate()">=</button>
    </div>
  </div>

  <script>
    let display = document.getElementById('display');
    let expression = '';

    function append(value) {
      if (display.textContent === '0' || display.textContent === 'Error') {
        display.textContent = value;
      } else {
        display.textContent += value;
      }
    }

    function clearDisplay() {
      display.textContent = '0';
    }

    function deleteLast() {
      display.textContent = display.textContent.slice(0, -1) || '0';
    }

    function calculate() {
      try {
        const result = Function('"use strict"; return (' + display.textContent + ')')();
        display.textContent = result;
      } catch (e) {
        display.textContent = 'Error';
      }
    }

    // Keyboard support
    document.addEventListener('keydown', (e) => {
      if ((e.key >= '0' && e.key <= '9') || ['+', '-', '*', '/', '%', '.'].includes(e.key)) {
        append(e.key);
      } else if (e.key === 'Enter') {
        calculate();
      } else if (e.key === 'Backspace') {
        deleteLast();
      } else if (e.key === 'Escape') {
        clearDisplay();
      }
    });
  </script>

</body>
</html>
