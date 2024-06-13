const cron = require('node-cron');
const axios = require('axios');

// OpenWeatherMap API setup
const API_KEY = 'your_openweathermap_api_key';
const CITY = 'London';
const URL = `http://api.openweathermap.org/data/2.5/weather?q=${CITY}&appid=${API_KEY}`;

const fetchWeatherData = async () => {
    try {
        const response = await axios.get(URL);
        const data = response.data;

        const weatherInfo = {
            city: data.name,
            temperature: (data.main.temp - 273.15).toFixed(2), // Convert from Kelvin to Celsius
            weather: data.weather[0].description,
            date: new Date().toLocaleString()
        };

        console.log(`Weather data fetched at ${weatherInfo.date}`);
        console.log(`City: ${weatherInfo.city}`);
        console.log(`Temperature: ${weatherInfo.temperature}°C`);
        console.log(`Weather: ${weatherInfo.weather}`);
    } catch (error) {
        console.error('Error fetching weather data:', error);
    }
};

// Schedule the task to run every hour
cron.schedule('0 * * * *', fetchWeatherData);

console.log('Cron job scheduled to fetch weather data every hour.');