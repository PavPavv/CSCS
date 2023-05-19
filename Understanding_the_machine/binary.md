# 3. BINARY ARITHMETIC AND BIT OPERATIONS

## Adding Binary Values

- 0 + 0 = 0
- 0 + 1 = 1
- 1 + 0 = 1
- 1 + 1 = 0 with carry
- Carry + 0 + 0 = 1
- Carry + 0 + 1 = 0 with carry
- Carry + 1 + 0 = 0 with carry
- Carry + 1 + 1 = 1 with carry

## Subtracting Binary Values

- 0 – 0 = 0
- 0 – 1 = 1 with a borrow
- 1 – 0 = 1
- 1 – 1 = 0
- 0 – 0 – borrow = 1 with a borrow
- 0 – 1 – borrow = 0 with a borrow
- 1 – 0 – borrow = 0
- 1 – 1 – borrow = 1 with a borrow

## Multiplying Binary Values

- 0 × 0 = 0
- 0 × 1 = 0
- 1 × 0 = 0
- 1 × 1 = 1

## Dividing Binary Values

## Logical Operations on Bits

There are four main logical operations we’ll need to perform on hexadecimal and binary numbers: **AND**, **OR**, **XOR** (exclusive-or), and **NOT**.
The logical **AND**, **OR**, and **XOR** operations accept two single-bit operands and compute the following results in the **truth tables**:

- 0 and 0 = 0
- 0 and 1 = 0
- 1 and 0 = 0
- 1 and 1 = 1

- 0 or 0 = 0
- 0 or 1 = 1
- 1 or 0 = 1
- 1 or 1 = 1

- 0 xor 0 = 0
- 0 xor 1 = 1
- 1 xor 0 = 1
- 1 xor 1 = 0

## Logical Operations on Binary Numbers and Bit Strings

Because most programming languages manipulate groups of 8, 16, 32, or 64 bits, we need to extend the deﬁnition of these logical operationsbeyond single-bit operands to operate on a bit-by-bit (or bitwise ) basis.

This bit-by-bit execution applies to the other logical operations as well. The ability to force bits to 0 or 1 using the logical **AND** and **OR** operations, and to invert bits using the logical **XOR** operation, is very important when you’re working with strings of bits (such as binary numbers). These operations let you selectively manipulate certain bits within a value while leaving other bits unaffected.

Manipulating bit strings with the logical **AND**, **OR**, and **XOR** operations is known as _masking_ .

## Useful Bit Operations

### Testing Bits in a Bit String Using AND

```c++
IsOdd = (ValueToTest & 1) != 0;
```

### Testing a Set of Bits for Zero/Not Zero Using AND

You can also use the bitwise **AND** operator to see if all bits in a set are 0.

```c++
IsDivisibleBy16 := (ValueToTest and $f) = 0;
```

### Shifts and Rotates

These functions can be further broken down into _shift lefts_, _rotate lefts_, _shift rights_, and _rotate rights_.

In the C-language family _shift left_ operator is **<<**. Shifting the binary representation of a number one position to the left is equivalent to multiplying that value by 2.

A _shift right_ operation is similar to a _shift left_, except we move the data in the opposite direction. Bit 7 moves into bit 6, bit 6 moves into bit 5, bit 5 moves into bit 4, and so on. During a _shift right_, we’ll move a 0 into bit 7, and bit 0 will be the carry out of the operation. C, C++, C#, Swift, and Java use the **>>** operator for a _shift right_ operation. Shifting an unsigned binary value one position to the right divides that value by 2.

## Bit Fields and Packed Data

CPUs generally operate most efficiently on byte, word, double-word and quad-word data types, 4 but occasionally you’ll need to work with a data type whose size is something other than 8, 16, 32, or 64 bits. In such cases, you may be able to save some memory by packing different strings of bits together as compactly as possible, without wasting any bits to align a particular data ﬁeld on a byte or other boundary.

## Packing and Unpacking Data

The advantage of packed data types is efficient memory use.
Encoding an SSN using three separate (32-bit) integers takes 12 bytes. That’s more than the 11 bytes needed to represent the number using an array of characters. A better solution is to encode each ﬁeld using short (16-bit) integers. Now it takes only 6 bytes to represent the SSN.

Fields that begin at bit position 0 in a packed data object can be accessed most efficiently, so you should arrange the ﬁelds in your packed data type such that the ﬁeld you access most often 6 begins at bit 0.

Assuming the data you want to insert appears in some variable and contains 0 s in the unused bits, inserting a ﬁeld into a packed object requires three operations. First, if necessary, you shift the ﬁeld’s data to the left so its alignment matches the corresponding ﬁeld in the packed object. Next, clear the corresponding bits in the packed structure, then logically OR the shifted ﬁeld into the packed object.

Here’s the C/C++/Swift code that accomplishes the operation shown in Figure 3-10:

```c++
packedValue = (packedValue & 0xFFc000FF) | (ThirdField << 8 );
```
