<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Simple Weather App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #4facfe, #00f2fe);
      color: #fff;
      text-align: center;
      padding: 50px;
    }

    .app {
      background: rgba(0,0,0,0.3);
      padding: 20px;
      border-radius: 10px;
      display: inline-block;
      min-width: 300px;
    }

    input {
      padding: 10px;
      width: 70%;
      border: none;
      border-radius: 5px;
      margin-bottom: 10px;
    }

    button {
      padding: 10px 15px;
      border: none;
      background: #fff;
      color: #333;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background: #ddd;
    }

    .weather {
      margin-top: 20px;
    }

    .temp {
      font-size: 40px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="app">
    <h2>🌤 Weather App</h2>
    <input type="text" id="city" placeholder="Enter city name">
    <br>
    <button onclick="getWeather()">Get Weather</button>

    <div class="weather" id="weather"></div>
  </div>

  <script>
    const apiKey = "YOUR_API_KEY_HERE"; // Replace with your OpenWeatherMap API key

    async function getWeather() {
      const city = document.getElementById("city").value;
      const weatherDiv = document.getElementById("weather");

      if (!city) {
        weatherDiv.innerHTML = "Please enter a city name.";
        return;
      }

      weatherDiv.innerHTML = "Loading...";

      try {
        const res = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`
        );

        if (!res.ok) throw new Error("City not found");

        const data = await res.json();

        weatherDiv.innerHTML = `
          <h3>${data.name}, ${data.sys.country}</h3>
          <div class="temp">${data.main.temp}°C</div>
          <p>${data.weather[0].description}</p>
          <p>Humidity: ${data.main.humidity}%</p>
          <p>Wind Speed: ${data.wind.speed} m/s</p>
        `;
      } catch (error) {
        weatherDiv.innerHTML = "Error fetching weather data.";
      }
    }
  </script>

</body>
</html>
