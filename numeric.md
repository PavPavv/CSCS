## 1. NUMERIC REPRESENTATION

The decimal positional numbering system represents numbers using strings of Arabic numerals, optionally including a decimal point to separate whole and fractional portions of the number representation.
_(1 × 10^2) + (2 × 10^1) + (3 × 10^0) + (4 × 10^–1) + (5 × 10^–2) = 123.45_

To convert a binary value to decimal, add 2 i for each 1 in the binary string, where i is the zero-based position of the binary digit. For example, the binary value 11001010 2 represents:
_(1 × 2 ^7) + (1 × 2^6) + (0 × 2^5) + (0 × 2^4) + (1 × 2^3) + (0 × 2^2) + (1 × 2^1) + (0 × 2^0) = 202_

```javascript
function fromDecToBin(num) {
  const result = [];

  function add(n){
    if (n % 2 === 0) {
      result.push(0);
    } else {
      result.push(1);
    }
    const next = parseInt(n / 2);
    if (next !== 0) {
      add(next);
    }
  }
  add(num);
  return +result.reverse().join('');
};

console.log(fromDecToBin(202)) //  11001010
```
