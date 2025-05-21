
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Казино</title>
  <style>
    body {
      background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      font-size: large;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      margin: 0;
      gap: 20px;
      transition: background 0.5s;
    }

    .button-container {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      justify-content: center;
    }

    button {
      padding: 15px 32px;
      font-size: 16px;
      border: none;
      cursor: pointer;
      border-radius: 8px;
      color: white;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
      transition: transform 0.2s, background-color 0.3s;
    }

    button:hover {
      transform: scale(1.05);
    }

    button#gambling {
      background-color: #4CAF50;
    }

    button#stopGambling {
      background-color: #f44336;
      display: none;
    }

    button#black {
      background-color: #222;
      display: none;
    }

    button#white {
      background-color: #e09;
      display: none;
    }

    #gifImage {
      display: none;
      max-width: 300px;
      border-radius: 15px;
      box-shadow: 0 0 20px rgba(0,0,0,0.3);
    }

    #result {
      display: none;
      padding: 10px 20px;
      background-color: white;
      border-radius: 10px;
      font-weight: bold;
      color: #222;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      text-align: center;
      font-size: 24px;
    }
  </style>
</head>
<body>

  <div class="button-container">
    <button id="gambling">Депнуть всё в казино</button>
    <button id="black">Ставка на чёрное</button>
    <button id="white">Ставка на белое</button>
    <button id="stopGambling">Остановить крутку</button>
  </div>

  <img id="gifImage" src="../shkola/8C5T.gif" alt="Анимация казино">
  <div id="result"></div>

  <script>
    const gamblingBtn = document.getElementById('gambling');
    const stopGamblingBtn = document.getElementById('stopGambling');
    const gifImage = document.getElementById('gifImage');
    const blackBtn = document.getElementById('black');
    const whiteBtn = document.getElementById('white');
    const resultBox = document.getElementById('result');

    let userChoice = null;
    let spinTimeout;

    function getRandomBit() {
      return Math.random() < 0.5 ? 0 : 1;
    }

    function playCasino(userBet) {
      gifImage.style.display = 'block';
      resultBox.style.display = 'none';
      stopGamblingBtn.style.display = 'block';
      blackBtn.style.display = 'none';
      whiteBtn.style.display = 'none';

      spinTimeout = setTimeout(() => {
        const result = getRandomBit();
        gifImage.style.display = 'none';
        stopGamblingBtn.style.display = 'none';
        gamblingBtn.style.display = 'inline-block';
        showResult(result === userBet);
      }, 2500);
    }

    function showResult(win) {
      resultBox.style.display = 'block';
      resultBox.textContent = win ? "🎉 Вы выиграли!" : "💀 Вы проиграли...";
      resultBox.style.color = win ? "#28a745" : "#c0392b";
    }

    gamblingBtn.addEventListener('click', () => {
      gamblingBtn.style.display = 'none';
      blackBtn.style.display = 'inline-block';
      whiteBtn.style.display = 'inline-block';
      resultBox.style.display = 'none';
    });

    blackBtn.addEventListener('click', () => {
      userChoice = 0;
      playCasino(userChoice);
    });

    whiteBtn.addEventListener('click', () => {
      userChoice = 1;
      playCasino(userChoice);
    });

    stopGamblingBtn.addEventListener('click', () => {
      clearTimeout(spinTimeout);
      gifImage.style.display = 'none';
      gamblingBtn.style.display = 'inline-block';
      stopGamblingBtn.style.display = 'none';
      resultBox.textContent = '⛔ Крутка остановлена';
      resultBox.style.color = '#555';
      resultBox.style.display = 'block';
    });
  </script>
</body>
</html>
