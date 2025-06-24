const app = document.querySelector('.weather-app');
const temp = document.querySelector('.temp');
const dateOutput = document.querySelector('.date');
const timeOutput = document.querySelector('.time');
const conditionOutput = document.querySelector('.condition');
const nameOutput = document.querySelector('.name');
const icon = document.querySelector('.icon');
const cloudOutput = document.querySelector('.cloud');
const humidityOutput = document.querySelector('.humidity');
const windOutput = document.querySelector('.wind');
const form = document.getElementById('locationInput');
const search = document.querySelector('.search');
const btn = document.querySelector('.submit');
const cities = document.querySelectorAll('.city');

let cityInput = "Chennai";

cities.forEach((city) => {
  city.addEventListener('click', (e) => {
    cityInput = e.target.innerHTML;
    fetchWeatherData();
    app.style.opacity = "0";
  });
});

form.addEventListener('submit', (e) => {
  e.preventDefault();
  if (search.value.length === 0) {
    alert('Please type the city name');
  } else {
    cityInput = search.value;
    fetchWeatherData();
    search.value = "";
    app.style.opacity = "0";
  }
});

function dayofTheWeek(day, month, year) {
  const weekday = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
  const formattedDate = `${year}-${month}-${day}`;
  return weekday[new Date(formattedDate).getDay()];
}

function fetchWeatherData() {
  fetch(`https://api.weatherapi.com/v1/current.json?key=09c6eee4a79f4b43a1b104807252406&q=${cityInput}`)
    .then(response => response.json())
    .then(data => {
      console.log(data);

      temp.innerHTML = `${data.current.temp_c}&#176;`;
      conditionOutput.innerHTML = data.current.condition.text;

      const date = data.location.localtime;
      const y = parseInt(date.substr(0, 4));
      const m = parseInt(date.substr(5, 2));
      const d = parseInt(date.substr(8, 2));
      const time = date.substr(11);

      dateOutput.innerHTML = `${dayofTheWeek(d, m, y)} ${d}/${m}/${y}`;
      timeOutput.innerHTML = time;
      nameOutput.innerHTML = data.location.name;

      // Use full URL for icon
      icon.src = "https:" + data.current.condition.icon;

      cloudOutput.innerHTML = `${data.current.cloud}%`;
      humidityOutput.innerHTML = `${data.current.humidity}%`;
      windOutput.innerHTML = `${data.current.wind_kph}km/h`;

      let timeOfDay = data.current.is_day ? "day" : "night";
      const code = data.current.condition.code;

      // Set background using Unsplash images
      if (code === 1000) {
        app.style.backgroundImage = `url('https://source.unsplash.com/1600x900/?clear-sky,${timeOfDay}')`;
        btn.style.background = timeOfDay === "day" ? "#e5ba92" : "#181e27";
      } else if (
        [1003, 1006, 1009, 1030, 1069, 1087, 1135, 1273, 1276, 1279, 1282].includes(code)
      ) {
        app.style.backgroundImage = `url('https://source.unsplash.com/1600x900/?cloudy,${timeOfDay}')`;
        btn.style.background = timeOfDay === "day" ? "#fa6d1b" : "#181e27";
      } else if (
        [1063, 1069, 1072, 1150, 1153, 1180, 1183, 1186, 1189, 1192, 1195, 1204, 1207, 1240, 1243, 1246, 1249, 1252].includes(code)
      ) {
        app.style.backgroundImage = `url('https://source.unsplash.com/1600x900/?rain,${timeOfDay}')`;
        btn.style.background = timeOfDay === "day" ? "#647d75" : "#325c80";
      } else {
        app.style.backgroundImage = `url('https://source.unsplash.com/1600x900/?snow,${timeOfDay}')`;
        btn.style.background = timeOfDay === "day" ? "#4d72aa" : "#1b1b1b";
      }

      app.style.opacity = "1";
    })
    .catch(() => {
      alert("City not found, please try again");
      app.style.opacity = "1";
    });
}

// Initial call
fetchWeatherData();
