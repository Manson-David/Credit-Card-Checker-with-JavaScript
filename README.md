# 🔍 Credit Card Checker (JavaScript)

A simple JavaScript project that validates credit card numbers using the **Luhn Algorithm**.  
It identifies invalid cards and determines which companies issued them.

This project is part of a JavaScript learning challenge and helps practice working with arrays, loops, and logic.

---

## 📌 Features

- Validate credit card numbers using the Luhn algorithm  
- Detect invalid card numbers in a dataset  
- Identify card companies (Visa, Mastercard, Amex, Discover)  
- Works with nested arrays of card numbers  
- Fully written in JavaScript (no libraries needed)

---

## 📁 Project Structure

credit-card-checker/
│── index.js
│── README.md

yaml
Copy code

---

## 🧠 How the Luhn Algorithm Works

The Luhn algorithm is used to verify whether a credit card number is valid:

1. Start from the second-to-last digit and move left.
2. Double every other digit.
3. If the result is greater than 9, subtract 9.
4. Add all digits together.
5. If the total modulo 10 equals 0, the card is **valid**; otherwise, it’s **invalid**.

---

## 🧩 Functions Explained

### 1️⃣ `validateCred(arr)`
Validates a single credit card number.

```js
const validateCred = (arr) => {
  let digits = arr.slice();
  for (let i = digits.length - 2; i >= 0; i -= 2) {
    digits[i] *= 2;
    if (digits[i] > 9) digits[i] -= 9;
  }
  const sum = digits.reduce((acc, val) => acc + val, 0);
  return sum % 10 === 0;
};
2️⃣ findInvalidCards(nestedArr)
Returns all invalid credit cards from a nested array.

js
Copy code
const findInvalidCards = (nestedArr) => {
  let invalidCards = [];
  for (let card of nestedArr) {
    if (!validateCred(card)) invalidCards.push(card);
  }
  return invalidCards;
};
3️⃣ idInvalidCardCompanies(invalidCards)
Identifies companies that issued invalid cards based on the first digit:

First Digit	Company
3	Amex
4	Visa
5	Mastercard
6	Discover

js
Copy code
const idInvalidCardCompanies = (invalidCards) => {
  let companies = [];
  for (let card of invalidCards) {
    switch(card[0]) {
      case 3:
        if (!companies.includes("Amex")) companies.push("Amex");
        break;
      case 4:
        if (!companies.includes("Visa")) companies.push("Visa");
        break;
      case 5:
        if (!companies.includes("Mastercard")) companies.push("Mastercard");
        break;
      case 6:
        if (!companies.includes("Discover")) companies.push("Discover");
        break;
      default:
        console.log("Company not found");
    }
  }
  return companies;
};
🧪 Example Usage
js
Copy code
const invalidCards = findInvalidCards(batch);

console.log("Invalid cards:", invalidCards);
console.log("Companies that issued invalid cards:", idInvalidCardCompanies(invalidCards));
Example Output:

less
Copy code
Invalid cards: [ [4,5,3,2,...], [5,7,9,5,...], ... ]
Companies that issued invalid cards: [ 'Visa', 'Mastercard', 'Amex', 'Discover' ]
🚀 Run the Program
Make sure Node.js is installed, then run:

bash
Copy code
node index.js
📜 License
This project is open-source and free to use.
