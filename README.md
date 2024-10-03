const express = require('express');
const bodyParser = require('body-parser');
const axios = require('axios');

const app = express();
app.use(bodyParser.json());

app.post('/webhook', (req, res) => {
    const message = req.body;

    // Proses pesan yang diterima
    console.log(message);

    // Kirim balasan
    const reply = {
        to: message.from,
        body: 'Hello! This is a response from sam bot.',
    };

    axios.post('https://api.whatsapp.com/v1/messages', reply)
        .then(response => {
            res.sendStatus(200);
        })
        .catch(error => {
            console.error(error);
            res.sendStatus(500);
        });
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
