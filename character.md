# 4. CHARACTER REPRESENTATION

The term character refers to a human-or machine-readable symbol that is typically a non-numeric entity. In addition to alphabetic characters, character
data includes punctuation marks, numeric digits, spaces, tabs, carriage returns (the ENTER key), other control characters, and other special symbols.

Most computer systems use a 1-byte or multi-byte binary sequence to encode the various characters. Windows, macOS, and Linux fall into this category, using the ASCII or Unicode character sets, whose members can all be represented with 1- or multi-byte binary sequences.

## The ASCII Character Set

The ASCII (American Standard Code for Information Interchange) character set maps 128 characters to the unsigned integer values 0 through 127.

The ASCII character set is divided into four groups of 32 characters. The ﬁrst 32 characters, ASCII codes $0 through $1F (0 through 31), form a special set of non-printing characters called the control characters . As their name implies, these characters perform various printer and display control operations rather than displaying symbols. Examples of control
characters include the carriage return, which positions the cursor at the beginning of the current line of characters; line feed, which moves the cursor down one line on the output device; and backspace, which moves the cursor back one position to the left. Unfortunately, because there’s very little standardization among output devices, different control
characters perform different operations on different output devices. To ﬁnd out exactly how a particular control character affects a certain device, consult the device’s manual.

The second group of 32 ASCII character codes comprises various punctuation symbols, special characters, and the numeric digits. The most notable characters in this group include the space character (ASCII code $20 ) and the numeric digits (ASCII codes $30..$39 ).

The third group of 32 ASCII characters contains the uppercase alphabetic characters. The ASCII codes for the characters A through Z lie in the range $41 through $5A . Because there are only 26 different alphabetic characters, the remaining six codes hold various special symbols.

The fourth and ﬁnal group of 32 ASCII character codes represents the lowercase alphabetic symbols, ﬁve additional special symbols, and
another control character (delete). The lowercase character symbols use the ASCII codes $61 through $7A . If you convert the codes for the upper- and lowercase characters to binary, you’ll notice that the uppercase symbols differ from their lowercase equivalents in exactly one bit position.

"E" - 0100_0101
"e" - 0110_0101

> Uppercase alphabetic characters always contain a 0 in bit 5; lowercase alphabetic characters always contain a 1 in bit 5.

Despite the fact that it is a “standard,” simply encoding your data using ASCII characters does not guarantee compatibility across systems.
An A on one machine is most likely an A on another system; but, of the 32 control codes in the ﬁrst group of ASCII codes, plus the delete code in the last group, only 4 control codes are commonly supported by most devices and applications—backspace (BS), tab, carriage return (CR), and line feed (LF).

> Windows, MS-DOS, CP/M, and other systems mark end-of- line by the two-character sequence CR/LF. The original Apple Macintosh OS and many other systems mark end-of-line by a single CR character. Linux, BeOS, macOS, and other Unix systems mark end-of-line with a single LF character.

## The EBCDIC (Extended Binary Coded Decimal Interchange Code) Character Set

Earlier IBM systems and keypunch machines used BCDIC (Binary Coded Decimal Interchange Code) , a character set based on punched cards and decimal representation (for IBM’s older decimal machines).

## Double-Byte Character Sets

Because a byte can represent a maximum of 256 characters, some computer systems use double-byte character sets (DBCSs) to represent more than 256 characters. DBCSs do not encode every character using 16 bits; instead, they use a single byte for most character encodings and use double-byte codes only for certain characters.

## The Unicode Character Set

The Unicode definition included all of the (known/living) character sets at the time, giving each character a unique encoding, to avoid the consistency problems that plagued differing DBCSs.
The original Unicode standard used a 16-bit word to represent each character. Therefore, Unicode supported up to 65,536 different character codes—a huge advance over the 256 possible codes that are representable with an 8-bit byte.
Today, Unicode is a universal character set, long replacing ASCII and older DBCSs. All modern operating systems (including macOS, Windows, Linux, iOS, Android, and Unix), web browsers, and most modern applications provide Unicode support.

A Unicode code point is simply an integer value that Unicode associates with a particular character symbol; you can think of it as the Unicode equivalent of the ASCII code for a character. The convention for Unicode code points is to specify the value in hexadecimal with a U+prefix; for example, U+0041 is the Unicode code point for the letter A.

Each Unicode code point has a unique name. For example, U+0045 has the name “LATIN CAPITAL LETTER A.” Note that the symbol A is not the name of the character. A is a glyph —a series of strokes (one horizontal and two slanted strokes) that a device draws in order to represent the character.

There are many different glyphs for the single Unicode character “LATIN CAPITAL LETTER A.” For example, a Times Roman letter A and a Times Roman Italic letter A have different glyphs, but Unicode doesn’t differentiate between them (or between A characters in any two different fonts). The character “LATIN CAPITAL LETTER A” remains U+0045 regardless of the font or style you use to draw it.

In Unicode, however, a character is largely equivalent to a code point. This is not what people normally think of as a character. In Unicode terminology, a grapheme cluster is what people commonly call a character —it’s a sequence of one or more Unicode code points that combine to form a single language element (that is, a single character). So, when we talk about characters with respect to symbols that an application displays to an end user, we’re really talking about **grapheme clusters**.

### Unicode Encodings

**UTF-32** uses 32-bit integers to hold Unicode scalars. The advantage to this scheme is that a 32-bit integer can represent every Unicode scalar value (which requires only 21 bits). The obvious drawback to UTF-32 is that each Unicode scalar value requires 4 bytes of storage—twice that of the original Unicode definition and four times that of ASCII characters.

**UTF-16** uses 16-bit (unsigned) integers to represent Unicode values. Because the vast majority of useful characters ﬁt into 16 bits, most UTF-16 characters require only 2 bytes. For those rare cases where surrogates are necessary, UTF-16 requires 2 words (32 bits) to represent the character.

The **UTF-8** encoding is forward compatible from the ASCII character set. In particular, all ASCII characters have a single-byte representation (their original ASCII code, where the HO bit of the byte containing the character contains a 0 bit).
UTF-8 encoding is probably the most common encoding in use. Most web pages use it. Most C standard library string functions will operate on UTF-8 text without modification (although some C standard library functions can produce malformed UTF-8 strings if the programmer isn’t careful with them).

## Character Strings

In general, a character string is a sequence of characters with two main attributes: a length and the character data.

### Character String Formats

#### Zero-Terminated Strings

Without question, zero-terminated strings are the most common string representation in use today, because this is the native string format for C, C++, and several other languages.
A zero-terminated ASCII string is a sequence containing zero or more 8-bit character codes ending with a byte containing **0**.

#### Length-Preﬁxed Strings

In a length-prefixed scheme (in Pascal), the string "abc" consists of 4 bytes: the length byte ( $03 ), followed by a , b , and c.

#### Seven-Bit Strings

The 7-bit string format is an interesting option that works for 7-bit encodings like ASCII. It uses the (normally unused) higher-order bit of the characters in the string to indicate the end of the string. All but the last character code in the string has its HO bit clear, and the last character in the string has its HO bit set.

#### HLA Strings

The HLA string format uses a 4-byte length prefix, allowing character strings to be just over four billion characters long (obviously, this is far more than any practical HLA application will use). HLA also appends a 0 byte to the character string data. The additional 4 bytes of overhead contain the maximum legal length for that string.

#### Descriptor-Based Strings

A slightly more flexible scheme is to maintain such information in a record structure, known as a descriptor , that also contains a pointer to the character data.

#### Java Strings

Java uses a descriptor-based string form. The actual String data type (that is, the structure/class that deﬁnes the internal representation of a Java string) is opaque , which means you really aren’t supposed to know about or mess with it.

#### Swift Strings

Like Java, the Swift programming language uses Unicode characters in its strings. As with Java, Swift’s String type is opaque, so you shouldn’t attempt to mess with (or otherwise use) its internal representation.

#### C# Strings

The C# programming language uses UTF-16 encoding for characters in its strings. As with Java and Swift, C#’s string type is opaque and you shouldn’t attempt to mess with (or otherwise use) its internal representation. That being said, the Microsoft documentation does claim that C# strings are an array of (Unicode) characters.

#### Python Strings

Today, modern versions of Python use a special string format that tracks the characters in strings and stores them as ASCII, UTF-8, UTF-16, or UTF-32, based on the most compact representation. You can’t really access the internal string representation directly within Python, so the caveats of opaque types aren’t relevant.

Based on the various string formats covered thus far, we can now define three string types according to when the system allocates storage for the string. There are static, pseudo-dynamic, and dynamic strings.

1. Pure static strings are those whose maximum size a programmer chooses when writing the program.

```Pascal
var pascalString :string(255);
```

```c
char cString[256];
```

2. A pseudo-dynamic string is one whose length the system sets at runtime by calling a memory management function like **malloc()** to allocate storage for it.

3. Dynamic string systems, which typically use a descriptor-based format, automatically allocate sufficient storage for a string object whenever you create a new string or otherwise do something that affects an existing string. Operations like string assignment and substring are relatively trivial in dynamic string systems—generally they copy only the string descriptor data, so these operations are fast.

## Creating character set

ASCII and EBCDIC were developed with now-antiquated hardware in mind—mechanical teletypewriters’ keyboards and punched-card systems, respectively. Given that such equipment is
found mainly in museums today, the layout of the codes in these character sets has almost no benefit in modern computer systems. If we could design our own character sets today, they’d be considerably different from ASCII or EBCDIC. They’d probably be based on modern keyboards (so they’d include codes for common keys, like LEFT ARROW, RIGHT ARROW , page up, and page down). They’d also be laid out to make various common computations a whole lot easier.
Although the ASCII and EBCDIC character sets are not going away any time soon, there’s nothing stopping you from defining your own application-specific character set. Of course, such a set is, well, application-specific, and you won’t be able to share text files containing characters encoded in your custom character set with applications that are ignorant of your private encoding. But it’s fairly easy to translate between different character sets using a lookup table, so you can convert between your application’s internal character set and an external character set (like ASCII) when performing I/O operations.

Using a single unsigned comparison to check if a character code is less than or equal to 9 , we can see if a character is a digit.

> The character code and the numeric representation are one and the same

> The lowercase characters have ASCII codes that are greater than the uppercase characters.

To test a character to see if it’s a member of a single case, you need two comparisons—first to see if it’s alphabetic, then to determine its case.

```c
if( (c >= 76) && (c & 1) )
{
// execute this code if it's an uppercase character
}
if( (c >= 76) && !(c & 1) )
{
// execute this code if it's a lowercase character
}
```

If you’re working in 80x86 assembly language, you can test a character to see if it’s uppercase or lowercase by using three machine instructions:

```assembly
// Note: ROR(1, AL) maps lowercase to the range $26..$3F (38..63)
// and uppercase to $A6..$BF (166..191). Note that all other characters
// get mapped to smaller values within these ranges.

ror( 1, al );
cmp( al, $26 );
jnae NotLower;

// Note: must be an unsigned branch!
// Code that deals with a lowercase character.

NotLower:

// For uppercase, note that the ROR creates codes in the range $A8..$BF which
// are negative (8-bit) values. They also happen to be the *most* negative
// numbers that ROR will produce from the HyCode character set.

ror( 1, al );
cmp( al, $a6 );
jge NotUpper;

// Note: must be a signed branch!
// Code that deals with an uppercase character.

NotUpper:
```

Let’s first take a look at what the standard case-insensitive character comparison would look like in C/C++ for two ASCII characters:

```c
if( toupper( c ) == toupper( d ))
{
// do code that handles c==d using a case-insensitive comparison.
}
```

This code doesn’t look too bad, but consider what the function (or, usually, macro) expands to:

```c
#define toupper(ch) ( (ch >= 'a' && ch <= 'z') ? ch & 0x5f : ch )
```

With this macro, you wind up with the following once the C preprocessor expands the previous if statement:

```c
if
(
( (c >= 'a' && c <= 'z') ? c & 0x5f : c )
== ( (d >= 'a' && d <= 'z') ? d & 0x5f : d )
)
{
// do code that handles c==d using a case-insensitive comparison.
}
```

This expands to 80x86 code similar to this:

```assembly
// assume c is in cl and d is in dl.
cmp( cl, 'a' ); // See if c is in the range 'a'..'z'
jb NotLower;
cmp( cl, 'z' );
ja NotLower;
and( $5f, cl ); // Convert lowercase char in cl to uppercase.
NotLower:

cmp( dl, 'a' ); // See if d is in the range 'a'..'z'
jb NotLower2;
cmp( dl, 'z' );
ja NotLower2;
and( $5f, dl ); // Convert lowercase char in dl to uppercase.
NotLower2:


cmp( cl, dl );  // Compare the (now uppercase if alphabetic) chars.

jne NotEqual; // Skip the code that handles c==d if they're not equal.

// do code that handles c==d using a case-insensitive comparison.
NotEqual:
```

Several programs (beyond compilers) need to efficiently process strings of characters that represent program identifiers. Most languages allow alphanumeric characters in identifiers, and, as you just saw, we can check a character to see if it’s alphanumeric using only two comparisons.
