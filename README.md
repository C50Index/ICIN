# International Crypto Identification Number (ICIN)
The ICIN is a way to uniquelly identify cryptocurrencies.

With new cryptocurrencies popping up every day it is becoming more difficult to identify cryptocurrencies uniquely.  There needs to be a way to identify and categorize cryptocurriences.  


## What is it?
An 13 digit number to uniquely identify cryptocurrencies

# How it works
- 1-3 Sector
- 4-8 Coin Symbol
- 9 - Token Type 
- 10 - Supply
- 11 - Reserved for duplicates
- 12 - Reserved for duplicates
- 13 - Checksum digit

### Sector
The market sector determined by C50Index

## Token Type
0 - undefined
1 - Cryptocurrency
2 - Token

### Symbol
The first four digits of a cryptocurrency

### The Supply
- 0 = undefined
- 1 = 0 - 10 ^1 - 1
- 2 = (10 ^1) - (10^2-1)
- 3 = (10^2) - (10^2 -1)
- A = (10^10) - (10^10 - 1)
- Y = 10^25+
- Z = Uncapped

## Checksum Digit
13 - Checksum using the Luhn Algorithm https://en.wikipedia.org/wiki/Luhn_algorithm


## The Code
```javascript
    // Calculate the ICIN
    function ICIN(symbol, duplicates=0) {
      let result = "";
      
      // Add the first 4 character codes of a the symbol to the number
      for(let i = 0 ; i < symbol.length  && i < 4; i++) {
        result += symbol.charCodeAt(i);
      }
      // Add the number of duplicates
      result += duplicates;
      for(let i = result.length; i < 10; i++) {
        result+= (0);
      }
      let sum = 0;
      for(let i = 0; i < result.length; i++) {
        sum += Number(result[i]);
      }
    /* The check digit (x) is obtained by computing the sum of the non-check digits then computing 9 times that value modulo 10 */
      let check = (9 * sum) % 10;
      return result += check;
    }
```


