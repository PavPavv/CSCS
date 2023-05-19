# 3. FLOATING-POINT REPRESENTATION

## Introduction to Floating-Point Arithmetic

There is an infinite number of possible real values. Floating-point representation uses a **finite** number of bits and, therefore, can represent a **finite** number of different values!! When a given floating-point format cannot exactly represent some real value, **the closest value that the format can exactly represent is used**.
Fixed-point formats represent fractional values, but at the expense of the range of integer values they can represent. This problem, which the floating-point format solves, is one of _dynamic range_.

You cannot exactly represent as many different values with a floating- point format as with an integer format because the floating-point format encodes multiple representations (that is, different bit patterns) for the same value.

The lack of precision (the number of digits or bits maintained in a computation) affects the accuracy (the correctness of the computation).
To improve the accuracy, we use extra digits during the calculation. These extra digits are known as guard digits (or guard bits in the case of a binary format). They greatly enhance accuracy during a long chain of computations.

> Whenever subtracting two numbers with the same signs or adding two numbers with different signs, the accuracy of the result may be less than the precision available in the floating- point format.
> When performing a chain of calculations involving addition, subtraction, multiplication, and division, perform the multiplication and division operations first.

x × ( y + z ) ---> x × y + x × z

When you multiply two very large or very small numbers, _overflow_ or _underflow_ may occur.

> Never compare two floating-point values to see if they are equal!

Two seemingly equivalent floating-point computations will not necessarily produce exactly equal results, a straight comparison for equality—which succeeds if and only if all bits (or digits) in the two operands are the same — may fail.

## IEEE (Institute of Electrical and Electronics Engineers) Floating-Point Formats

When Intel planned to introduce a floating-point unit (FPU) for its original 8086 microprocessor, they created a format which is became IEEE Std 754 floating-point format.

To handle a wide range of performance and accuracy requirements, Intel actually introduced three floating-point formats:

- single precision
- double precision
- and extended precision

The single- and double- precision formats corresponded to C **float** and **double** types.
Extended precision contains 16 extra bits that long chains of computations can use as guard bits before rounding down to a double-precision value when storing the result.

### Single-Precision Floating-Point Format

The single-precision format uses a 24-bit mantissa and an 8-bit exponent (with 1 bit for a sign if it signed).

0_000_0000\_\_\_\_1000_0000_0000_0000_0000_0000

- 1 sign bit
- 7 bits for exponent
- always 1
- 23 bits for mantissa

One’s complement has the unusual property that there are two representations for 0 (with the sign bit set or clear).

> Although there is an infinite number of values between 1 and 2, we can represent only 8 million (2^23 ) of them because we use a 23-bit mantissa (the 24th bit is always 1 ), and therefore have only 23 bits of precision.

### Double-Precision Floating-Point Format

The double-precision format helps overcome the problems of the single-precision floating-point.

0_000_0000_0000\_\_\_\_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000

- 1 sign bit
- 11 bits for exponent
- 53 bits for mantissa

### Extended-Precision Floating-Point Format

0_000_0000_0000_0000\_\_\_\_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000

- 1 sign bit
- 15 bits for exponent
- 64 bits for mantissa

### Quad-Precision Floating-Point Format

0_000_0000_0000_0000\_\_\_\_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000_0000

- 1 sign bit
- 15 bits for exponent
- 112 bits for mantissa

### Normalization and Denormalized Values

To maintain maximum precision during floating-point computations, most computations use normalized values. A normalized floating-point value is one whose HO mantissa bit contains 1.
You can normalize almost any unnormalized value by shifting the mantissa bits to the left and decrementing the exponent until a 1 appears in the mantissa’s HO bit.

### Rounding

During a calculation, floating-point arithmetic functions may produce a result with greater precision than the floating-point format supports (the guard bits in the calculation maintain this extra precision).

Traditionally, floating-point software and hardware use one of four different ways to round values: truncation, rounding up, rounding down, or rounding to nearest.

### Special Floating-Point Values

If the exponent contains all 1 s and the mantissa is nonzero (discounting the implied bit), then the HO bit of the mantissa (again discounting the implied bit) determines whether the value represents a **quiet not-a-number (QNaN)** or a **signaling not-a-number (SNaN)**. These **not-a-number (NaN)** results tell the system that some serious miscalculation has taken place and that the result of the calculation is completely undefined. **QNaNs** represent indeterminate results, while **SNaNs** specify that an invalid operation has taken place. Note that the sign bit is irrelevant for **NaN**s.

Two other special values are represented when the exponent contains all 1 bits, and the mantissa contains all 0s. In such a case, the sign bit determines whether the result is the representation for **+infinity** or **-infinity** .

Finally, if the exponent bits are all 0 , the sign bit indicates which of the two special values, –0 or +0, the floating-point number represents.
Because the floating-point format uses a one’s complement notation, there are two separate representations for 0. Note that with respect to comparisons, arithmetic, and other operations, +0 is equal to –0.

Intel recommends using the sign bit to indicate that 0 was produced via underflow of a negative value (with the sign bit set) or underflow of a positive number (with the sign bit clear).

### Floating-Point Exceptions

The IEEE floating-point standard defines certain degenerate conditions under which the floating-point processor (or software-implemented floating-point code) should notify the application software. These exceptional conditions include the following:

- Invalid operation
- Division by zero
- Denormalized operand
- Numeric overflow
- Numeric underflow
- Inexact result

### Floating-Point Operations

#### Floating-Point Addition and Subtraction

Addition and subtraction use essentially the same code. After all, computing X - Y is equivalent to computing X + (- Y) . If we can add a negative number to some other value, then we can also perform subtraction by first negating some number and then adding it to another value. And because the IEEE floating-point format uses the one’s complement representation, negating a value is trivial—we just invert the sign bit.

#### Floating-Point Multiplication

#### Floating-Point Division

Floating-point division is a little bit more involved than multiplication because the IEEE ﬂoating-point standard says many things about degenerate conditions that can occur during division.
