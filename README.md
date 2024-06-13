const cron = require('node-cron');

// Define a simple task
const task = () => {
    const now = new Date();
    console.log(`Task executed at ${now}`);
};

// Schedule the task to run every minute
cron.schedule('* * * * *', task);

console.log('Cron job scheduled to run every minute.');