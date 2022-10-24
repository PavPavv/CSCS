# 5. CHARACTER REPRESENTATION

The term character refers to a human-or machine-readable symbol that is typically a non-numeric entity. In addition to alphabetic characters, character
data includes punctuation marks, numeric digits, spaces, tabs, carriage returns (the ENTER key), other control characters, and other special symbols.

Most computer systems use a 1-byte or multi-byte binary sequence to encode the various characters. Windows, macOS, and Linux fall into this category, using the ASCII or Unicode character sets, whose members can all be represented with 1- or multi-byte binary sequences.

## 1. The ASCII Character Set

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

## 2. The EBCDIC Character Set