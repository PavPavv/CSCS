# 5. CHARACTER REPRESENTATION

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






