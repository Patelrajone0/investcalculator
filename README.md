# investcalculator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Future Investment & Calculator App</title>
  <style>
    :root {
      --bg-light: #f9f9f9;
      --text-light: #111;
      --bg-dark: #121212;
      --text-dark: #f9f9f9;
      --primary: #4CAF50;
      --accent: #FF9800;
      --card-bg-light: #ffffff;
      --card-bg-dark: #1e1e1e;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--bg-light);
      color: var(--text-light);
      transition: background-color 0.3s, color 0.3s;
    }

    .dark-mode {
      background-color: var(--bg-dark);
      color: var(--text-dark);
    }

    .container {
      max-width: 900px;
      margin: auto;
      padding: 2rem;
    }

    h1, h2 {
      text-align: center;
      color: var(--primary);
    }

    .toggle-btn {
      float: right;
      padding: 0.5rem 1rem;
      background: var(--accent);
      border: none;
      color: white;
      font-weight: bold;
      cursor: pointer;
      border-radius: 5px;
    }

    .card {
      background-color: var(--card-bg-light);
      border-radius: 10px;
      padding: 20px;
      margin-top: 20px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      transition: background-color 0.3s;
    }

    .dark-mode .card {
      background-color: var(--card-bg-dark);
    }

    label {
      display: block;
      margin: 10px 0 5px;
    }

    input[type="number"], select {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-bottom: 10px;
    }

    button.calculate-btn {
      background: var(--primary);
      color: white;
      padding: 10px;
      border: none;
      border-radius: 5px;
      width: 100%;
      font-size: 1rem;
      cursor: pointer;
    }

    .result {
      font-size: 1.2rem;
      margin-top: 10px;
      text-align: center;
      font-weight: bold;
      color: var(--accent);
    }

    .row {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
    }

    .col {
      flex: 1 1 45%;
      min-width: 300px;
    }

    footer {
      text-align: center;
      margin-top: 40px;
      color: gray;
    }
  </style>
</head>
<body>
  <div class="container">
    <button class="toggle-btn" onclick="toggleMode()">Toggle Light/Dark</button>
    <h1>💰 Future Investment & 🧮 Calculator App</h1>

    <div class="row">
      <!-- Investment Calculator -->
      <div class="col">
        <div class="card">
          <h2>📈 Future Investment Calculator</h2>
          <label for="principal">Principal Amount (₹)</label>
          <input type="number" id="principal" placeholder="Enter initial amount">

          <label for="rate">Annual Interest Rate (%)</label>
          <input type="number" id="rate" placeholder="e.g., 7.5">

          <label for="years">Time (in years)</label>
          <input type="number" id="years" placeholder="e.g., 5">

          <label for="compound">Compound Frequency</label>
          <select id="compound">
            <option value="1">Annually</option>
            <option value="2">Semi-Annually</option>
            <option value="4">Quarterly</option>
            <option value="12">Monthly</option>
          </select>

          <button class="calculate-btn" onclick="calculateInvestment()">Calculate Future Value</button>
          <div class="result" id="investmentResult"></div>
        </div>
      </div>

      <!-- Basic Calculator -->
      <div class="col">
        <div class="card">
          <h2>🧮 Basic Calculator</h2>
          <label for="num1">First Number</label>
          <input type="number" id="num1" placeholder="Enter first number">

          <label for="operation">Operation</label>
          <select id="operation">
            <option value="+">Addition (+)</option>
            <option value="-">Subtraction (-)</option>
            <option value="*">Multiplication (×)</option>
            <option value="/">Division (÷)</option>
          </select>

          <label for="num2">Second Number</label>
          <input type="number" id="num2" placeholder="Enter second number">

          <button class="calculate-btn" onclick="calculateBasic()">Calculate</button>
          <div class="result" id="basicResult"></div>
        </div>
      </div>
    </div>
    
    <footer>
      &copy; 2025 Created by Raj Patel | Future Investment & Calculator Tool
    </footer>
  </div>

  <script>
    function calculateInvestment() {
      const principal = parseFloat(document.getElementById('principal').value);
      const rate = parseFloat(document.getElementById('rate').value) / 100;
      const years = parseFloat(document.getElementById('years').value);
      const compound = parseInt(document.getElementById('compound').value);

      if (isNaN(principal) || isNaN(rate) || isNaN(years) || isNaN(compound)) {
        document.getElementById('investmentResult').innerText = "❌ Please fill in all fields.";
        return;
      }

      const amount = principal * Math.pow((1 + rate / compound), compound * years);
      const futureValue = amount.toFixed(2);
      document.getElementById('investmentResult').innerText = `📊 Future Value: ₹${futureValue}`;
    }

    function calculateBasic() {
      const num1 = parseFloat(document.getElementById('num1').value);
      const num2 = parseFloat(document.getElementById('num2').value);
      const op = document.getElementById('operation').value;

      if (isNaN(num1) || isNaN(num2)) {
        document.getElementById('basicResult').innerText = "❌ Enter both numbers.";
        return;
      }

      let result;
      switch (op) {
        case '+': result = num1 + num2; break;
        case '-': result = num1 - num2; break;
        case '*': result = num1 * num2; break;
        case '/':
          if (num2 === 0) {
            document.getElementById('basicResult').innerText = "❌ Cannot divide by zero.";
            return;
          }
          result = num1 / num2;
          break;
      }

      document.getElementById('basicResult').innerText = `✅ Result: ${result.toFixed(2)}`;
    }

    function toggleMode() {
      document.body.classList.toggle('dark-mode');
    }
  </script>
</body>
</html>
