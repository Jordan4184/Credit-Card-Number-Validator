# Credit Card Validator

## Overview

This project provides functions to validate credit card numbers using the Luhn algorithm, identify invalid card numbers from a batch, and determine the issuing companies of those invalid cards.

## Features

1. **Validate Credit Card Numbers**: Uses the Luhn algorithm to check if a credit card number is valid.
2. **Find Invalid Credit Card Numbers**: Scans a batch of credit card numbers and returns those that are invalid.
3. **Identify Issuing Companies of Invalid Cards**: Determines the companies that issued the invalid credit card numbers.

## Code Details

### Valid and Invalid Credit Card Numbers

The code includes predefined arrays of valid and invalid credit card numbers:

- `valid1`, `valid2`, `valid3`, `valid4`, `valid5`: Arrays of valid credit card numbers.
- `invalid1`, `invalid2`, `invalid3`, `invalid4`, `invalid5`: Arrays of invalid credit card numbers.
- `mystery1`, `mystery2`, `mystery3`, `mystery4`, `mystery5`: Arrays that could be either valid or invalid.
- `batch`: An array containing all the above arrays.

### Functions

#### 1. `validateCred(arr)`

Validates a credit card number using the Luhn algorithm.

- **Parameters**: `arr` - An array of numbers representing the credit card number.
- **Returns**: `true` if the credit card number is valid, `false` otherwise.

```javascript
const validateCred = (arr) => {
    let sum = 0;
    let double = false;

    for (let i = arr.length - 1; i >= 0; i--) {
        let digit = arr[i];

        if (double) {
            digit *= 2;
            if (digit > 9) {
                digit -= 9;
            }
        }

        sum += digit;
        double = !double;
    }
    return sum % 10 === 0;
};
```

#### 2. `isValid(arr)`

Returns a message indicating whether a credit card number is valid.

- **Parameters**: `arr` - An array of numbers representing the credit card number.
- **Returns**: `'Credit Card is Valid'` if valid, `'Credit Card is Invalid'` if invalid.

```javascript
const isValid = (arr) => {
    return validateCred(arr) ? 'Credit Card is Valid' : 'Credit Card is Invalid';
};
```

#### 3. `findInvalidCards(cards)`

Identifies invalid credit card numbers from a batch.

- **Parameters**: `cards` - An array of credit card number arrays.
- **Returns**: An array of invalid credit card numbers.

```javascript
function findInvalidCards(cards) {
    const invalid = [];

    for (let i = 0; i < cards.length; i++) {
        let currCred = cards[i];
        if (!validateCred(currCred)) {
            invalid.push(currCred);
        }
    }

    return invalid;
}
```

#### 4. `idInvalidCardCompanies(invalidBatch)`

Identifies the issuing companies of invalid credit card numbers.

- **Parameters**: `invalidBatch` - An array of invalid credit card number arrays.
- **Returns**: An array of company names that issued the invalid credit cards.

```javascript
function idInvalidCardCompanies(invalidBatch) {
    const companies = [];
    for (let i = 0; i < invalidBatch.length; i++) {
        switch (invalidBatch[i][0]) {
            case 3:
                if (companies.indexOf('Amex') === -1) {
                    companies.push('Amex');
                }
                break;
            case 4:
                if (companies.indexOf('Visa') === -1) {
                    companies.push('Visa');
                }
                break;
            case 5:
                if (companies.indexOf('Mastercard') === -1) {
                    companies.push('Mastercard');
                }
                break;
            case 6:
                if (companies.indexOf('Discover') === -1) {
                    companies.push('Discover');
                }
                break;
            default:
                console.log('Company not found');
        }
    }
    return companies;
}
```

## Usage Example

```javascript
// Validate a credit card number
console.log(isValid(valid1)); // Output: 'Credit Card is Valid'

// Find invalid credit card numbers in a batch
const invalidCards = findInvalidCards(batch);
console.log(invalidCards); // Output: Array of invalid credit card numbers

// Identify the companies that issued the invalid credit cards
const companies = idInvalidCardCompanies(invalidCards);
console.log(companies); // Output: Array of company names
```