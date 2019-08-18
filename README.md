# Basics of Encoding that every Developer should know

## Preface
The general meaning of encoding is a process of converting data from one 
form to another. In computer science `Encoding` means the conversion of 
data into specialized required form for several processes like program 
compiling, data transmission, storage, compressing/decompressing of the data 
and as ultimate representation can be numbers, electrical pulses, bits, etc.   
Transmitting data through the Internet or storing it on a disk requires 
representing it on a low machine level device. But, if the data is only 
stored on a device and is viewed on the same computer it is not important 
how they are encoded as the reader will not see the same characters.
When the data needs to be transmitted through a network to another 
machine encode standard should be specified because otherwise it will 
lead to misunderstanding of a character or character sets.
If, for example, a set consists of Chinese characters,
it can be encoded with Guobiao and Big5 and it is possible that a receiving
computer may not recognize both standards and as a result will only 
show meaningless characters. So, encoding it is a necessary component 
for internalization. 

## Terminology
`Character` - representation of the smallest fundamental item of written 
language; basic unit of encoding  
`Character set`- a collection of characters used to represent textual 
information  
`Encoded / coded character` - ordered and numbered association between 
character and code point  
`Code point` - a unique number that has been assigned to a character  
`Code unit` - the minimal bit combination that represents an encoded text 
for processing  

## What Unicode is
Before the Unicode standard was developed, there were numerous different 
encoding systems that could not handle all languages and most did not 
support the English language letters, punctuation, emoji and technical symbols.
Since then, Unicode has been improved and nowadays supports the writing 
and presentation systems with unique code for every character,
in every language, in every program or application on any operating system.

Unicode is the standard for digital representation of characters 
and as a main function it provides a universal character set for storing,
interchanging and searching for texts of any language. 

The Unicode Standard defines three encoding forms, thus allowing 
the same data to be transmitted in a byte equivalent,
word or double word oriented format (8-bits, 16-bits and 32-bits 
(not mentioned in this article) per code unit).
An example of Unicode form is the letter  ع,
which is the Arabic Letter Ain, and has a Unicode number U+0639 or 
1593 in hexadecimal and decimal number respectively. 

It is important to note, depending on encoding type hex,
dec and binary values are different. 
To know values, see the Unicode 
table here → https://unicode-table.com/en/#control-character. 

## UTF-8 
UTF-8 is a system of encoding characters using 8-bits sequence.
It is able to store a string in  Unicode, where code point starts with U+
numbers and in binary format in memory using one to four 8-bits code units.

<img src="/images/utf-8.png">

_Picture 1. UTF-8 encoding_

In the table above the reader, can see the structure of the encoding.
The encoding of the first 128 code points are equivalent 
to the ASCII encoding table. Higher code points represent 
more than one byte. Each byte is a single character which starts 
with a special bit sequence to signal that it is refers to the same character. 

For example, LATIN CAPITAL LETTER C code point in hexadecimal U+0043,
0x43 in UTF-8 hexadecimal and 01000011 in binary. In comparison,
LATIN CAPITAL LETTER C WITH CEDILLA Ç has U+00C7 code point in hex,
0xc3 0x87 in UTF-8 hex and 11000011 10000111 in binary because the 
letter has an additional element - cedilla - and thus an additional block.
As the reader can see, the first blocks of both C and Ç are the same due 
to the equal base character. So, cedilla has its own block after the 
C character block. 

## UTF-16, UTF-16BE and UTF-16LE
As with UTF-8, UTF-16 is a Unicode Transformation Format that 
is able to encode the same count of code points as UTF-8, 1 112 064.
Code points are encoded as one or two 16-bits code units. 

Code points from U+0000 to U+D7FF and from U+E000 to U+FFFF are encoded 
with 2 bytes. Code points from U+D800 to U+DFFF are permanently reserved. 

UTF-16BE form uses big-endian byte serialization (writing begins 
with the most-significant byte and ans ends with the least-significant byte)
and LE form uses little-endian byte serialization (writing begins 
with the least-significant byte and ends with the most significant byte) 
and unmarked form uses big-endian by default. 

<img src="/images/serialization.png">

_Picture 2. UTF-16BE and UTF-16LE_

Every time the developer should consider what form of serialization is used 
on specific platform and define one from another. 

## The difference between UTF-8 and UTF-16
UTF-8          
1 bytes: ASCII  
2 bytes: Arabic, Hebrew, European  
3 bytes: BMP   
4 bytes: All unicode characters   

UTF-16  
2 bytes: BMP  
4 bytes: All unicode characters 

| UTF-8 pros | UTF-16 pros |
|:-:|:-:|
| UTF-8 uses 1 byte as minimum  | Basic Multilingual Plane contains characters for almost all modern languages (2 bytes) |
| No null bytes | When string has supplementary characters they are still represented by pairs of 16 bits blocks |
| Bytes oriented format, that’s why there are no problems with byte oriented networks or files | Represents languages like Chinese and Japanese with 2 bytes. |
| Better recovering from errors | |

_Table 1. Pros of UTF-8 and UTF-16_

| UTF-8 cons | UTF-16 cons |
|:-:|:-:|
| Many common characters have different lengths, which slows indexing | Lots of null bytes, which waste memory | 
| Represents languages like Chinese and Japanese with 3 bytes | Not byte oriented and needs to establish an order before working with byte oriented systems |
| | Incompatible with ASCII |
| | Cannot deal with lost bytes | 


_Table 2. Cons of UTF-8 and UTF-16_

## Conclusion
Choosing an encoding type for a program or just small script, 
that will work with letters, is vital thing due to different concepts 
each of these types. The developer should consider advantages and 
disadvantages, that specific encoding type on a specific operating system 
or motherboard could lead to. So, defining purposes of a software,
technical characteristics and audience, for whom this software 
will be developed, can already give to the developer answer what encoding 
type is the most convenient.
