## 1. NUMERIC REPRESENTATION

The decimal positional numbering system represents numbers using strings of Arabic numerals, optionally including a decimal point to separate whole and fractional portions of the number representation.
_(1 × 10^2) + (2 × 10^1) + (3 × 10^0) + (4 × 10^–1) + (5 × 10^–2) = 123.45_

To convert a binary value to decimal, add 2 **i** for each 1 in the binary string, where **i** is the zero-based position of the binary digit. For example, the binary value 11001010 2 represents:
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

Because assemblers vary widely, there are many different ways to represent binary literal constants in an assembly language program.
**MASM** represents binary values as a sequence of binary digits ( 0 and 1 ) ending with a b or B (_1001b_). HLA preﬁxes binary values with the percent symbol ( % ). To make
binary numbers more readable, HLA also allows you to insert underscores within binary strings like so (*%11_1011_0010_1101*).

Hexadecimal representation offers two great features: it’s very compact, and it’s easy to convert between binary and hexadecimal. Hexadecimal representation uses the letters A through F for the additional six digits it requires (above the 10 standard decimal digits, 0–9). (_234_, _DEAD_, _BEEF_, _0AFB_, _FEED_, _DEAF_).
One problem with hexadecimal representation is that it’s difﬁcult to differentiate hexadecimal values like “DEAD” from standard program identiﬁers.

| Binary    | Decimal     |  Hexadecimal |
|-----------|-------------|--------------|
|  00000000 |      0      |       0      |
|  00000001 |      1      |       1      |
|  00000010 |      2      |       2      |
|  00000011 |      3      |       3      |
|  00000100 |      4      |       4      |
|  00000101 |      5      |       5      |
|  00000110 |      6      |       6      |
|  00000111 |      7      |       7      |
|  00001000 |      8      |       8      |
|  00001001 |      9      |       9      |
|  00001010 |     10      |       A      |
|  00001011 |     11      |       B      |
|  00001100 |     12      |       C      |
|  00001101 |     13      |       D      |
|  00001110 |     14      |       E      |
|  00001111 |     15      |       F      |
|  00010000 |     16      |      10      |


To convert the hexadecimal representation of a number into binary, substitute the corresponding 4 bits for each hexadecimal digit. (_ABCD_ = _1010 1011 1100 1101_).

*1C = 0001_1100*

```javascript
/**
  @param {string} str
  @return {number}
  func('123') -> 123
*/

function myParseInt(str) {
  let int = 0;
  for (let i = 0; i < str.length; i++) {
    const asciiCode = str[i].charCodeAt();
    const digit = String.fromCharCode(asciiCode);
    int += digit;
  }
  return int * 10 / 10;
}
console.log(myParseInt('123')); //  123
console.log(myParseInt('20458')); //  20458
```

Most modern computer systems use an internal binary format torepresent values and other objects. However, most systems can only efficiently represent binary values of a given size. In order to write great code, you need to make sure that your programs use data objects that the machine can represent efficiently.

> The smallest unit of data on a binary computer is a single bit.

A byte is 8 bits and is the smallest addressable data item on many CPUs; that is, the CPU can efficiently retrieve data in groups of 8 bits from memory. For this reason, the smallest data type that many languages support consumes 1 byte of memory (regardless of the actual number of bits the data type requires).

A _word_ is deﬁned differently depending on the CPU: it may be a 16-bit, 32-bit, or 64-bit object.
