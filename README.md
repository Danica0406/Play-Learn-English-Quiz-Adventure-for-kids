# Play-Learn-English-Quiz-Adventure-for-kids
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Rock Paper Scissors</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="container">
    <h1>Rock Paper Scissors</h1>
    <div class="score-board">
      <div id="user-label" class="badge">User</div>
      <div id="computer-label" class="badge">Comp</div>
      <span id="user-score">0</span>:<span id="computer-score">0</span>
    </div>
    <div class="result">
      <p>Make your move</p>
    </div>
    <div class="choices">
      <div class="choice" id="r">
        <img src="https://i.imgur.com/TONdG3K.png" alt="Rock" />
      </div>
      <div class="choice" id="p">
        <img src="https://i.imgur.com/7s2nF2U.png" alt="Paper" />
      </div>
      <div class="choice" id="s">
        <img src="https://i.imgur.com/LghSkIw.png" alt="Scissors" />
      </div>
    </div>
    <p id="action-message">Choose Rock, Paper or Scissors</p>
  </div>

  <script src="script.js"></script>
</body>
</html>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: #1f1f1f;
  color: white;
  font-family: 'Segoe UI', sans-serif;
  text-align: center;
  padding: 20px;
}

.container {
  max-width: 600px;
  margin: auto;
}

h1 {
  margin-bottom: 20px;
}

.score-board {
  display: flex;
  justify-content: center;
  font-size: 24px;
  margin-bottom: 20px;
}

.badge {
  font-size: 14px;
  background-color: #e2584d;
  padding: 5px 10px;
  border-radius: 4px;
  margin: 0 10px;
}

.result {
  font-size: 20px;
  margin-bottom: 20px;
}

.choices {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.choice {
  cursor: pointer;
  transition: transform 0.3s ease;
}

.choice:hover {
  transform: scale(1.1);
}

.choice img {
  width: 100px;
}

#action-message {
  font-size: 18px;
  font-style: italic;
}

let userScore = 0;
let computerScore = 0;
const userScore_span = document.getElementById("user-score");
const computerScore_span = document.getElementById("computer-score");
const result_p = document.querySelector(".result p");
const actionMessage = document.getElementById("action-message");
const rock_div = document.getElementById("r");
const paper_div = document.getElementById("p");
const scissors_div = document.getElementById("s");

function getComputerChoice() {
  const choices = ['r', 'p', 's'];
  const randomIndex = Math.floor(Math.random() * 3);
  return choices[randomIndex];
}

function convertToWord(letter) {
  if (letter === "r") return "Rock";
  if (letter === "p") return "Paper";
  return "Scissors";
}

function win(userChoice, computerChoice) {
  userScore++;
  userScore_span.textContent = userScore;
  result_p.textContent = `${convertToWord(userChoice)} beats ${convertToWord(computerChoice)}. You win!`;
}

function lose(userChoice, computerChoice) {
  computerScore++;
  computerScore_span.textContent = computerScore;
  result_p.textContent = `${convertToWord(userChoice)} loses to ${convertToWord(computerChoice)}. You lost!`;
}

function draw(userChoice, computerChoice) {
  result_p.textContent = `${convertToWord(userChoice)} equals ${convertToWord(computerChoice)}. It's a draw.`;
}

function game(userChoice) {
  const computerChoice = getComputerChoice();
  switch (userChoice + computerChoice) {
    case "rs":
    case "pr":
    case "sp":
      win(userChoice, computerChoice);
      break;
    case "rp":
    case "ps":
    case "sr":
      lose(userChoice, computerChoice);
      break;
    case "rr":
    case "pp":
    case "ss":
      draw(userChoice, computerChoice);
      break;
  }
}

rock_div.addEventListener("click", () => game("r"));
paper_div.addEventListener("click", () => game("p"));
scissors_div.addEventListener("click", () => game("s"));

