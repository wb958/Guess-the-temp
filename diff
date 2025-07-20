<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Guess the Temp</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="manifest" href="manifest.json" />
  <style>
    body { font-family: sans-serif; padding: 2rem; max-width: 480px; margin: auto; }
    h1 { font-size: 1.5rem; }
    input, button { font-size: 1rem; padding: 0.5rem; }
    #result { margin-top: 1rem; }
  </style>
</head>
<body>
  <h1>🌍 Guess the Temp!</h1>
  <p>City: <strong id="city">Loading...</strong></p>
  <p>Your guess (°C): <input type="number" id="guess" /><button id="check">Check</button></p>
  <div id="result"></div>
  <script>
    const cities = ["Tokyo", "Paris", "Nairobi", "Sydney", "New York", "Reykjavik", "Mumbai", "London", "Moscow", "Rio de Janeiro"];
    const apiKey = "4625efdcd57bb3f56d7b1cec93150d6b"; // ← Replace with your Met Office or OpenWeatherMap API key
    let actualTemp;

    function pickCityAndFetch() {
      const city = cities[Math.floor(Math.random() * cities.length)];
      document.getElementById("city").textContent = city;
      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`)
        .then(res => res.json())
        .then(data => {
          actualTemp = Math.round(data.main.temp);
        })
        .catch(e => document.getElementById("result").textContent = "Error getting temp.");
    }

    function checkGuess() {
      const guess = Number(document.getElementById("guess").value);
      if (isNaN(guess)) return alert("Please enter a number!");
      const diff = Math.abs(guess - actualTemp);
      const points = Math.max(0, 5 - diff);
      const msg = diff === 0
        ? `🎉 Perfect! It's ${actualTemp}°C — you get 5 points!`
        : `You guessed ${guess}°C, actual is ${actualTemp}°C. You get ${points} point${points === 1 ? "" : "s"}.`;
      document.getElementById("result").textContent = msg;
      document.getElementById("check").disabled = true;
    }

    document.getElementById("check").onclick = checkGuess;
    pickCityAndFetch();
  </script>
</body>
</html>
