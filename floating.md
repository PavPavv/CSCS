# 4. FLOATING-POINT REPRESENTATION

## Introduction to Floating-Point Arithmetic

There is an infinite number of possible real values. Floating-point representation uses a finite number of bits and, therefore, can represent a finite number of different values. When a given floating-point format cannot exactly represent some real value, the closest value that the format can exactly represent is used.
Fixed-point formats represent fractional values, but at the expense of the range of integer values they can represent. This problem, which the floating-point format solves, is one of _dynamic range_.

You cannot exactly represent as many different values with a floating- point format as with an integer format because the floating-point format encodes multiple representations (that is, different bit patterns) for the same value.

The lack of precision (the number of digits or bits maintained in a computation) affects the accuracy (the correctness of the computation).
To improve the accuracy, we use extra digits during the calculation. These extra digits are known as guard digits (or guard bits in the case of a binary format). They greatly enhance accuracy during a long chain of computations.

> Whenever subtracting two numbers with the same signs or adding two numbers with different signs, the accuracy of the result may be less than the precision available in the floating- point format.
> When performing a chain of calculations involving addition, subtraction, multiplication, and division, perform the multiplication and division operations first.

x × ( y + z ) ---> x × y + x × z

When you multiply two very large or very small numbers, _overflow_ or _underflow_ may occur.

> Never compare two floating-point values to see if they are equal.

Two seemingly equivalent floating-point computations will not necessarily produce exactly equal results, a straight comparison for equality—which succeeds if and only if all bits (or digits) in the two operands are the same—may fail.

## IEEE Floating-Point Formats

When Intel planned to introduce a floating-point unit (FPU) for its original 8086 microprocessor, they created a format which is became  IEEE Std 754 floating-point format.

To handle a wide range of performance and accuracy requirements, Intel actually introduced three floating-point formats:

- single precision
- double precision
- and extended precision

The single- and double- precision formats corresponded to C’s **float** and **double** types.
Extended precision contains 16 extra bits that long chains of computations can use as guard bits before rounding down to a double-precision value when storing the result.

### Single-Precision Floating-Point Format

The single-precision format uses a 24-bit mantissa and an 8-bit exponent.

0_000_0000____1000_0000_0000_0000_0000_0000

- sign bit
- 7 bits for exponent
- always 1
- 23 bits for mantissa

One’s complement has the unusual property that there are two representations for 0 (with the sign bit set or clear).

> Although there is an infinite number of values between 1 and 2, we can represent only 8 million (2 23 ) of them because we use a 23-bit mantissa (the 24th bit is always 1 ), and therefore have only 23 bits of precision.

### Double-Precision Floating-Point Format
