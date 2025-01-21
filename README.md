const axios = require('axios');
const yargs = require('yargs');

const API_URL = 'https://api.exchangerate-api.com/v4/latest/USD';

async function fetchExchangeRate() {
    try {
        const response = await axios.get(API_URL);
        const rates = response.data.rates;
        return {
            USD_TO_INR: rates.INR,
            INR_TO_USD: 1 / rates.INR,
        };
    } catch (error) {
        console.error('Error fetching exchange rates:', error.message);
        process.exit(1);
    }
}

async function convertCurrency(amount, from, to) {
    const rates = await fetchExchangeRate();
    let convertedAmount;
# currency-converter
