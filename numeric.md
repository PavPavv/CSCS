## 1. NUMERIC REPRESENTATION

## Numbering systems

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

## Numeric/string conversions

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

Most modern computer systems use an internal binary format to represent values and other objects. However, most systems can only efficiently represent binary values of a given size. In order to write great code, you need to make sure that your programs use data objects that the machine can represent efficiently.

> The smallest unit of data on a binary computer is a single bit.

A "nibble" is a collection of 4 bits. Most computer systems don’t provide efﬁcient access to nibbles in memory. Notably, it takes exactly 1 nibble to represent a single hexadecimal digit.

A byte is 8 bits and is the smallest addressable data item on many CPUs; that is, the CPU can efficiently retrieve data in groups of 8 bits from memory. For this reason, the smallest data type that many languages support consumes 1 byte of memory (regardless of the actual number of bits the data type requires).

A "word"_" is deﬁned differently depending on the CPU: it may be a 16-bit, 32-bit, or 64-bit object:

- 0 - bit
- 0000 - "nibble" (precise hexadecimal digit)
- 0000_0000 - 8-bit "word" (1 byte)
- 0000_0000_0000_0000 - 16-bit "word"
- 0000_0000_0000_0000_0000_0000_0000_0000 - 32-bit "word"
- 0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000 - 64-bit "word"


As noted, most CPUs efﬁciently handle objects up to a certain size (typically 32 or 64 bits on contemporary systems). That doesn’t mean you can’t work with larger objects, only that it’s less efﬁcient to do so.
In general, with an n-bit string you can represent up to 2 n different values.

|   Size of bit string  |  Number of possible combinations (2 n )                   |
|-----------------------|-----------------------------------------------------------|
| 1                     | 2                                                         |
| 4                     | 16                                                        |
| 8                     | 256                                                       |
| 16                    | 65,536                                                    |
| 32                    | 4,294,967,296                                             |
| 64                    | 18,446,744,073,709,551,616                                |
| 128                   | 340,282,366,920,938,463,463,374,607,431,768,211,456       |

The two’s complement system uses the HO (high order) bit as a sign bit.

## Signed and Unsigned Numbers

What about negative numbers? To represent signed values, most computer systems use the two’s complement numbering system.
With n bits, we can represent only 2^n different objects.
In general, with n bits we can represent the signed values in the range *–2^(n–1) to +2^(n–1) – 1*.
The two’s complement system uses the HO bit as a sign bit. If the HO bit is 0 , the number is non-negative and has the usual binary encoding; if the HO bit is 1 , the number is negative and uses the two’s complement encoding.

To negate a number, you can use the two’s complement operation as follows:

1. Invert all the bits in the number; that is, change all the 0 s to 1 s and vice versa.
2. Add 1 to the inverted result (ignoring any overﬂow).

### Useful Properties of Binary Numbers:

- If bit position 0 of a binary (integer) value contains 1 , the number is an odd number; if this bit contains 0 , then the number is even.
- If the LO n bits of a binary number all contain 0 , then the number is evenly divisible by 2 n .
- If a binary value contains a 1 in bit position n , and 0 s everywhere else, then that number is equal to 2 n .
- If a binary value contains all 1 s from bit position 0 up to (but not including) bit position n , and all other bits are 0 , then that value is equal to 2 n – 1.
- Shifting all the bits in a number to the left by one position multiplies the binary value by 2.
- Shifting all the bits of an unsigned binary number to the right by one position effectively divides that number by 2 (this does not apply to signed integer values). Odd numbers are rounded down.
- Multiplying two n -bit binary values together may require as many as 2 × n bits to hold the result.
- Adding or subtracting two n -bit binary values never requires more than n + 1 bits to hold the result.Inverting all the bits in a binary number (that is, changing all the 0 s to 1 s and vice versa) is the same thing as negating (changing the sign) of the value and then subtracting 1 from the result.
- Incrementing (adding 1 to) the largest unsigned binary value for a given number of bits always produces a value of 0 .
- Decrementing (subtracting 1 from) 0 always produces the largest unsigned binary value for a given number of bits.
- An n -bit value provides 2 n unique combinations of those bits.
- The value 2 n –1 contains n bits, each containing the value.

|   n  |    2^n  |
|------|---------|
|0     |  1      |
| 1    |  2      |
| 2    |  4      |
| 3    |  8      |
| 4    |  16     |
| 5    |  32     |
| 6    |  64     |
| 7    |  128    |
| 8    |  256    |
| 9    |  512    |
| 10   | 1,024   |
| 11   | 2,048   |
| 12   | 4,096   |
| 13   | 8,19214 |
| 14   | 16,384  |
| 15   | 32,768  |
| 16   | 65,536  |

## Sign Extension, Zero Extension, and Contraction

Binary Coded Decimals (BCD)

## Fixed-Point Representation

FPU - Floating Point Unit.
There are two ways computer systems commonly represent numbers with fractional components: ﬁxed-point representation and ﬂoating-point representation.
Adding more bits to the fractional component of your ﬁxed-point number will give you a more accurate approximation of this value.
In a ﬁxed-point binary numbering system, there are certain values you can never accurately represent regardless of how many bits you add to the fractional part of your ﬁxed-point representation.

## Scaled Numeric Formats

One big problem with the fractional representations we’ve seen is thatthey provide a close approximation, but not an exact representation, for all rational values. For example, in binary or decimal you cannot exactly represent the value 1 / 3 . You could switch to a ternary (base-3) numbering system and exactly represent 1 / 3 , but then you wouldn’t be able to exactly represent fractional values like 1 / 2 or 1 / 10 . We need a numbering system that can represent any rational fractional value.

## Rational Representation

Rational representation uses pairs of integers to represent fractional values. One integer represents the numerator ( n ) of a fraction, and the other represents the denominator ( d ).

## BINARY ARITHMETIC AND BIT OPERATIONS