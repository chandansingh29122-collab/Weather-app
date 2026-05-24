<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Weather app</title>

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family:Arial, sans-serif;
    }

    body{
      height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      background:linear-gradient(135deg,#4facfe,#00f2fe);
    }

    .container{
      width:350px;
      background:#fff;
      padding:25px;
      border-radius:20px;
      text-align:center;
      box-shadow:0 10px 20px rgba(0,0,0,0.2);
    }

    h1{
      margin-bottom:20px;
      color:#333;
    }

    .search-box{
      display:flex;
      gap:10px;
      margin-bottom:20px;
    }

    input{
      flex:1;
      padding:10px;
      border:2px solid #ddd;
      border-radius:10px;
      outline:none;
      font-size:16px;
    }

    button{
      padding:10px 15px;
      border:none;
      background:#4facfe;
      color:white;
      border-radius:10px;
      cursor:pointer;
      font-size:16px;
    }

    button:hover{
      background:#2196f3;
    }

    .weather-box{
      display:none;
    }

    .weather-box img{
      width:100px;
    }

    .temp{
      font-size:40px;
      margin:10px 0;
      color:#333;
    }

    .city{
      font-size:28px;
      color:#555;
    }

    .description{
      font-size:18px;
      color:#777;
      margin-top:10px;
      text-transform:capitalize;
    }

    .error{
      color:red;
      margin-top:10px;
      display:none;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Weather App</h1>

  
  <script>
    const apiKey = "627d76291e9edb6b6b47f18d61d8ea03";

    async function getWeather() {

      const cityInput = document.getElementById("cityInput").value;

      const weatherBox = document.getElementById("weatherBox");
      const error = document.getElementById("error");

      if(cityInput === ""){
        return;
      }

      const url = `https://api.openweathermap.org/data/2.5/weather?q=${cityInput}&units=metric&appid=${apiKey}`;

      const response = await fetch(url);

      const data = await response.json();

      if(data.cod === "404"){
        error.style.display = "block";
        weatherBox.style.display = "none";
        return;
      }

      error.style.display = "none";
      weatherBox.style.display = "block";

      document.getElementById("temp").innerHTML = `${Math.round(data.main.temp)}°C`;

      document.getElementById("city").innerHTML = data.name;

      document.getElementById("description").innerHTML = data.weather[0].description;

      document.getElementById("icon").src =
      `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
    }
  </script>

</body>
</html>
