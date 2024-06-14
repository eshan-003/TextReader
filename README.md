const fetch = require('node-fetch');

const URL = 'https://jsonplaceholder.typicode.com/posts';

const getPosts = async () => {
    try {
        const response = await fetch(URL);
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const posts = await response.json();
        console.log('Posts:');
        posts.slice(0, 5).forEach(post => {
            console.log(`Title: ${post.title}`);
            console.log(`Body: ${post.body}`);
            console.log('---');
        });
    } catch (error) {
        console.error(`Error fetching posts: ${error.message}`);
    }
};

getPosts();