<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Akash - Betting Game</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      background: #0c1021;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      height: 100vh;
    }

    h1 {
      margin-top: 20px;
      font-size: 2rem;
      color: #00f7ff;
    }

    .balance {
      margin: 10px;
      font-size: 1.2rem;
    }

    .bet-section {
      margin: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      background: #1f2333;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 0 20px rgba(0, 255, 255, 0.2);
    }

    input {
      padding: 10px;
      font-size: 1rem;
      width: 150px;
      margin: 10px;
      border: none;
      border-radius: 8px;
      outline: none;
    }

    button {
      padding: 10px 20px;
      font-size: 1rem;
      margin: 10px;
      border: none;
      border-radius: 8px;
      background: #00f7ff;
      color: #000;
      cursor: pointer;
      transition: background 0.3s;
    }

    button:hover {
      background: #00c0cc;
    }

    .results {
      margin-top: 20px;
      text-align: center;
    }

    .results p {
      margin: 5px 0;
      font-size: 1.1rem;
    }
  </style>
</head>
<body>
  <h1>AKASH - Big or Small</h1>
  <div class="balance">Balance: $<span id="balance">100</span></div>

  <div class="bet-section">
    <input type="number" id="betAmount" placeholder="Enter bet amount" min="1" />
    <div>
      <button onclick="placeBet('big')">Bet on Big (8-12)</button>
      <button onclick="placeBet('small')">Bet on Small (1-6)</button>
    </div>
  </div>

  <div class="results">
    <p id="randomNumber">Result: -</p>
    <p id="outcome">Place your bet</p>
  </div>

  <script>
    let balance = 100;

    function placeBet(choice) {
      const betAmount = parseInt(document.getElementById("betAmount").value);
      const resultDisplay = document.getElementById("randomNumber");
      const outcomeDisplay = document.getElementById("outcome");
      const balanceDisplay = document.getElementById("balance");

      if (isNaN(betAmount) || betAmount <= 0) {
        alert("Enter a valid bet amount.");
        return;
      }

      if (betAmount > balance) {
        alert("You don't have enough balance.");
        return;
      }

      const number = Math.floor(Math.random() * 12) + 1;
      resultDisplay.innerText = `Result: ${number}`;

      if (number === 7) {
        balance -= betAmount;
        outcomeDisplay.innerText = "Number is 7: House wins!";
      } else if ((number >= 8 && choice === "big") || (number <= 6 && choice === "small")) {
        balance += betAmount;
        outcomeDisplay.innerText = "You won!";
      } else {
        balance -= betAmount;
        outcomeDisplay.innerText = "You lost!";
      }

      balanceDisplay.innerText = balance;

      if (balance <= 0) {
        alert("Game over! You have no money left.");
        document.querySelectorAll("button").forEach(btn => btn.disabled = true);
      }
    }
  </script>
</body>
</html>
