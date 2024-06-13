const cron = require('node-cron');
const axios = require('axios');

// Dog CEO's Dog API URL
const URL = 'https://dog.ceo/api/breeds/image/random';

const fetchDogImage = async () => {
    try {
        const response = await axios.get(URL);
        const data = response.data;

        console.log(`Fetched dog image at ${new Date().toLocaleString()}`);
        console.log(`Image URL: ${data.message}`);
    } catch (error) {
        console.error('Error fetching dog image:', error);
    }
};

// Schedule the task to run every 5 minutes
cron.schedule('*/5 * * * *', fetchDogImage);

console.log('Cron job scheduled to fetch a dog image every 5 minutes.');