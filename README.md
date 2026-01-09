# calculator
simple calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .calculator {
            width: 250px;
            border-radius: 10px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            text-align: center;
        }
        .display {
            width: 100%;
            height: 50px;
            font-size: 24px;
            text-align: right;
            padding: 10px;
            margin-bottom: 20px;
            border: 2px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        .button {
            width: 50px;
            height: 50px;
            font-size: 20px;
            border: none;
            border-radius: 5px;
            background-color: #f0f0f0;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .button:hover {
            background-color: #ddd;
        }
        .button:active {
            background-color: #ccc;
        }
        .button.clear {
            background-color: #ff4d4d;
            color: #fff;
        }
        .button.equals {
            background-color: #4caf50;
            color: #fff;
            grid-column: span 2;
        }
        .button.operator {
            background-color: #f9b500;
            color: white;
        }
    </style>
</head>
<body>

<div class="calculator">
    <input type="text" class="display" id="display" disabled />
    <div class="buttons">
        <button class="button" onclick="appendNumber('7')">7</button>
        <button class="button" onclick="appendNumber('8')">8</button>
        <button class="button" onclick="appendNumber('9')">9</button>
        <button class="button operator" onclick="setOperation('/')">/</button>

        <button class="button" onclick="appendNumber('4')">4</button>
        <button class="button" onclick="appendNumber('5')">5</button>
        <button class="button" onclick="appendNumber('6')">6</button>
        <button class="button operator" onclick="setOperation('*')">*</button>

        <button class="button" onclick="appendNumber('1')">1</button>
        <button class="button" onclick="appendNumber('2')">2</button>
        <button class="button" onclick="appendNumber('3')">3</button>
        <button class="button operator" onclick="setOperation('-')">-</button>

        <button class="button" onclick="appendNumber('0')">0</button>
        <button class="button" onclick="clearDisplay()" class="clear">C</button>
        <button class="button equals" onclick="calculate()">=</button>
        <button class="button operator" onclick="setOperation('+')">+</button>
    </div>
</div>

<script>
    let currentInput = '';
    let previousInput = '';
    let operation = null;

    // Append number to the display
    function appendNumber(number) {
        currentInput += number;
        updateDisplay();
    }

    // Set the operation (like +, -, *, /)
    function setOperation(op) {
        if (currentInput === '') return;
        if (previousInput !== '') {
            calculate();
        }
        operation = op;
        previousInput = currentInput;
        currentInput = '';
    }

    // Calculate the result
    function calculate() {
        let result;
        const prev = parseFloat(previousInput);
        const current = parseFloat(currentInput);
        if (isNaN(prev) || isNaN(current)) return;

        switch (operation) {
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
        operation = null;
        previousInput = '';
        updateDisplay();
    }

    // Clear the display
    function clearDisplay() {
        currentInput = '';
        previousInput = '';
        operation = null;
        updateDisplay();
    }

    // Update the display
    function updateDisplay() {
        document.getElementById('display').value = currentInput;
    }
</script>

</body>
</html>
