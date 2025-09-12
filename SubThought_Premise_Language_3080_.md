

The Premise Language

_version 3.0_

by

Michael S P Miller

_The Premise Language_

_The Premise Language_

_version 3.0_

by

Michael S. P. Miller

Copyright © 2013 – 2025. Michael S. P. Miller.

All Rights Reserved. No part of this book may be reproduced in any form by any electronic or mechanical means (including photocopying, recording, or information storage and retrieval systems) without permission in writing from the author–except in the case of a reviewer who may quote brief passages embodied in critical articles or in a review.

Trademarked names may appear throughout this book. Rather than use a trademark symbol with every occurrence of a trademarked name, names are used in an editorial fashion, with no intention of infringement of the respective owner’s trademark or copyright. The same applies to quotations or synopses of copyrighted material.

The information in this book is distributed on an “as is” basis, without warranty. Although every precaution has been taken in the preparation of this work, neither the author nor the publisher shall have any liability to any person or entity with respect to any loss or damage caused directly or indirectly by the information contained in this book. The source code examples and specifications in this book are for illustrative purposes only, and are therefore provided as is, without warranty of any kind, neither expressed nor implied that the examples work or are fit for a particular purpose. The author and publisher assume no responsibility or liability for damages or losses, neither incidental nor consequential, incurred as a result of using the provided specifications or source code.

The Premise Language<sup>TM</sup>, The Premise Programming Language<sup>TM</sup> and The SubThought Logo<sup>TM</sup>, the \[P\] logo<sup>TM</sup>, are Copyright © 2013 – 2025 SubThought Corporation. All Rights Reserved.

For comments on the SubThought Premise Language contact: [subthoughti@hotmail.com](mailto:premise.ai@gmail.com)

For electronic inquiries or permissions contact: <subthought@hotmail.com>.

by mail: SubThought Corporation, 254 N. Lake Ave. #213, Pasadena, CA 91101 USA

This book was published in the United States of America.

Paperback ISBN-13: 979-8-849321-64-6 Paperback ISBN-10: 8-849321-64-3  
Hardcover ISBN-13: 979-8-849796-21-5 Hardcover ISBN-10: 8-849796-21-8

Cover by Michael S. P. Miller

Document version: 3.072

_For those who seek truth._

# Contents

[Contents 11](#_Toc203575930)

[Figures 12](#_Toc203575931)

[Tables 12](#_Toc203575932)

[Acknowledgements 13](#_Toc203575933)

[Disclaimer 13](#_Toc203575934)

[Introduction 15](#_Toc203575935)

[1\. Getting Started 19](#_Toc203575936)

[2\. The Interpreter 21](#_Toc203575937)

[3\. Taxonomy 25](#_Toc203575938)

[4\. Control Flow 57](#_Toc203575939)

[5\. Code Examples 77](#_Toc203575940)

[6\. Foundation Modules 114](#_Toc203575941)

[7\. Quick Reference 115](#_Toc203575942)

[8\. Function Reference 125](#_Toc203575943)

[Bibliography 661](#_Toc203575944)

[Index 663](#_Toc203575945)

# Figures

[Figure 1. The Premise Interpreter Architecture 21](#_Toc204097267)

[Figure 2. Premise Taxons. 25](#_Toc204097268)

# Tables

[Table 3. Function Quick Reference 124](#_Toc204097255)

# Acknowledgements

“_Do you see over yonder, friend Sancho, thirty or forty_

_hulking giants? I intend to do battle with them and slay them._”

― Miguel de Cervantes Saavedra, Don Quixote

This work was not possible without the efforts and advice of Dr. Sheldon Linker, whose collaboration on terminology and functionality was most welcome, and combined with his proficient coding skills led to the 2013 Java implementation of a just in time interpreter: The Premise 0.1 Executive.  
Suzuki Hisao's lucid and concise C# implementation of Nukata Lisp Lite was insightful, as was Peter Norvig's implementation of JScheme. Allen Holub's book Compiler Design in C was also instructive, particularly in the area regarding approaches to tokenization and parsing. Christian Queinnec's tome, Lisp In Small Pieces, also provided invaluable insights on expression evaluation. Christian's encouragement on this project was greatly appreciated. Roland Hausser's left associative grammar was pivotal in the tokenizer design.

The author would also like to thank Aaron Hosford for his suggestions on numeric similarity metrics, Ryan Hewitt for his comments on prototype construction, Brian Will for his ideas on restricted scoping, Dr. Ghassan Azar, Todd Kaufmann, Dr. Michael Schuresko, Robert Rossi, Jean-Louis Villecroze and the rest of the Premise Language group for their constructive feedback and suggestions.

# Disclaimer

The source code examples and specifications in this book are for illustrative purposes only, and are therefore provided as is, without warranty of any kind, neither expressed nor implied that the examples work or are fit for a particular purpose. The author and publisher assume no responsibility or liability for damages or losses, neither incidental nor consequential, incurred as a result of using the provided specifications or source code, up to and including loss of business, injury, or death.

# Introduction

The Premise Language is a functional prototype programming language which combines high level intrinsic primitives with seamless object persistence. The goal of the Premise Language is to provide a platform for artificial intelligence programming. Software agents written in Premise share a knowledge base where they can create, modify, and delete object instances amongst themselves in a stigmergic manner. Premise is influenced by Lisp, Self, JavaScript, OPS5, and CLIPS.

The Premise Language was developed by Michael S. P. Miller and Sheldon O. Linker during 2013 and 2014. In creating a platform for agent based programming for intelligent systems (JCB English and The Piagetian Modeler) they found a need for a very high level language in which to code asynchronous agent processes to perform complex pattern matching and inference. They explored the Sapir-Whorf hypothesis as it relates to computer programming–namely, that the primitive operations available in a computer language influence the way software developers frame and solve problems, and it was early determined that the primitives of the needed language should be very high level and include logical and similarity-based pattern matching, inference, messaging, stigmergy, and asynchrony. The language combines elements of declarative, functional, and imperative programming with seamless persistent object storage and retrieval. The goals of The Premise Language are simple:

- To define memory as a portable abstraction across different physical implementations. Premise uses a persistent object store as its memory.
- To facilitate the fast formation of relationships in a persistent memory. Constructing persisted records in Premise is the same as asserting facts to the working memory of other declarative language platforms such as CLIPS or OPS.
- To allow rapid interrogation of relationships in the memory.
- To provide scalability to billions of persisted records.
- To explore the Sapir Whorf hypothesis as it relates to computer programming: that the constructs available in computer languages influence the way people think about and solve problems.
- To explore the stigmergic programming paradigm, where objects constructed by one agent are later used or consumed by other agents.
- To provide a clear and concise API.

The Premise Language serves as a testbed for agent programming. Functions are the primary unit of processing. Numbers, strings, literals, prototypes, persisted records, lexicons, lists and calls provide the primary data types. The Premise Language opens up new possibilities for knowledge representation and artificial intelligence programming.

We hope you enjoy using this language.

Michael Miller

February 2019 (version 1.0)

July 2025 (version 3.0)

## Document Conventions

The following are conventions used in this document.

### Source Code

Premise source code will appear in Courier New font in a colored text region. The gray text region depicts a session in the Premise interpreter.

```

> (take "{a b c}")

.:  {a b c}

```

A green text region depicts Premise source code snippets that appear in a file editor.

```

(relation Problem

:Name :Status

)

```

A blue text region depicts non-Premise source code snippets that appear in a file editor.

```

SELECT DISTINCT LENGTH(CategoryName)

FROM Category

```

### Source Code Comments

In-line comments are denoted by semicolons. Everything from the comment to the end of the line is ignored by the interpreter.

```

; this is an in-line comment

```

Multi-line comments are delimited by double quotation marks. Everything between the delimiters is treated as a single string and returned as-is by the interpreter. A free standing string, not part of a function or macro call, evaluates to itself, and thus can be used as a comment.

```

"this is a

multi-line

comment"

```

## Language Style Conventions

As a matter of style, each of the following language elements is written in a specific case:

Modules    are written in Pascal case.

Types  are written in  Pascal case.  
:Slots           are written in Pascal case with a preceding colon.

!methods    are written in camel case with a preceding exclamation point.  
functions   use camel case for verbs and Pascal case for nouns.  
?locals (local variables) are in camel case with a preceding question mark.

?Modular (modular variables) are in Pascal case with a preceding question mark.

?Global (global variables) are in Pascal case with a preceding question mark.

?CONSTANTS are written in upper case with a preceding question mark.  

# 1\. Getting Started

To use the Premise Language, download the Premise executable to a folder on your computer then extract the file using standard decompression software.

To run the Premise evaluator type the following:

premise

Example:

```

C:\\projects\\SubThought\\>premise

\[Premise :Version 3.0 :Build 20250801.0001 :OS Windows 11 :Edition Community\]

Enter expressions followed by a blank line. Type (help), (copyright) or (license)

for information. Type (grok "file.theory") to read a file. Type (bye) to exit.

> (copyright)

.:  "Copyright (c) 2014-2025 SubThought Corporation, All Rights Reserved."

>

```

# 2\. The Interpreter

The goal of Premise is to facilitate fast persistent relationship formation in a client server environment. Clients connect to the server and execute expressions. The expressions create and modify records in the object store.

![A diagram of a data processing process

AI-generated content may be incorrect.](data:image/jpeg;base64,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)

Figure 1. The Premise Interpreter Architecture

The Premise Language interpreter follows several guiding principles, among them:

1. Metacircular evaluation. Parts of Premise are written in the Premise Language itself.  

2. A Lisp-1 approach to symbol and function lookup is employed. This means that variables and functions can share the same symbol environment. Because variables are prefixed by question marks and functions are not, the difference between the symbol "?foo" and the function "foo" is evident. This eliminates one source of complexity for Lisp like languages.
3. The main point of The Premise Language is to build shared structures. To that end, relations, premises, and certain containers are persisted in an object store (e.g., a RAM database) to facilitate pattern matching over persisted records, and to facilitate concurrent access to shared structures.

## The Read Evaluate Print Loop

The Premise Language interpreter, otherwise known as the Read Evaluate Print Loop, allows users to enter expressions at the prompt (i.e., >). The interpreter evaluates the expression and returns the result. The result is printed after the ergo sign (i.e., .:). For example, when the literal true is entered at the prompt, it evaluates to itself and is returned by the interpreter as follows:

```

> true

.:  true

```

An expression that adds two numbers together would return the sum like this:

```

> (+ 1 2)

.:  3

```

To print "Hello World" one would type the following.

```

> (tell user "Hello, World. \\n")

Hello, World.

.:  told

```

## Imperative Programming

The Premise Language facilitates imperative, functional, and declarative programming. For example, adding the numbers from one to ten in an imperative style could involve defining a symbol ?total to store the result, and looping an iteration symbol from 1 to 10.

```

> (function sum {list ?numbers}

(let ?total 0) ; assume ?total is 0

(for ?n in ?numbers

(set ?total (+ ?total ?n))) ; set ?total to the result of adding ?total and ?n

?total) ; return ?total

.:  sum

> (sum {1 2 3 4 5 6 7 8 9 10}) ; test the function

.:  55

```

## Functional Programming

Adding numbers in a functional style might involve generating a list of numbers, walking through the list, and adding the numbers until we reach the end of the list. This approach eliminates the need for a ?total symbol since the result is recursively kept on the program stack.

```

> (function sum1 {list ?numbers}

(if (void-p ?numbers) ; if the list of numbers is empty

0 ; return zero

else

(+ (@ ?numbers) ; add the first number

(sum (rest ?numbers)))) ; to the sum of the remaining numbers

)

.:  sum1

> (range 1 to 10) ; generate a list of numbers

.:  {1 2 3 4 5 6 7 8 9 10}

> (sum1 (range 1 to 10)) ; test the function

.:  55

```

An even more concise approach to sum uses the function reduce.

```

> (function sum2 {list ?numbers}

(reduce ?numbers +)

)

.:  sum2

> (sum2 (range 1 to 10))

.:  55

```

## Declarative Programming

Declarative programming involves establishing a set facts and writing a query or rule to utilize the facts. In The Premise Language, this approach utilizes relation instances, called "thoughts."

```

> (relation Addend ; make an Addend relation

:Value

:Counted false

)

.:  Addend

> (step ?i from 1 to 10

(new Addend :Value ?i)) ; make the individual addends

.:  Addend_10

> (relation Total ; make a total relation

:Result 0

)

.:  Total

> (new Total) ; make a new total

.:  Total_1

> (with

\[Total ^ as ?total\] ; match the Total

\[Addend ^ as ?addend :Value as ?value :Counted = false\] ; match uncounted

do

(put ?addend :Counted true) ; indicate that the addend was used

(==> ?total + :Result ?value) ; apply + to :Result and ?value, put in :Result slot

(:Result ?total)) ; return the :Result slot value

.:  55

```

# 3\. Taxonomy

In Premise, the data types are are called taxons and are organized into a taxonomy as follows.
```
├── variant ; an abstract value of any type. \\%variant
|├── nothing ; a concrete value representing nothing. \\%nothing
||├── nil ; a concrete unspecified value. \\%nil
||├── void ; a concrete value denoting emptiness \\%void
|├── thing ; an abstract value representing something. \\%thing
||├── container ; an abstract container. \\%container
|||├── assortment ; an abstract unordered grouping. \\%assortment
||||├── configuration ; a concrete assortment of persisted key value pairs. \\%configuration
||||├── enumeration ; a concrete assortment of name to number pairs. \\%enumeration
||||├── environment ; a concrete assortment of symbol or literal to value pairs. \\%environment
||||├── lexicon ; a concrete assortment of key to value pairs. \\%lexicon
|||├── group ; an abstract unordered grouping. \\%group
||||├── bag ; a concrete group of possibly duplicated items. \\%bag
||||├── collection ; a concrete set of unique values. \\%collection
||||├── queue ; a concrete priority queue. \\%queue
|||├── sequence ; an abstract ordered grouping. \\%sequence
||||├── call ; a concrete function call. \\%call
||||├── expression ; a concrete undelimited sequence of variants. \\%expression
||||├── list ; a concrete curly brace delimeted sequence of variants. \\%list
|||||├── plist ; a concrete curly brace delimeted sequence of slot value pairs. \\%plist
||||├── series ; a concrete iterator. \\%series
|||||├── cursor ; a concrete handle to a remote sequence. \\%cursor
||||├── string ; a concrete double quote a delimited character sequence. \\%string
||||├── vector ; a concrete pipe delimited sequence of numbers or literals. \\%vector
||||├── tuple ; a concrete square bracket delimited sequence of variants. \\%tuple
|||||├── pattern ; a tuple having a literal and triples of slot, function and either value, call, or symbol. \\%pattern
|||||├── premise ; a tuple having a literal and slot value pairs. \\%premise
||├── atom ; an abstract simple thing. \\%atom
|||├── number; an abstract number. \\%number
||||├── big ; a concrete integer longer than 128 bits \\%big
||||├── complex ; a concrete number with real and imaginary parts \\%complex
||||├── imaginary ; a concrete coefficient for the square root of -1 \\%imaginary
||||├── integer ; a concrete 64 bit signed integer. \\%integer
||||├── long ; a concrete 128 bit signed integer. \\%long
||||├── numeric ; a concrete numeric value, one of {\\%infinity \\%ninfinity \\%undefined}. \\%numeric
||||├── rational ; a concrete number as numerator over denominator. \\%rational
||||├── real ; a concrete decimal number in scientific notation. \\%real
||||├── float ; a concrete concrete 128 bit floating point number. \\%float
||||├─ unsigned ; concrete an unsigned 64 bit integer. \\%unsigned
|||├── time ; an abstract measurement. \\%time
||||├── instant ; an abstract single point in time. \\%instant
|||||├── date ; a concrete UTC date. \\%date
|||||├── epoch ; a concrete Unix epoch. \\%epoch
|||||├── jiffy ; a concrete clock speed (0.0166667 seconds). \\%jiffy
|||||├── moment ; a concrete nanoyear (0.0031573275 seconds). \\%moment
|||||├── second ; a concrete second. \\%second
|||||├── tick ; a concrete nanosecond. \\%tick
|||||├── temporal ; a concrete time value, one of {\\%eternity \\%neternity \\%indefinite}. \\%temporal
||||├── interval ; a concrete period spanning two time instants. \\%interval
|||├── identifier ; an abstract non-delimited case insensitive string. \\%identifier
||||├── symbol ; a concrete question prefixed mutable variable. \\%symbol
|||||├── constant ; a concrete question prefixed immutable constant. \\%constant
||||├── reference ; a concrete pointer to a symbol. \\%reference
||||├── literal ; a concrete undelimited alphanumeric sequence. \\%literal
|||||├── function ; a concrete literal that defines a function. \\%function
||||||├── anonym ; an concrete anonymous function. \\%anonym
||||||├── esonym ; an concrete internally named function. \\%esonym
||||||├── exonym ; a concrete user named function. \\%exonym
||||||├── generator ; a concrete function that creates a series. \\%generator
||||||├── junction ; a concrete parallel evaluation function. \\%junction
||||||├── macro ; a concrete user named macro. \\%macro
||||||├── method ; a concrete exclamation prefixed function literal. \\%method
||||||├── predicate ; a concrete monadic function returning a truth value. \\%predicate
||||||├── procedure ; a concrete function returning nothing. \\%procedure
||||||├── rule ; a concrete rule \\%rule
||||||├── special ; a concrete special form \\%special
||||||├── thunk ; a concrete evaluation delay. \\%thunk
|||||├── reserved ; a concrete reserved set of literals. \\%reserved
||||||├── truth ; a concrete truth value, one of {\\%true \\%false \\%unknown}. \\%truth
||||||├── sigil ; a concrete sigil value, one of {\\%optional \\%keyword \\%variadic}. \\%sigil
|||||├── module ; a concrete module. \\%module
|||||├── slot ; a concrete colon prefixed property identifier. \\%slot
|||||├── resource ; an abstract resource location. \\%resource
||||||├── url ; a concrete universal resource. \\%url
|||||||├── data ; a concrete data base connection. \\%data
|||||||├── file ; a concrete file resource. \\%file
|||||||├── folder ; a concrete file resource. \\%file
|||||||├── index ; a concrete relation access resource. \\%index
|||||||├── knowledge ; a concrete knowledge base connection. \\%knowledge
|||||||├── port ; a concrete port. \\%port
|||||||├── pipe ; an concrete input output resource. \\%pipe
||||||├── interpreter ; a concrete expression interpreter. \\%interpreter
||||||├── reader ; a concrete expression reader. \\%reader
|||||||├── lexer ; a concrete tokenizer. \\%lexer
|||||||├── parser ; a concrete expression generator. \\%parser
||||||├── evaluator; a concrete expression evaluator. \\%evaluator
||||||├── writer; a concrete expression writer. \\%writer
|||||||├── emitter; a concrete expression emitter. \\%writer
||||||├── prototype ; an abstract relationship. \\%prototype
|||||||├── relation ; a concrete persisted relationship. \\%relation
|||||||├── structure ; a concrete ephemeral relationship. \\%structure
||||||├── record ; an abstract record. \\%record
|||||||├── thought ; a concrete persisted record. \\%thought
|||||||├── ephemeron ; a concrete ephemeral record. \\%ephemeron
||||||├── task ; a concrete task resource. \\%task
||||||├── uuid ; a concrete unique identifier. \\%uuid
```
Figure 2.  Premise Taxons

## Variants

In Premise, all values are typed. Variables (also called symbols) are bound to typed values, but the symbols themselves are not typed. A variant is a value that can be any type. Variants are either nothing or something (i.e. a thing).

## Nothing

The taxon \\%nothing which evaluates to the literal nothing represents values that do not exist. The taxon \\%nil represents something that is unspecified. It can be compared to the literal nil . Unspecified values default to nil with the is function. A value of \\%void means a container has no elements. The function null-p can be used to determine whether a value is either unspecified or nonexistent. Containers default to empty and can be tested with the void-p function.

```

\\%nothing \\%nil \\%void

```

## Things

The type thing represents a value that exists. The function exists-p can be used to detect if a value exists. The thing type is subdivided into atom and container.

## Atoms

An atom is a number, time value , or identifier (symbol or literal).

### Numbers

The number data type encapsulates several sub types: big, integer, long, unsigned, rational, real, float, imaginary, and complex.

#### Integers

Positive and negative decimal integers up to 64 bits are supported. Apostrophes (') used as separators within numbers are ignored.

```

\-5 +3

+999999999999999999 -999'999'999'999'999'999

```

##### Radix

Integers from radix 2 through radix 36 of the form \\#TDDrSN… are supported, where T is a taxon indicator (n:Integer, g:Long, b:Big, r:Real, f:Float, i:Imaginary, u:Unsigned, c:Complex), D is a decimal number between zero and nine, S is an optional sign for positive (+) or negative (-) number, and N is a number from zero (0) to nine (9) or an uppercase letter from A through Z. The radix combination DD must be within the range of 2 to 36 inclusive and the digits N must be less than DD. For example #2r has digits 0 and 1 while #16r has digts 0 through F.

```  
\\#n02r+10110 \\#n16r-778CF20 \\#n36r+84QQN250MLQZ

```

##### Binary

Binary integers (\\#n2r) are supported in the abbreviated form #\\nbSN… for N equals 0 or 1.

```  
\\#nb+1010 \\#nb-10101 \\#nb0

```

##### Octal

Octal integers (\\#n8r) are supported in the form #noSN… for N from 0 to 7.

```  
\\#no+1234 \\#no+0 \\#no+72'342

```

##### Decimal

Decimal integers (\\#n10r) are supported by default and also in the form \\#ndSN… for N from 0 to 9.

```  
\\#nd+9821 \\#nd+0 \\#nd-8'290'553

```

##### Hexadecimal

Hexadecimal integers (#n16r) are supported in the form #nxSN… for N from 0 to F.

```  
\\#nx-00FF \\#nx0 \\#nx82'9CA'FF3

```

##### Hexatridecimal

Hexatridecimal integers (\\#n36r) are supported in the form \\e#nzSN… for N from 0 to Z.

```  
\\#nz-QA5N \\#nz0 \\#nz+7'0M6'Z8P

```

#### Longs

A long number is a decimal integer that is 128 bits.

```  
\\#gd+100000000000000000000 \\#gd-800'000'000'000'000'000'000  
```

#### Big

A big number is a decimal integer that is longer than 128 bits.

```  
\\#bd+100000000000000000000 \\#bd0 \\#bd-8000000000000000000000000000

\\#bd23928374928379658218798105687251871972938729387492837492876582736482763876283762487364827364872638476827368427634872638476287482364827634872638476283476287634827364872638476824768237648276348273648276384726834762837648768  
```

#### Rationals

Rational numbers have a decimal integer numerator over a decimal integer denominator.

```  
3/4 -8/20  
```

#### Reals & Floats

Real numbers are 64 bit decimal floating-point numbers in scientific notation. A float is a sub type of real. Float numbers are 128 bits, have higher precision and a smaller range than real numbers. Floats can be used for monetary values. Float calculations must be made explicit by wrapping them in the float function , e.g. (+ (float 100) (float 200)), or prefixing \\#fd before the number.

```  
10.0 -98'768'762'983.237876867749

(real 0.001) (float -2342.0e-23)

\\#rd+2342.243 \\#fd+234.0e+0

\\#rd-54.50 \\#fd124.95

```

#### Imaginaries

Imaginary numbers are decimal numbers having a floating point number suffixed by the letter "i" (representing the square root of -1).

```  
\\#id+21 \\#id-5.0 \\#id2.9 \\#id-9.93  
```

#### Complexes

Complex numbers include a decimal real part plus a decimal imaginary part.

```  
\\#cd+55+34i \\#cd-2.35+7i \\#cd-32-14.3i

\\#cd+0-2i \\#cd75+i \\#cd0+i  
```

#### Unsigned

Unsigned decimal integers up to 64 bits are supported. They are prefixed by the letter "u"

```

\\#ud+0 \\#ud+3

\\#ud+18446744073709551615 \\# ud+99'999'999'999'999'999

```

#### Numerics

A numeric represents any of the values for infinity, negative infinity or undefined numbers.

```  
\\%numeric  
```

##### Infinity

The infinity taxon represents a positive infinite number.

```  
\\%infinity  
```

##### Ninfinity

The ninfinity taxon represents a negative infinte number.

```  
\\%ninfinity  
```

##### Undefined

The undefined taxon represents an impossible or undefined number.

```  
\\%undefined  
```

### Time

Time is supported in several varieties: dates, epochs, intervals, moments, seconds, and ticks.

#### Dates

A date represents time as a universal time coordinate (YYYY-MM-DDThh:mm:ss.sZ) in Zulu time or with an offset.

```

\\@d1990-01-10T09:30:00.001Z \\@d2016-11-24T08:15:30-08:00

```

#### Epochs

The epoch data abstraction represents time in unix epochs as a 128 bit integer value prefixed by the letter "e". An epoch represents the number of seconds since midnight January 1, 1970.

```  
\\@e10 \\@e592 \\@e60  
```

#### Jiffies

The jiffy data abstraction represents time as 1/60<sup>th</sup> of a second or as 16,666,666 nanoseconds.

```  
\\@j-12 \\@j+600 \\@j60  
```

#### Intervals

The interval data abstraction represents a time coordinate as a pair of time points. The lesser time point is followed by the greater time point.

```

\\@i{\\@m2012001005050000 \\@m2025500000000000} \\@i{\\@s3 \\@s10}

\\@i{\\@d2012-05-19 \\@d2013-07-23} \\@i{\\@u946 \\@u1577}

```

#### Moments

The moment data abstraction represents time in nano-years (approximately 0.0031573275 seconds) as a 16 digit, 64 bit, integer value prefixed by the letter "m".

```

\\@m2025500000000000 \\@m-1

\\@m2012001005050000 \\@m+3000 ; approximately 10 seconds

```

#### Seconds

The seconds data abstraction represents time in seconds as a 64 bit integer value prefixed by the letter "s".

```  
\\@s10 \\@s592 \\@s60  
```

#### Ticks

The tick data abstraction represents time in nanoseconds as a 64 bit integer value prefixed by the letter "t".

```  
\\@t2342 \\@t100000  
```

#### Temporal

The temporal taxon represents eternity, negative eternity, impossible, or indefinite time.

```  
\\%temporal  
```

##### Eternity

The eternity taxon represents an infinite amount of time in the future.

```  
\\%eternity  
```

##### Neternity

The neternity taxon represents an infinite amount of time in the past.

```  
\\%neternity  
```

##### Indefinite

The indefinite taxon represents an undefined or impossible time. Usually the default for an instant.

```  
\\%indefinite  
```

### Identifiers

An identifier is an alphanumeric sequence of characters not delimited by quotes.

#### Symbols

A symbol is a variable, i.e., an identifier that has both a name and an associated value. In the Premise Language, symbols are literals starting with a question mark and ending with a sequence of numeric or alphanumeric characters. When symbols are declared their value is immediately set to an initial value. Referencing an undeclared symbol will cause a failure. Symbols are typically written in lowercase. Dots in the symbol name indicate a symbol within a particular module. For example:

```

?height ?User.width ?length ?2

```

##### Constants

A constant is a symbol whose value cannot change. By convention constants are written in uppercase.

```

?MAX-LIMIT ?WIDTH-MIN ?\*DEFAULT-LENGTH\*

```

##### References

A symbol reference is a pointer to a symbol. A reference allows a symbol value to be passed as a parameter. A reference is printed as \\& and the symbol name. (e.g., \\&?me).

```

(reference ?MAX-LIMIT) (reference ?2)

\\&?MAX-LIMIT \\&?2

```

##### Symbol Scoping

Symbol scope refers to the environment a symbol belongs to. A symbol may have one of five scopes: global, module, lexical, dynamic, task, and restricted.

###### Global Scope

Global variables are declared using the global function.

```

> (do (global ?X 1)

(function g (tell user ($$ ?X \\s)) (set ?X 2))

(function f (global ?X 3)(g)))

(f)

(tell user ($ ?X ($))))

3 2 .: told

```

###### Module Scope

&nbsp;A symbol may be scoped to the current module using the modular  function.

```

> (do (global ?X 1)

(function g (tell user ($$ ?X \\s)) (set ?X 2))

(function f (modular ?X 3) (g)))

(f)

(tell user ($ ?X ($))))

3 1 .: told

```

###### Lexical Scope

Lexical scoping in Premise is achieved via the so, let, and var special forms. Multiple tasks may access the same lexical symbol. The so special form creates a new scope, while let and var add variables to the existing scope.

```

> (do (global ?X 1)

(function g (tell user ($$ ?x \\s)) (set ?x 2))

(function f (so {?x 3} (g)))

(f)

(tell user ($ ?X ($))))

3 1 .: told

> (do (global ?X 1)

(function g (tell user ($$ ?x \\s)) (set ?x 2))

(function f (let ?x 3) (g)))

(f)

(tell user ($ ?X ($))))

3 1 .: told

> (do (global ?X 1)

(function g (tell user ($$ ?x \\s)) (set ?x 2))

(function f (var ?x 3) (g)))

(f)

(tell user ($ ?X ($))))

3 1 .: told

```

###### Dynamic Scope

&nbsp;A dynamic scope creates temporary global variables.

```

> (do (global ?X 1)

(function g (tell user ($$ ?X \\s)) (set ?x 2))

(function f (dynamic {?x 3} (g)))

(f)

(tell user ($ ?X ($))))

3 2 .: told

```

###### Task Scope

&nbsp;Variables local to a particular task are shielded from changes by other tasks.

```

> (do (global ?X 1)

(function g (tell user ($$ ?x \\s)) (set ?x 2))

(function f (local {?x 3} (g)))

(f)

(tell user ($ ?X ($))))

3 1 .: told

```

###### Restricted Scope

Rescricted scopes only shadow variables and prohibit free variables.

```

> (do (global ?X 1)

(function g (tell user ($$ ?x \\s)) (set ?x 2))

(function f (only {?x} (g)))

(f)

(tell user ($ ?X ($))))

1 1 .: told

```

##### Symbol Assignment

Variables may be bound to values in a variety of ways.

###### Fix

The fix special form declares taxon restricted variables in the current environment, returning true.

```

> (fix integer ?age 10 string ?name "John Doe" literal ?fruit grape)

.:  true

> ?age ?name ?fruit

.:  10 "John Doe" grape

```

###### Let

The let special form declares and initializes variables in the current environment, returning true.

```

> (let ?X 1 ?Y 2 ?Z 3)

.:  true

> (let {?a ?b ?c} {dog cat fish})

.:  true

> ?a ?b ?c ?X ?Y ?Z

.:  dog cat fish 1 2 3

```

###### Var

The var special form declares and initializes variables, returning the value of the last assignment.

```

> (var {?a ?b ?c} {dog cat fish} ?X 1 ?Y 2 ?Z 3)

.:  3

> ?a ?b ?c ?X ?Y ?Z

.:  dog cat fish 1 2 3

```

###### Tie

The tie special form updates declared variables, returning the last assigned value.

```

> (tie ?X 1 ?Y (++ ?X) ?Z (++ Y))

.:  3

> (tie {?X ?Z} {2 2})

.:  2

> ?X ?Y ?Z

.:  2 2 2

```

###### <-- Before Tie

The before tie special form captures a symbol's return value before binding the symbol to an expression.

```

> (global ?X 1 ?Y 1 ?Z 1)

.:  true

> (<-- ++ ?X)

.:  1

> ?X

.:  2

```

###### \--> After Tie

&nbsp;The after tie special form captures a symbol's return value after binding the symbol to an expression .

```

> (global ?X 1)

.:  true

> (--> + ?X 1)

.:  2

> ?X

.:  2

```

###### Set

The set special form updates declared variables, and returns true.

```

> (set ?X 1 ?Y (++ ?X) ?Z (++ Y))

.:  true

> ?X ?Y ?Z

.:  1 2 3

```

###### Bind

The bind special form declares variables in the current environment and binds them to object property values, object method values, sequence positions, or functions, and then returns true.

```

> (relation Counter

:Value 0 :Resets 0 :Reclaim false

)

.:  Counter

> (new Counter)

.:  Counter_1

> (bind Counter_1 :Value ?value)

.:  true

> ?value

.:  0

> (bind {a b c d e f g} 1 ?first # ?last)

.:  true

> ?first ?last

.:  a g

```

#### Literals

Literals are non-numeric constants which evaluate to themselves. Typically, literals begin with an alphabetic or punctuation character (such as colon or exclamation point), and contain contiguous sequences of alphabetic, numeric, underscore or period characters. Literals provide names for functions, relationship prototypes, enumeration values, and so forth. Some examples of literals are as follows:

```

a one :2 three

a_1 a_12-34 hello-world the_quick_brown_fox

\* ! ::= -a-curious-literal

```

##### Structures

Structures are unpersisted ephemeral relationships, created with the structure function.

```  
\> (structure Fault :What :Where :When)  


.:  Fault  


> (Structure Message :Sender :Recipient :Content)  


.:  Message  
```

###### Slots

Slots are literals preceded by a colon. Some examples are:

```  
:Height :Width :Length :321 ^  
```

The identifier slot is the caret character: ^ .

Slots hold data values. In relation definitions, slots are followed by values called defaults. In instances, slots are followed by actual values called terms. When no default or referent is present for a slot, the value nil is implied.

The following are examples of relationship prototypes with slots and defaults.

```

(structure Red

:Object corvette

:Size little )

```

```  
(structure Phrase

:Saying "Who goes there"

:Count 14 )

```

The following are some examples of premises with slots and terms.

```  
\[Red ^ Red_56 :Object corvette :Size litte\]

\[Event ^ Event_101 :Subject bird\]

\[Basket ^ Basket_12 :Items {apple banana orange}\]

\[Person ^ {Person_201 Person_202 Person_203} :Name "John Smith"\]  
```

When a call has a relation slot as its first item and a premise or thought as the second item, the call will return value of the slot within the premise or from the thought.

```  
\> (:Color \[Fruit :Color Green\])

  
.: Green

```

```  
\> (:Quantifier Fact_35)  


.:  Some  
```

##### Relations

A persisted relationship is comprised of a type literal, slots, methods, and default values. A thought premise has a relation literal, slots, methods, and actual values. Relationships are defined using the relation function. Thoughts are created using the new or the knew function. Finally, there are three kinds of slots for a Relationship: data slots (prefixed with a colon), method slots (prefixed with an exclamation point), and identity slots (using the caret character to name the slot).

The relation function is used to define a relationship. The relation definition starts with a left parenthesis, followed by the literal relation, followed by an identifier for the type name, followed by any relation dependencies (each dependency is preceded by the uses keyword), then the slots and default values, methods and function names, and finally ending with a right parenthesis.

A relationship prototype must be defined before a new thought can be formed. Consider the following definitions:

```  
\> (relation Fruit

:Color

:Weight 1.0

!eat Fruit_eat

)  


.:  Fruit

```

```  
\> (relation Apple

uses Fruit

:Color red

)

.:  Apple  


```

```  
\> (relation Delicious

uses Apple

:Color yellow

)

.:  Delicious

  
```

###### The Identity Slot

Thoughts have an identity slot (^) that contains the identifier value which uniquely demarcates the thought. Some examples of thought identifiers are

```  
Sentence_1 Red_34 SOV_74

Vocalization_9202 Instance_983  
```

Thought premises also contain an identity slot. For example,

```  
\> (premise Red_1)

.:  \[Red ^ Red_1 :Object corvette :Size little\]

> (premise Event_29)

.:  \[Event ^ Event_29 :subject bird\]

```

A self reference value can be used when forming thoughts using the new function. Self (\\^) is equivalent to a "this" symbol in some structured languages such as C++, or the ?me symbol in Premise.

```  
(new Car :make Dodge :model RAM :year 2010 :id \\^)  
```

###### Methods

Methods are literals preceded by an exclamation point. Some examples are:

```  
!action !cleanup !onNew !onOld  
```

Relationships have several built in methods which can be implemented by the developer: a constructor (!onNew), destructor (!onOld), copy method (!onCopy), and an update method (!onSet). The !onNew method initializes a premise. The !onOld method disposes of a premise.

Calling a method will look up the function name located in the method and invoke the function on the arguments. The methods cloneMe and Concept_Add will be retrieved when invoked.

```  
\[MyObject !save saveMe !clone cloneMe\]

\[Concept :Datum 0 !add Concept_add \]  
```

There are two ways of invoking a method. Methods are invoked using the call function or by using the method name as a function (i.e, by placing the method name first in a call followed by the instance containing the method). A method not found failure will be thrown if the instance does not contain the method.

```  
(call !start car_255 ?myKey) ; invoking a method using the call function.

(!start car_255 ?myKey) ; invoking a method using the method name.  
```

When a call has a method as its first item and a premise or identifier as the second item, the call will return the value of applying the method to the remaining arguments.

```  
\> (relation Foo

:Datum 100

!add2 Foo_addTwo

)

  
.: Foo

> (function Foo_addTwo {?me}

(==> ?me + :Datum 2)

)

.:  Foo_addTwo

```

```  
\> (new Foo :Datum 1000)

  
.: Foo_1

> (:Datum Foo_1)

  
.: 1000

> (!add2 Foo_1)

  
.: 1002

  
```

##### Resources

A resource is a literal which represents a tuple. Resources can be created for tasks, files, assortments, data connections, and so forth. Typically a resource will indicate the type of resource, followed by a hyphen, followed by an integer resource number.

```

File-45 Task-32 Data-988

Lexicon-87 Environment-67 Colors

```

###### Assortments

Assortments are resources that hold unordered elements, associations, bindings, or enumerations.

Collections

Collections are sets that contain only keys. They are created with the collection function.

```

> (collection

the quick brown fox 21 "over the" lazy dogs \[MyObject ^ MyObject_32\] )

.:  Collection-1

```

Configuration

Configurations are key value pairs that are persisted to a file. They are created with the configuration function.

```

> (configuration "file://localhost.com/c$/apps/Premise/"

"/mind/agent/delay" \\@m35

"/mind/activation/history/maximum" 15)

.:  Configuration-1

```

Environments

Environments contain identifier to value bindings. They are created with the environment function.

```

> (environment nil

(symbol x) 32 times10 (given {?x} (\* ?x 10)) )

.:  Environment-1

```

Enumerations

Enumerations contain literal elements. Each element of the enumeration has a position. By default the first element will have position one, the second two, and so forth. If any of the arguments to the enumeration function is numeric, then that argument will set the position for the preceding literal. Enumerations are created with the enumeration function.

```

> (enumeration Colors red orange yellow )

.:  Enumeration-1

> (enumeration Controls clock 100 timer 200 start 300)

.:  Enumeration-2

```

Ephemerons

Ephemerons are manifested structures created with the new function. A Fault ephemeron can be defined as follows. Because they are short lived, ephemerons are represented as premises, and do not have a unique identifier. They keys for an ephemeron are fixed and are defined by the structure the ephemeron instantiates.

```

> (new Fault :What AnError :Where RightHere :When Now)  


.:  \[Fault :What AnError :Where RightHere :When Now\]  


> (new Message :Sender Me :Recipient Todd :Content "Hello There")

.:  \[Message :Sender Me :Recipient Todd :Content "Hello There"\]

```

Thoughts

A relation is a prototype defines a fixed record structure. A thought is an instance of a relation that has predefined keys, and can be added to memory using the new function. Each thought instance has a literal identifier. In the case below, Apple_1 and Delicious_34 are identifiers for thoughts.  

```

> (new Apple :Weight 2.0)

.:  Apple_1

> (new Delicious)

.:  Delicious_34

```

Lexicons

Lexicons contain value to value associations. They are created with the lexicon function.

```

> (lexicon

{a b c} "123" the {" t" " th" "the" "he " "e "} :Every body )

.:  Lexicon-1

> (entries Lexicon-1)

.:  {{a b c} "123"}{the {" t" " th" "the" "he " "e "}}{:Every body}}

```

###### Continuations

Continuations enable jumps into functions. They are created with the continuation function.

```

> (function factorial_hps {?n ?k}

(let ?a 1)

(continuation ?m ?a)

(if (<= ?n 0)

(continue ?k ?a)

else

(--> -- ?n)

(continue ?m (\* (++ ?n) ?a))))

.:  factorial_hps

> (function factorial {?n}

(let ?r nil)

(continuation ?k ?r)

(if (nil-p ?r) (factorial_hps ?n ?k) else ?r))

.:  factorial

> (factorial 5)

.:  120

```

###### Data

Data resources enable the use of information sources. They are created with the data function.

```

> (global ?Data (data driver sqlserver server "//servername" port 1433

database mydata user "myUid" password "123456")

.:  Data-1

> (fetch ?Data "select top 2 empid, name, salary from employee")

.:  {{1 "John Smith" 10.50}{2 "Jane Johnson" 12.00}}

> (disconnect ?Data)

.:  disconnected

```

###### Files

File resources enable the reading and writing of files. They are created with the file function.

```

> (write (file name "quick.txt" seek 1) "The quick brown fox")

.:  File-1

> (close file-1)

.:  closed

```

###### Tasks

Tasks are expressions that can be evaluated in separate threads of execution. They are created with the task function.

```

> (task (/ 1000 57) (** 4 20) (** 4 20))

.:  {Task-1 Task-2 Task-3}

> (complete task-1 task-2)

.:  {Task-1 Task-2}

> (await task-1)

.:  17.54385964912281

> (await task-2)

.:  1099511627776

> (concurrent task-3)

.:  {Task-3}

> (await task-3)

.:  1099511627776

> (free {task-1 task-2 task-3})

.:  freed

```

###### Indices

Index resources are used to increased the speed of instance retrieval. They are created with the index function.

```

> (relation Car :Make :Model :Year)

.:  Car

> (index Car :Make :Model)

.:  Car_Index_1

> (index Car :Model)

.:  Car_Index_2

> (new Car :Make A :Model M1)

.:  Car_1

> (with Car ^ as ?i :Model M1) list ?i)

.:  {Car_1}

> (drop Car_Index_1)

.:  dropped

> (drop Car_Index_2)

.:  dropped

```

##### Reserved Literals

Certain literals are keywords that have a distinctive meaning. Keywords can optionally be prefixed with \\% to be explicit about the use of the keyword. For example, the Truth reserved literals represents a possible logical states.

```  
true false unknown

  
\\%True \\%False \\%Unknown

```

##### Intrinsic Functions

The function literals that comprise the Premise Language are reserved and should not be redefined in their native modules since attempting to do so would redefine the behavior of the language.

##### Modules

Modules are name spaces. A module literal is used to avoid literal collisions and provide modularity in Premise code. Modules are delimited by dots (.) within a literal. There are several initial modules.

Apex Global environment

Base Foundational functions

IO File & Messaging functions

KB Knowledge access

Maths Mathematic functions

Tasks Task functions

User Default environment

All modules are global, meaning that the modules cannot be concatenated or nested. Modules are declared with the module function, and modified with the extend function, and deleted with the discard function.

## Containers

Containers are groupings of values. There are two kinds of containers, assortments and sequences. Assortments are unordered resource groupings. Sequences are ordered groupings of values.

### Sequences

Sequences are ordered groupings of values. The main function of a sequence is to group values into arrays, sets, or bags of items. The Premise Language provides functions for accessing sequences as a series of elements.

#### Expressions

Expressions are sequences of zero or more variants without delimiters. Expressions are usually found inside sequences such as lists, tuples, or calls.

```

an expression don't do that

another expression He said, Sure why not?

```

#### Lists

Lists are ordered groupings of values which evaluate to themselves. Lists are malleable so they can be extended or reduced and elements can be inserted or deleted. This malleability allows lists to represent stacks or queues or orderings. The empty list, { }, may be used in code for clarity. Lists are created with the list function.

```

{a b c} {1 2 3} {}

```

#### Vectors

Vectors are sequences of numbers delimited by pipes (vertical bar). Numbers are not supported as a distinct data type; instead a byte is an integer written in base 16.

```

|0| |1 2 3| |\\#nxFF \\#nxE2 \\#nxC8| |\\#gxFFE2C872|

```

#### Strings

Strings are sequences of characters delimited by double quotes. Characters are not supported as a distinct data type, instead characters are strings of length 1.

```

"a string" "don't do that"

"another string" "He said, 'Sure why not?'."

```

Backslashes provide character escaping. Doubling the backslash character within a string provides an escape for the backslash character. For Example \\\\ will represent a single \\. Other escape characters are as follows:

| Escape Sequences | Character Generated |
| --- | --- |
|     |     |
| \\\\ | \\  |
| \\' | '   |
| \\n | newline |
| \\t | tab |
| \\" | "   |
|     |     |

Character values can be generated using the backslash character. The octal values \\o0 to \\o177777, Unicode values \\u0000 to \\uFFFF, and decimal values \\d0 to \\d65535 can be contained in strings to select specific characters.

#### Tuples

Tuples are elements delimited by square brackets. For example \[1 2 3\] or \[a b c\]. Tuples are often used to represent relationships. Relationship tuples are comprised of a literal type and zero or more key-value pairs (called terms) enclosed in square brackets. For example

```

\[Fault :What nil :Where nil :When nil\]

```

is a tuple. Resources, ephemerons, and instances can all be represented as tuples.

##### Premises

Premises are tuples that represent language objects.

```

> (premise (new Fault :What "Printer Error" :Where "Line 287"

:When "2014-003-16T21:54"))

.:  \[Fault :What "Printer Error" :Where "Line 287" :When "2014-003-16T21:54"\]

```

For a relationship or thought, the premise function will retrieve a premise representation of the relationship or thought. The uses keyword coalesces many relations into one. Consider the following example where the get function retrieves the instance E_1.

```

> (relation A

:X 0

)

.:  A

> (relation B

:Y 1

)

.:  B

> (relation C

:Z 0  
)

.:  C

> (relation D  
uses A uses B uses C

)

.:  D  
```  
```  
\> (new D)

.:  D_1

> (premise D_1)

.:  \[D ^ D_1 :X 0 :Y 1 :Z 0\]

> (relation E

uses D

:Z 2

)  


.:  E

> (new E)  


.:  E_1

> (premise E_1)

.:  \[E ^ E_1 :X 0 :Y 1 :Z 2\]

```

##### Patterns

A pattern is a premise that is used to match thoughts. A pattern consists of a relation name or thought identifier list and some combination of slot bindings, slot tests, or both, enclosed within square brackets. A slot binding is a slot name, followed by as or each, followed by a symbol. A slot test is either a call containing a function that returns a truth value, or a slot name, followed by a predicate function name, followed by a value . Some examples of patterns are as follows:

```

\[Prediction :What ?what :Start ?start\] ; two slot bindings

\[Hypothesis ^ ?me :If ?if :Then ?then\] ; three slot bindings

\[Solution as ?s :Duration > \\@t5000\] ; one binding one test

```

Patterns can be used in with function calls in order to perform rule based inference. For example, we first create a relation and some instances like this:

```

> (relation Fact :All :Are)  
<br/>.: Fact

> (new Fact :All people :Are mortal)  
<br/>.: Fact_1

> (new Fact :All philosophers :Are people)  
<br/>.: Fact_2

```

Then the with expression can infer a conclusion

```

> (with \[Fact :All as ?S :Are as ?M\]

\[Fact :All = ?M :Are ?P)\]

get

(knew Fact :All ?S :Are ?P))

.:  \[Fact ^ Fact_3 :All philosophers :Are mortal\]

```

The patterns in the with expression above that matched the thoughts Fact_1 and Fact_2 are

```

\[Fact :All ?M :Are ?P\] matches Fact_1 and Fact_2

\[Fact ^ ?f :All ?S (= (:Are ?f) ?M)\] matches Fact_2 only.

```

Finally, the knew function attempts to find an existing thought whose slots match the values. If none are found, then the function creates a new thought.

```

> (knew Fact All ?S :Are ?P)  
<br/>.: Fact_3

```

#### Calls

A call is a parenthetical expression which when evaluated, will result in a value. For example, the expression (+ 1 2 3) is a call which when evaluated will result in the value 6. The first item in the expression is the left parenthesis, followed by a function literal followed by any actual parameters, followed by a right parenthesis. The function literal may be either a language intrinsic function or a user defined function. An empty call, (), returns itself.

```

(+ 1 2 3) (trim " abc ") ()

```

##### Functions

Functions (also called _exonyms_) are defined using function.

```

> (function foo {?a ?b}

(+ ?a ?b)

)

.:  foo

```

```  
\> (function bar {?a ?b}

(\* ?a ?b)

)

.:  bar

```

Functions are invoked by creating a call—wrapping the name and arguments in parentheses.

```

> (foo 10 20)  


.:  30

```

```  
\> (bar 10 20)  


.:  200  
```

###### Parameter Lists

There are several ways define the parameters to a function

1. No parameter list.

```

(function forgetEveryone

(each (with Person) old)

)

```

1. As a list containing zero parameters

```

(function helloWorld {}

(tell user "Hello World")

)

```

1. As a list containing one or more required parameters

```

(function addThem {?x ?y}

(+ ?x ?y)

)

```

1. As a list containing a variadic remainder parameter which contains all passed arguments.

```

(function addAll {& ?numbers}

(tell user ($ the sum of ?numbers is (apply + ?numbers) \\n))

)

```

1. As a list containing optional parameters.

```

(function result {+ ?y}

(--> default ?y 0)

(tell user ($ result = ?y \\n))

)

```

1. As a list containing optional parameters with default values.

```

(function result {+ ?y = 0}

(tell user ($ result = ?y \\n)) )

```

1. As a list containing required, optional, or remainder parameters.

```

(function result {?x + ?y = 1 & ?z}

(tell user ($ result = (apply \* (& ?x ?y ?z)) \\n))

)

```

1. As a list containing required and optional keyword parameters.

```

(function result {{color ?c} + % {length ?n} = 0 {width ?w} = 0

{height ?h} = 0}

(tell user ($ color ?c))

(tell user ($$ , \\s length \\s ?n , \\s width \\s ?w , \\s height \\s ?h) ))

)

```

1. Function parameters are automatically evaluated by default. Macro parameters are unevaluated by default.

```

(macro result {?x ?y ?z}

(tell user ($$ (eval ?x( ", " (eval ?y) ", " (eval ?z) \\n))

)

```

###### Parameter Specifications

Any required parameters are specified first. A failure is caused if a required parameter is not supplied with an argument when a function is called.

```

(function addThem {?x ?y} ; ?x and ?y are required.

"Add two numbers."

(+ ?x ?y)

)

```

The optional parameter sigil, the plus sign (+), precedes any optional ordered parameters. Optional parameters are processed sequentially and are bound to nil if no default values are specified.

```

(function AddTwoToFive {?a ?b + ?c = 0 ?d = 0 ?e}

"Add between two and five numbers."

(apply + (& ?a ?b ?c ?d ?e)

)

```

Default values may immediately follow an optional parameter symbol. The default value sigil, the equal sign (\=), precedes a default value to a symbol. Default values may only be literals, times, numbers, or strings. The default value must not be a symbol, resource, tuple, call, or list.

```

(function addThem {+ ?x = 0 ?y = 0}; ?x and ?y both default to zero.

"Add two numbers."

(+ ?x ?y)

)

```

A keyword parameter is a list containing a keyword pattern and symbol pair (e.g., {literal ?symbol}). Keyword parameters may be supplied instead of a symbol. They keyword literal is matched to the arguments and the value following the literal is placed into the symbol.

```

(macro myFor {?y {as ?x} & ?body}

(eval (\` (for , ?x in , ?y , ?body)))

)

```

A function or macro containing required keyword parameters would be called as follows

```

(myFor {Jane Jack Joe} as ?name (tell user ($ ?name \\n)))

```

Optional keywords are matched sequentially. Unordered keywords require the unordered keywords sigil, the percent sign (%). Unordered keyword arguments are matched in any order they occur in the argument list if their formal parameters follow the unordered keywords sigil.

```

(macro myStep { ' ?v {from ?a} + % {to ?z} {by ?i} = 1 & ?body}

(eval (\` (step , ?v from , ?a to , ?z by (default , ?i 1) , ?body)))

)

```

A variadic parameter sigil, the ampersand (&), ties the remaining arguments together into a list for the subsequent symbol. Only one symbol is permitted after the ampersand. The remainder parameter will be bound to an empty list if no actual parameters are supplied.

```

(function AddTwoOrMore {?x ?y & ?z}

(if (void-p ?z)

(+ ?x ?y)

else

(apply + (& ?x ?y ?z)))

)

```

It would be called as follows

```

(myStep ?i to 100 by 2 from 1 (tell user ($ ?i \\n)))

```

In functions, all arguments are evaluated before the function body is applied. This is not the case for macros. Macro parameters remain unevaluated until they are explicitly evaluated with the eval function within the body of the macro definition.

```

(macro callLength {?f}

(ensure Call ?f)

(# (eval ?f))

)

```

More examples…

```

(function foo

"No parameter list."

(do nothing))

(function foo {}

"Zero length param list."

(do nothing))

(function foo {?x ?y}

"Fixed number of required parameters."

(+ ?x ?y))

(function foo {+ ?x = 0 ?y = 0}

"Optional parameters with default values."

(+ ?x ?y))

(function foo {?w + ?x ?y & ?z}

"Required, optional, and remaining parameters."

(--> default ?x 0)

(--> default ?y 0)

(apply + (& ?w ?x ?y ?z)))

(function foo {+ ?w = 0 ?x = 0 ?y = 0 & ?z }

"Optional and remaining parameters with default values."

(apply + (& ?w ?x ?y ?z)))

(macro define {?name ?args & ?body}

"Unevaluated parameters."

(eval (\` (function , ?name , ?args ,_ ?body))))

```

###### Auto-named Functions

Auto-named functions (also called _endonyms_) are created by omitting the function name in the definition. When the function name is omitted, the Premise interpreter will automatically generate a function name for the function.

```  
\> (function {?x ?y}

(\* ?x ?y)

)

.:  fn-24

```

```  
\> (function {& ?args}

(apply \* ?args)

)

.:  fn-25

```

```  
\> (function

(with Truck ^ as ?t

do (old ?t)))  


.:  fn-26  
```

###### Anonymous Functions

Anonymous functions (i.e., also called _anonyms_) are implemented using given. An anonym expression can stand in for a named or auto-named function call.

```  
\> ((given {?x ?y} (\* ?x ?y)) 2 3) ; same effect as (fn-24 2 3)

.:  6

```

###### Generators

A generator is a function that creates a series. Generators are created using the generator function. When a generator is invoked it will produce a series.

```  
\> (generator generateABC {}

(yield a)

(yield b)

(yield c)

(stop))

.:  generateABC

> (collect ?e in (generateABC) ?e)

.:  {a b c}

> (generateABC)

.:  {...}

```

###### Macros

A macro is a call that evaluates an expanded expression. Macros are defined using macro. The back quote function (\`) expands an expression by substituting subexpressions that follow commas, then it evaluates the resultant expression.

```

> (macro plus {?a ?b}

(eval (\` (+ , ?a , ?b)))

)

.:  plus

```

```  
\> (macro prod {?a ?b}

(eval (\` (\* , ?a , ?b)))

)

.:  prod

```

Macros are invoked by wrapping the macro name and arguments in parentheses.

```

> (plus 10 20)

.:  30

```

```  
\> (prod 10 20)

.:  200

```

# 4\. Control Flow

The following expressions permit alterations to the normal sequential flow of expression evaluation.

## Conditional Expressions

Conditional expressions branch the flow of evaluation to alternate paths.

### if

The if special form provides branched conditional flow of evaluation.

```

> (if (= 1 2)

(tell user ($ An impossibility.))

(tell user ($ I'm certain. \\n))

or (= 2 1)

(tell user ($ Another impossibility.))

(tell user ($ Most definitely. \\n))

or (/= 1 1)

(tell user ($ A total absurdity.))

(tell user ($ Without a doubt. \\n))

else

(tell user ($ The world is right as rain. \\n))

HelloWorld)

The world is right as rain.

.:  HelloWorld

```

### case

The case special form provides branching based on a value.

```

> (case red

of green (tell user ($ Nature's)) (tell user ($ glory. \\n))

of blue (tell user ($ A wondrous)) (tell user ($ beauty. \\n))

in {brown black purple indigo violet} (tell user ($ A fabulous selection. \\n))

else

(tell user ($ Hmmm... I didn't consider that one.))

(tell user ($ ($) Bravo. \\n))

Hmmm... I didn't consider that one. Bravo.

.:  nil

```

### on

The on special form provides branched conditional flow of evaluation.

```

> (on (= 1 2)

(tell user ($ A truth.))

(tell user ($ An impossibility. \\n)))

An impossibility

.:  told

> (on (= 1 1)

(tell user ($ Without a doubt. \\n))

(tell user ($ A total absurdity.)))

Without a doubt.

.:  told

```

### do

The do special form provides subroutine resumption.

```

> (do

(escape)

(never-happens)

resume

(tell user ($ Resumed execution \\n))

finally

(tell user ($ Done. \\n)))

Resumed execution

Done.

.:  told

```

### try

The try special form provides exception handling,

```

> (try

(signal \[Failure :Name MyFault :Text "Failed Miserably"\])

learn ?failure

(tell user ($ Handled ?failure \\n))

finally

(tell user ($ Done. \\n)))

Handled \[Failure :Name MyFault :Text "Failed Miserably"\]

Done.

.:  told

```

## Looping Expressions

Certain expressions are used to loop through a sequence or iterate over a series of values.

### loop

The loop special form allows conditional repetition of one or more expressions.

```

> (global ?I 100)

.:  true

> (loop (--> -- ?I) until (= ?I 90))

.:  90

> (loop (--> ++ ?I) while (< ?I 100))

.:  100

> (loop (--> -- ?i) repeat 100)

.:  0

```

### for

The for special form repeatedly binds one or more variables through elements of a sequence.

```

> (for ?x in {hello world} (tell user ($$ ?x \\s)))

hello world .: told

> (for ?x in "hello world" (tell user ($$ ?x \\s)))

h e l l o w o r l d .: told

> (for ?k ?v in {a 1 b 2 c 3 d 4}

(tell user ($ ?k ($$ ?v ,))))

a 1, b 2, c 3, d 4, .: told

> (for ?x ?y ?z per {{a 1 $}{b 2 @}{c 3 #}{d 4 /})

(tell user ($ ?x ?y ($$ ?z ,))))

a 1 $, b 2 @, c 3 #, d 4 /, .: told

```

### step

The step special form increments or decrements a symbol over a series of numeric values.

```

> (step ?i from 5 to 9

(tell user ($$ "?i = " ?i ", " )))

?i = 5, ?i = 6, ?i = 7, ?i = 8, ?i = 9, .: told

> (step ?i from 100 to 50 by -10

(tell user ($$ "?i = " ?i ", " )))

?i = 100, ?i = 90, ?i = 80, ?i = 70, ?i = 60, ?i = 50, .: told

> (step ?i from 0 to 0.5 by 0.1

(tell user ($$ "?i = " ?i ", " )))

?i = 0, ?i = 0.1, ?i = 0.2, ?i = 0.3, ?i = 0.4, ?i = 0.5, .: told

```

### repeat

The repeat special form allows repetition of one or more expressions for a specified number of iterations.

```

> (repeat 1000 (--> ++ ?i))

.:  1100

> (repeat 5 (tell user ($$ hi \\s))

hi hi hi hi hi .: told

```

### count

The count special form repeatedly binds one or more variables to elements of a sequence and returns the count..

```

> (count ?x in {the quick brown fox} as ?total

(tell user ($ ?x \\t)))

the quick brown fox .: 4

```

### while

The while special form allows repetition of one or more expressions while a condition is true.

```

> (global ?N 0)

.:  true

> (while (< ?N 5)

(tell user ($ ?N \\n))

(--> ++ ?N))

0

1

2

3

4

.:  5

```

### until

The until special form provides repetition of one or more expressions until a condition is true.

```

> (global ?S {a b c d 1 2 3 4} ?i 0 ?result {})

.:  true

> (until (number-p (@ ?S (--> ++ ?i))) ; until S\[++?i\] is a number

(--> & ?result {{(@ ?S ?i) bar}})) ; merge ?result with { S\[?i\] bar }

.:  {{a bar}{b bar}{c bar}{d bar}}

```

## Control Flow Expressions

Control flow expressions redirect the flow of control.

### confirm

The confirm special form signals a failure if the test fails.

```

> (function multiply {?a ?b}

(confirm (taxon-p ?a number) since ($ ?a must be a number))

(confirm (taxon-p ?b number) since ($ ?b must be a number))

(\* ?a ?b))

.:  multiply

> (multiply 10 banana)

.:  \[Failure :Name DataTypeFailure :Text "banana must be a number"\]

```

### confute

The confute special form signals a failure if the test succeeds.

```

> (confute (= red blue) since "colors must be different")

.:  false

> (function reducing {?sequence ?function}

(ensure sequence ?sequence function ?function)

(confute (<= (# ?sequence) 1) since "Two or more elements are required.")

(let ?result (@ ?sequence))

(for ?element in (rest ?sequence) (--> ?function ?result ?element)))

.:  reducing

> (reducing {1} +)

.:  \[Failure :Name Confutation :Text "Two or more elements are required."\]

```

### break

The break special form transfers control out of the containing loop.

```

> (do (step ?i from 1 to 10

(if (= ?i 3) (break nil))

(tell user ($ ?i \\n)))

(tell user ($ done \\n)))

1

2

done

.:  nil

```

### continue

The continue special form transfers control to the next iteration of the containing loop.

```

> (for ?letter in "Premise"

(if (in "meis" ?letter) (continue))

(tell user ($ Letter is ($$ ?letter .) \\n)))

Letter is P.

Letter is r.

.:  nil

```

### exit

The exit special form transfers control out of the current task. Whereas return may exit from a nested function, exit terminates the task. Exit can be thought of as a task level return.

```

> (concurrent

(step ?x from 1 to 999999999

(if (> ?x 100) (exit exited))))

.:  {Task-1}

> (await task-1)

.:  exited

> (free task-1)

.:  freed

```

### signal

The signal special form transfers control to an encompassing try expression.

```

> (function myFun

(try

(signal \[Failure :Name BadAttitude :Text "example"\])

learn ?f

(case (:Name ?f)

of BadAttitude

(tell user ($ Caught inside myFun. \\n))

(signal ?f)))

)

.:  myFun

> (function main {& ?args}

(try

(myFun)

learn ?f

(case (:Name ?f)

of BadAttitude

(tell user ($ Caught inside main. \\n))))

)

.:  main

> (main)

Caught inside myFun.

Caught inside main.

.:  nil

```

### return

The return special form transfers control out of the current function.

```

> (function a {?i} (if (= ?i 5) (return nil)) (tell user ($ ?i \\n)))

.:  a

> (function b {?i} (if (> ?i 4) (return 4 from b)) (tell user ($ ?i \\n)) (return 2))

.:  b

> (function c {?k ?v} (return {?k ?v} from function))

.:  c

> (function d (a 30))

.:  d

> (do

(a 5)

(a 1)

(let ?i (b 5))

(tell user ($ ?i \\n))

(tell user ($ (@ (c 100 90) 2) \\n))

(d))

1

4

90

30

.:  nil

```

### ensure

The ensure special form transfers control to an encompassing try expression if a type check fails.

```

> (function multiply {?a ?b}

(ensure number ?a number ?b)

(\* ?a ?b))

.:  multiply

> (multiply 10 banana)

.:  \[Failure :Name EnsureType :Text "The value banana must be a number"\]

> (multiply 10 5)

.:  50

```

### escape

The escape function transfers control to an encompassing do expression containing a resume tag.

```

> (do

(escape)

resume here

(tell user ($ Resumed execution \\n))

finally

(tell user ($ Done. \\n)))

Resumed execution

Done.

```

### go

The go special form transfers control to a function.

```

> (relation Queue :Items {} :Capacity 10

!count (given {?me}(# (:Items ?me)))

!full-p (given {?me}(>= (!count ?me) (:Capacity ?me))))

.:  Queue

> (function produce {?q}

(tell user ($ producing \\n))

(if (not (!full-p ?q))

(repeat (random 1 to (- (:Capacity ?q) (!count ?q)))

(enq ?q :Queue (new Item))))

(go consume ?q))

.:  produce

> (function consume {?q}

(tell user ($ consuming \\n))

(if (more-p (:Queue ?q))

(repeat (random 1 to (# (:Queue ?q)))

(deliver (pop (:Queue ?q)))))

(either (void-p (:Queue ?q))

done

(go produce ?q))

> (produce (new Queue))

producing

consuming

producing

consuming

producing

consuming

producing

consuming

producing

consuming

producing

consuming

producing

consuming

producing

consuming

producing

consuming

producing

consuming

.:  done

```

## Multitasking Expressions

The Premise Language facilitates asynchronous and concurrent expression evaluation.

### concurrent

The concurrent function runs expressions asynchronously and returns immediately.

```

> (concurrent (+ 1 2 3 4) (/ 1000 57))

.:  {task-1 task-2}

> (await task-1)

.:  10

> (await task-2)

.:  17.54385964912281

> (free {task-1 task-2})

.:  nil

```

### complete

The complete function executes expressions concurrently and returns after all have completed.

```

> (complete (step ?i from 0 to 50000000 (do nothing))

(step ?i from 1 to 10000000 (do nada)))

.:  {Task-1 Task-2}

> (await task-1)

.:  nothing

> (await task-2)

.:  nada

> (free {task-1 task-2})

.:  freed

```

### scatter

The scatter function applies functions in parallel and returns a list of results.

```

> (function double {?x} (\* ?x 2))

.:  double

> (scatter {5} {++ -- double})

.:  {6 4 10}

> (scatter {{the quick brown fox jumped over the lazy dogs}}

{except rest top last})

.:  {{the quick brown fox jumped over the lazy }

{quick brown fox jumped over the lazy dogs}

{the}

{dogs}}

> (scatter {2 3 4} {+ \* -})

.:  {9 24 -5}

```

# 5\. Code Examples

The following are simple examples demonstrating the language.

## Inference

Logical pattern matching and declarative inference.

```

(relation Statement

:All

:Are

)

(new Statement :All people :Are mortal)

(new Statement :All philosophers :Are people)

(with \[Statement :All as ?s :Are as ?m\]

\[Statement :All = ?m :Are as ?p\]

list

(knew Statement :All ?s :Are ?p))

```

```

> (relation Statement

:All

:Are

)

.:  Statement

> (new Statement :All people :Are mortal)

.:  Statement_1

> (new Statement :All philosophers :Are people)

.:  Statement_2

> (with \[Statement :All as ?s :Are as ?m\]

\[Statement :All = ?m :Are as ?p\]

list

(knew Statement :All ?s :Are ?p))

.:  {Statement_3}

> (with Statement)

.:  {\[Statement ^ Statement_1 :All people :Are mortal\]

\[Statement ^ Statement_2 :All philosophers :Are people\]

\[Statement ^ Statement_3 :All philosophers :Are mortal\]}

```

## Memoization

Memoization is the process of saving intermediate results for lookup rather than recomputation. Once a value has been computed, it can be memorized so that if the value is needed again, it can be easily retrieved rather than recomputed. The following example uses memoization in computing Fibonacci numbers.

```

> (relation Memoized

&nbsp;  :Number

&nbsp;  :Result

&nbsp;)

.:  Memoized

> (new Memoized :Number 0 :Result 0)

.:  Memoized_1

> (new Memoized :Number 1 :Result 1)

.:  Memoized_2

> (function fib {?n}

&nbsp;  (confirm (>= ?n 0) since

($ ?n must be zero or more.))

&nbsp; (with

\[Memoized ^ :Number as ?n :Result as ?r\] ; if a matching instance exists

do

(return ?r)) ; then return, otherwise do nothing

(let ?result (+ (fib (- ?n 1)) (fib (- ?n 2))))

(new Memoized :Number ?n :Result ?result)

(return ?result)

)

.:  fib

> (fib 7)

.:  13

> (with Memoized)  
<br/>.: {\[Memoized ^ Memoized_1 :Number 0 :Result 0\]

\[Memoized ^ Memoized_2 :Number 1 :Result 1\]

\[Memoized ^ Memoized_4 :Number 3 :Result 2\]

\[Memoized ^ Memoized_6 :Number 5 :Result 5\]

\[Memoized ^ Memoized_3 :Number 2 :Result 1\]

\[Memoized ^ Memoized_8 :Number 7 :Result 13\]

\[Memoized ^ Memoized_7 :Number 6 :Result 8\]

\[Memoized ^ Memoized_5 :Number 4 :Result 3\]}

```

## Programming Patterns

Event driven programming.

```

> (structure Event

:Topic

:Content

)

.:  Event

> (relation Fault

:Who

:What

:Where

:When

)

.:  Fault

> (function dispatcher {?message}

(try

(let ?taken (take ?message)

?event (either (takeable-p ?taken) (@ ?taken) else nil)

(ensure Event ?event)

(let ?event :Topic as ?topic :Content as ?content)

(case ?topic

of Percept (onPerceptReceived ?content)

of Ping (onPingReceived ?content)

else

(signal \[Failure :Name BadTopic :Text ($ Unknown topic ?topic)\]))

(tell user ($ Handled ?message))

learn ?failure

(new Fault :Who Dispatcher :What ?failure :When (date)

:Where {dispatcher ?message}))

)

.:  dispatcher

> (global ?URL (config "/application/eventUrlAndPort"))

.:  true

> (listener ?URL dispatcher) ; creates a message loop

.:  Listener-1

> (tell ?URL ($ (new Event :Topic Ping :Content {:Sent (moment)}))))

.:  told

Handled \[Event :Topic Ping :Content {:Sent \\@m201804991265124}\]

> (free Listener-1 cancel yes)

.:  freed

```

## Similarity Based Matching

The ~ and best language intrinsics perform similarity based comparisons to support case-based reasoning.

```

> (~ {a b c} {a d e})

.:  0.2

> (~ "a b c" "a d e")

.:  0.090909091

> (~ 57 890)

.:  0.00119904076738

> (best 2001 (range 1 to 1000000) 5)

.:  {{2001 1} {2000 0.5} {2002 0.5} {1999 0.33333333333333333}

{2003 0.33333333333333333}}

> (best "this" {"that" "hat" "hit" "with" "isthmus"} 3)

.:  {{"that" 0.11111111111111111} {"hat" 0.08333333333333333}

{"hit" 0.08333333333333333}}

```

## Asynchrony and Concurrency

The concurrent, complete, and task functions run expressions asynchronously, concurrently, or as required. The concurrence function complete returns after all tasks have completed whereas the asynchronicity function concurrent returns immediately after invocation. The task function creates a task for deferred execution. The functions each return a list of task handles.

```

> (concurrent (step ?i from 1 to 30000000 (do something)) ; runs asynchronously

(step ?j from 1 to 60000000 (do something-else)))

.:  {Task-1 Task-2}

> (ready-p task-1)

.:  false

> (await task-1)

.:  something

> (await task-2 1000 timed-out) ; adding timeout and default args

.:  timed-out

```

```

> (await task-2)

.:  something-else

> (free {task-1 task-2})

.:  freed

> (complete (step ?i from 1 to 30000000 (do someOtherThing)) ; runs concurrently

&nbsp;  (step ?j from 1 to 60000000 (do anotherThing)

&nbsp;   (step ?k from 1 to 100000000 (do oneLastThing))

.:  {Task-3 Task-4 Task-5}

> (cancel task-5)

.:  cancelled

> (await task-3 0 timed-out)

.:  someOtherThing

> (await task-4 0 timed-out)

.:  anotherThing

> (free {task-3 task-4})

.:  freed  
<br/>\> (function sayHello {}

(for ?c in "hello " (tell user ($ ?c))))

.:  sayHello

> (global ?Tasks (task (sayHello) (sayHello) (sayHello) (sayHello)))

.:  true

> (free (complete ?Tasks))

hhehelelohl lello l ol o .: freed

> (function sayHello {}

(critical printing

(for ?c in "hello " (tell user ($ ?c)))))

.:  sayHello

> (set ?Tasks (task (sayHello) (sayHello) (sayHello) (sayHello)))

.:  true

> (free (complete ?Tasks))

hello hello hello hello .: freed

> (undeclare ?Tasks)

.:  undeclared

```

## Sequences

A sequence is a string, a list, a call, or a tuple. The language provides functions to manipulate sequences (e.g, # element, make, bind, for).

```  
\> (@ "ABC" 2) ; find the second element of the string

.:  "B"

> (@ {The quick brown fox jumped over the lazy dogs} 5)

.:  jumped

> (copy {A B C} 1 X 3 Z)  ; copy list, replacing positions 1 and 3

.:  {X B Z}

> (copy "ABC" 1 X 3 Z) ; copy string, replacing positions 1 and 3

.:  "XBZ"

> ?v1

.:  \[Failure :Name UndefinedSymbol :Text "Symbol ?v is undefined."\]

> (let {A B C} 1 ?v1 2 ?v2)

.:  true

> ?v1

.:  A

> (let "ABC" 1 ?s1 2 ?s2)

.:  true

?s1

.:  "A"

> ?s2

.:  "B"  


> (for ?c in "the quick brown fox"

(tell user ($ ?c)))

the quick brown fox .: told

> (for ?n in {1 2 3}

(tell user ($$ (\* ?n 10) \\s )))

10 20 30 .: told

```

## Tuples

Premises are tuples and there are specific functions to manipulate premises (e.g., get, let, set, zap).

```

> (relation Foo :Bar :Baz)

.:  Foo

> (new Foo :Bar 100)

.:  Foo_1

> (premise Foo_1)

.:  \[Foo ^ Foo_1 :Bar 100 :Baz nil\]

> ?bar

.:  \[Failure :Name UndefinedSymbol :Text "Symbol ?bar is undefined."\]

> (let (premise Foo_1) :Bar as ?bar)

.:  true

> ?bar

.:  100

> (put Foo_1 :Baz "The quick brown fox")

.:  Foo_1

> (zap Foo_1 :Bar)

.:  Foo_1

> (premise Foo_1)

.:  \[Foo ^ Foo_1 :Bar nil :Baz "The quick brown fox"\]

> (zap Foo_1)

.:  Foo_1

> (premise Foo_1)

.:  \[Foo ^ Foo_1 :Bar nil :Baz nil\]

```

## Assortments

Assortments are resources that contain unordered items. Assortments such as collections, lexicons, environments, and enumerations are provided along with specific functions to manipulate them (e.g., add, cut, item, keys, put, the, tie, values, etc.).

```

> (lexicon q nil)

.:  Lexicon-1

> (add Lexicon-1 "z" foo)

.:  Lexicon-1

> (add Lexicon-1  84 nil)

.:  Lexicon-1

> (entries Lexicon-1)

.:  {{q nil}{'z' foo}{84 nil}}

> (cut Lexicon-1 "z")

.:  Lexicon-1

> (entries Lexicon-1)

.:  {{84 nil}{q nil}}

> (lexicon :Length 24 :Width 12 :Height 9 :Units inch)

.:  Lexicon-2

> (@ Lexicon-2 :Length)

.:  24

> (@ Lexicon-2 :Width)

.:  12

> ?width

.:  \[Failure :Name UndefinedSymbol :Text "Symbol ?width is undefined."\]

> ?height

.:  \[Failure :Name UndefinedSymbol :Text "Symbol ?height is undefined."\]

> (bind Lexicon-2 :Width ?width :Height ?height)

.:  true

> ?width

.:  12

```

```

> ?height

.:  9

> (keys Lexicon-2)

.:  {:Height :Length :Units :Width}

> (values Lexicon-2)

.:  {inch 12 24 9}

> (enumeration Colors

red orange yellow green blue indigo violet)

.:  Enumeration-1

> (@ Enumeration-1 red)

.:  1

> (keys (enum Colors))

.:  {red orange yellow green blue indigo violet}

> (values Enumeration-1)

.:  {1 2 3 4 5 6 7}

> (@ Enumeration-1 green)

.:  4

> (entries Enumeration-1)

.:  {{red 1}{orange 2}{yellow 3}{green 4}{blue 5}{indigo 6}{violet 7}}

> (enumeration Controls  

&nbsp;

clock 100

timer 200

start 300)

.:  Enumeration-2  

> (@ (enum Controls) timer)

.:  200

> (keys Enumeration-2)

.:  {clock start timer}

> (collect ?key ?value per (sort (entries Enumeration-2) {< 2}) ?key)

.:  {clock timer start}  
```

```

> (enumeration Highways

&nbsp;Maine-Miami             ; defaults to 1

&nbsp;  Maine-Idaho              ; defaults to 2

&nbsp;  Michigan-Washington 10

&nbsp;  NewYork-Louisiana        ;will be 11

&nbsp;  Massachusetts-Oregon 20

&nbsp;  Ohfile-Florida             ; will be 21

&nbsp;  NewJersey-Oregon 30

&nbsp;  Michigan-Alabama

&nbsp;  NewJersey-California 40

&nbsp;  Michigan-Florida

&nbsp;  Maryland-Nevada  50

&nbsp;  Wisconsin-Louisiana

&nbsp;  Illinois-California 60

&nbsp;  Minnesota-Louisiana

&nbsp;  NorthCarolina-Arizona  70

&nbsp;  JeffersonHighway

&nbsp;  Georgia-California 80

&nbsp;  NorthDakota-Texas

&nbsp;  Florida-Texas 90

&nbsp;  Montana-Nevada

&nbsp;  Washington-California 101)

.:  Enumeration-3

> (sort (values (enum Highways)) <)

.:  {1 2 10 11 20 21 30 31 40 41 50 51 60 61 70 71 80 81 90 91 101}

> (@ (enum Highways) NewJersy-California)

.:  40

```

## Rules

The rule function creates a rule that asynchronously match thoughts. Rules are run spontaneously when thoughts match the rule’s preconditions. There is no guarantee as to when or whether a particular rule will execute. The rule may be cancelled and reclaimed using the reclaim function.

```

> (reasoning)

.:  false

> (reasoning on)

.:  true

> (relation Summation :Result 0)

.:  Summation

> (relation Addend :Value 0 :Status pending)

.:  Addend

> (rule

when \[Summation ^ as ?sum\]

\[Addend ^ as ?add :Value as ?value :Status = pending\]

do

(==> ?sum + :Result ?value)

(put ?add :Status added))

.:  Rule-1

> (new Addend :Value 5)

.:  Addend_1

> (premise Addend_1)

.:  \[Addend ^ Addend_1 :Value 5 :Status pending\]

> (new Summation)

.:  Summation_1

> (premise Summation_1)

.:  \[Summation ^ Summation_1 :Result 5\]

> (premise Addend_1)

.:  \[Addend ^ Addend_1 :Value 5 :Status added\]

> (new Addend :Value 7)

.:  Addend_2

> (premise Addend_2)

.:  \[Addend ^ Addend_2 :Value 7 :Status added\]

```

```

> (premise Summation_1)

.:  \[Summation ^ Summation_1 :Result 12\]

> (new Addend :Value 11)

.:  Addend_3

> (premise Addend_3)

.:  \[Addend ^ Addend_3 :Value 11 :Status = added\]

> (premise Summation_1)

.:  \[Summation ^ Summation_1 :Result 23\]

> (free Rule-1)

.:  freed

> (rule when \[Addend ^ as ?a :Status = added\] do (old ?a))

.:  Rule-2

> (with Addend)

.:  {}

> (with Summation)

.:  {\[Summation ^ Summation_1 :Result 23\]}

> (old Summation_1)

.:  gone

> (nix Summation)

.:  nixed

> (nix Addend)

.:  nixed

> (free (rules))

.:  freed

> (reasoning off)

.:  false

```

## Functions

Functions are defined using the function intrinsic. Function names may not be preceded by a question mark. Functions may have no parameter list, an empty parameter list, or a list containing, required, optional, remainder or keyword parameters.

```

> (function factorial {?n} ; named function with a parameter list

(reduce (range 1 to ?n) \*)

)

.:  factorial

> (factorial 4)

.:  24

  
\> (function prime-p {?n} ; named function with required parameter

(if (< ?n 2)

(return false)

else

(step ?i from 1 to (++ (ceiling (root ?n)))

(if (and (> ?i 1)(< ?i ?n)(zero-p (% ?n ?i)))

(return false))))

true

)

.:  prime-p

> (prime-p 2)

.:  true

> (prime-p 6)

.:  false

> (function sum {& ?args} ; named function with a remaining parameter symbol

returns number ; with return type restriction

(apply + ?args)

)

.:  sum

> (sum 1 2 3 4)

.:  10

```

```  
\> (function addTwoToFive {?1 ?2 + ?3 = 0 ?4 = 0 ?5 = 0} ; named function with optional

(apply + (& ?1 ?2 ?3 ?4 ?5)) ; defaulted parameters

)

.:  addTwoToFive

> (addTwoToFive 5 5)

.:  10

> (addTwoToFive 5 6 7 8)

.:  26

> (function addAll {?1 ?2 + ?3 = 0 ?4 = 0 & ?rest} ; named function with optional and

&nbsp;  (apply + (& ?1 ?2 ?3 ?4 ?rest)) ; remainder parameters

)

.:  addAll

> (addAll 1 2 3 4 5 6 7 8 9 10)

.:  55

> (function forgetIt {?relation} ; named function  
(confirm (relation-p ?prototye) since ($ ?relation must be a relation.))  
 (for ?x in (with ?relation) (old ?x))

forgotten

)

.:  forgetIt

> (with Statement)

.:  {\[Statement ^ Statement_1 :All people :Are mortal\]

\[Statement ^ Statement_2 :All philosophers :Are people\]

\[Statement ^ Statement_3 :All philosophers :Are mortal\]}

> (forgetIt Statement)

.:  forgotten

> (with Statement)

.:  {}

> (function {& ?args} ; auto-named function with

(apply \* ?args) ; remaining parameter symbol

)

.:  fn-1

```

```  
\> (fn-1 1 2 3 4)

.:  24  
<br/>\> (function transitivity ; no parameters  
(with \[Statement :All as ?a :Are as ?b\]  
\[Statement :All = ?b :Are as ?c\]  
do  
(knew Statement :All ?a :Are ?c))  
)  
<br/>.: transitivity

> (macro myFor {?x {in ?y} & ?body} ; a required keyword parameter  
  (eval (\` (apply for (& , ?x in , ?y ,_ ?body))))

)

.:  myFor

> (myFor ?name in {Jane John Sally} (tell user ($ ?name \\n)))

Jane

John

Sally

.:  told

> (macro myStep {?v {from ?a} {to ?z} + {by ?i = 1} & ?body} ; optional keyword  
  (eval (\` (step , ?v from , ?a to , ?z by , ?i ,_ ?body))))

)

.:  myStep

> (myStep ?x from 1 to 5 by 2 (tell user ($ ?x \\n)))

1

3

5

.:  told  
<br/>

> (myStep ?x from 1 to 5 (tell user ($ ?x \\n)))

1

2

3

4

5

.:  told  
```

## Modules

Modules are literals that encapsulate function definitions. In practice, a function has a module preceding the function name, (as in “module.function”). Functions having a module in their literal are “qualified”. Functions without modules are “unqualified”. The module intrinsic creates modules. The extend intrinsic allows more function definitions to be added to a module. The using intrinsic sets or returns the current module. The require intrinsic allows functions to be visible between modules.

```

> (modules) ; view the modules collection

.:  {Apex Base IO KB Math Tasks User}

> (use User) ; work in a specific module

.:  User

> (module Arithmetic ; define a new module Arithmetic

(function sum {& ?args}

(apply + ?args)

)

)

.:  Arithmetic

> (modules)

.:  {Arithmetic Apex Base IO KB Math Tasks User}

> (sum 1 2 3 4) ; is sum visible from user module?

.:  \[Failure :Name ArgumentValue :Text "The function sum isn't found"\]

> (Arithmetic.sum 1 2 3 4) ; is fully qualified function visible?

.:  10

> (require Arithmetic as a) ; user module requires definitions

.:  Arithmetic

> (sum 1 2 3 4) ; now sum is visible

.:  10

> (a.sum 1 2 3 4) ; now a.sum is visible

.:  10

> (Arithmetic.sum 1 2 3 4) ; still accessible as Arithmetic.sum

.:  10

```

```

> (extend Arithmitic

(function product {& ?args} ; add a new function

(apply \* ?args)

)

)

.:  Arithmetic

```

## Delegates

Delegates are functions that are passed as parameters to other functions.

```

> (relation Product :Name :Price )

.:  Product

> (relation Cart :Items {} !total Cart_Total )

.:  Cart

> (function Cart_Total {?me ?SubTotDelegate ?TotalDelegate ?DiscountDelegate}

(ensure Cart ?me Function ?SubTotDelegate Function ?TotalDelegate

Function ?DiscountDelegate)

(let ?subTotal (sum (map (:Items ?me) :Price)))

(?SubTotDelegate ?subTotal)

(?DiscountDelegate ($ Discounts applied.\\n))

(?TotalDelegate (:Items ?me) ?subTotal))

.:  Cart_Total

> (relation Program :Cart !onNew (given {?me}(put ?me :Cart (new Cart))))

.:  Program

> (function main {& ?args}

(let ?me (new Program))

(enq (:Cart ?me) :Items (new Product :Name Cheese :Price 5.50))

(enq (:Cart ?me) :Items (new Product :Name Bread :Price 7.00))

(enq (:Cart ?me) :Items (new Product :Name Milk :Price 4.65))

(enq (:Cart ?me) :Items (new Product :Name Eggs :Price 5.95))

(tell user ($ Your total is

(!total (:Cart ?me)

(given {?sub}(tell user ($ The subtotal is ?sub \\n)))

(given {?products ?sub}

(if (> (# ?products) 3)

(\* ?sub 0.90)

else ?sub))

(given {?msg}(tell user ?msg)))

\\n \\n)))

.:  main

> (main)

The subtotal is 23.10

Discounts Applied.

Your total is 20.7

.:  told

```

## Poker Hand Analyzer

This function tells what kind of poker hand each player has.

```

> (enumeration Suits

Clubs Diamonds Hearts Spades

)

.:  Enumeration-1

> (enumeration Ranks

Ace Two Three Four Five Six Seven

Eight Nine Ten Jack Queen King Joker

)

.:  Enumeration-2

> (relation Card

:Rank

:Suit

:Dealt

)

.:  Card

> (relation Player

:Order

:Cards {}

:Hand Unknown

)

.:  Player

> (function setup

(repeat 2 ; use 2 decks

(for ?suit ?i per (entries (enum Suits))

(for ?rank ?j per (entries (enum Ranks))

(if (/= ?rank Joker) (new Card :Rank ?rank :Suit ?suit)))))

(let ?order 0)

(repeat (random 2 to 8) (new Player :Order (--> ++ ?order)))

)

.:  setup

> (function deal

(with Card ^ as ?card do (bind ?card :Dealt false))

(with Player ^ as ?player do (bind ?player :Cards {} :Hand unknown))

(let ?players (which Player sort :Order < )

?cards (shuffle (which Card)))

(repeat (config "/Game/Poker/CardsPerPlayer")

(for ?player in ?players

(so {?card (pop ?cards)}

(enq ?player :Cards ?card)

(put ?card :Dealt true)))

)

dealt

)

.:  deal

```

```

> (enumeration Hands

Nothing

OnePair

TwoPairs

ThreeOfAKind

Straight

Flush

FullHouse

FourOfAKind

StraightFlush

)

.:  Enumeration-3

> (function analyze

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Suit as ?s :Rank as ?r\]

(let ?n (position Ranks ?r))

\[Card ^ as ?c2 (contains ?cards ?c2) :Suit = ?s :Rank = (@ Rank (+ ?n 1))\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Suit = ?s :Rank = (@ Rank (+ ?n 2))\]

\[Card ^ as ?c4 (contains ?cards ?c4) :Suit = ?s :Rank = (@ Rank (+ ?n 3))\]

\[Card ^ as ?c5 (contains ?cards ?c5) :Suit = ?s :Rank = (@ Rank (+ ?n 4))\]

(/= ?c1 ?c2 ?c3 ?c4 ?c5)

do

(put ?p :Hand StraightFlush))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Rank = ?r\]

\[Card ^ as ?c2 (contains ?cards ?c2) :Rank = ?r\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Rank = ?r\]

\[Card ^ as ?c4 (contains ?cards ?c4) :Rank = ?r\]

(/= ?c1 ?c2 ?c3 ?c4)

do

(put ?p :Hand FourOfAKind))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Rank as ?m\]

\[Card ^ as ?c2 (contains ?cards ?c2) :Rank = ?m\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Rank = ?m\]

\[Card ^ as ?c4 (contains ?cards ?c4) :Rank as ?n (/= ?m ?n)\]

\[Card ^ as ?c5 (contains ?cards ?c5) :Rank = ?n\]

(/= ?c1 ?c2 ?c3 ?c4 ?c5)

do

(put ?p :Hand FullHouse))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Suit as ?s\]

\[Card ^ as ?c2 (contains ?cards ?c2) :Suit = ?s\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Suit = ?s\]

\[Card ^ as ?c4 (contains ?cards ?c4) :Suit = ?s\]

\[Card ^ as ?c5 (contains ?cards ?c5) :Suit = ?s\]

(/= ?c1 ?c2 ?c3 ?c4 ?c5)

do

(put ?p :Hand Flush))

(with \[Player ^ as ?p Cards ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Rank as ?r\]

(let ?n (position Ranks ?r))

\[Card ^ as ?c2 (contains ?cards ?c2) :Rank = (@ Ranks (+ ?n 1))\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Rank = (@ Ranks (+ ?n 2))\]

\[Card ^ as ?c4 (contains ?cards ?c4) :Rank = (@ Ranks (+ ?n 3))\]

\[Card ^ as ?c5 (contains ?cards ?c5) :Rank = (@ Ranks (+ ?n 4))\]

(/= ?c1 ?c2 ?c3 ?c4 ?c5)

do

(put ?p :Hand Straight))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Rank as ?n\]

\[Card ^ as ?c2 (contains ?cards ?c2) :Rank = ?n\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Rank = ?n\]

(/= ?c1 ?c2 ?c3)

do

(put ?p :Hand ThreeOfAKind))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Rank as ?m\]

\[Card ^ as ?c2 (contains ?cards ?c2) :Rank = ?m\]

\[Card ^ as ?c3 (contains ?cards ?c3) :Rank as ?n (/= ?m ?n))\]

\[Card ^ as ?c4 (contains ?cards ?c4) :Rank = ?n\]

(/= ?c1 ?c2 ?c3 ?c4)

do

(put ?p :Hand TwoPairs))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

\[Card ^ as ?c1 (contains ?cards ?c1) :Rank as ?m\]

\[Card ^ as ?c2 (contains ?cards ?c2) :Rank = ?m\]

(/= ?c1 ?c2)

do

(put ?p :Hand OnePair))

(with \[Player ^ as ?p :Cards as ?cards :Hand = Unknown\]

do

(put ?p :Hand Nothing))

ready

)

.:  analyze

> (do (setup) (deal) (analyze))

.:  ready

```

## OPS5 Comparison

The OPS5 programming language was developed by Charles Forgy in the late 1970s. OPS is an acronym for "Official Production System" and it is a rule based programming language primarily used for expert system development. The following is an OPS5 program that implements a model of cars.

### OPS5

```

(literalize car

age ; new or old

condition ; good or junk

)

(p old-not-junk

(car ^age old ^condition <> good)

\--->

(write (crlf) that is believable))

(p good-not-old

(car ^age <> old ^condition good)

\--->

(write (crlf) that is possible))

(p new-and-junk

(car ^age new ^condition junk)

\--->

(write (crlf) There are no new, junk cars))

(copy car ^age new ^condition good)

```

### Premise

```

(relation Car

:Age ; new or old

:Condition ; good or junk

)

(rule old-not-junk

when \[Car :Age = old :Condition /= good\]

do (tell user ($ that is believable \\n)))

(rule good-not-old

when \[Car :Age /= old :Condition = good\]

do (tell user ($ that is possible \\n)))

(rule new-and-junk

when \[Car :Age = new :Condition = junk\]

do (tell user ($ There are no new, junk cars \\n)))

(new Car :Age new :Condition good)

```

## CLIPS Comparison

The C Language Integrated Production System, CLIPS, was developed in 1985 by NASA and was based on Charles Forgy's OPS languages and the Automated Reasoning Tool language from Inference Corporation. The example below is derived from <https://en.wikipedia.org/wiki/CLIPS>.

### CLIPS

```

(deftemplate problem

(slot name)

(slot status))

(defrule rule1

(problem (name ignition_key) (status on))

(problem (name engine) (status wont_start))

(problem (name headlights) (status don’t_work))

\=>

(confirm (problem (name battery) (status faulty))))

(deffacts trouble_shooting

(problem (name ignition_key) (status on))

(problem (name engine) (status wont_start))

(problem (name headlights) (status don’t_work)))

```

### Premise

```

(relation Problem

:Name

:Status

)

(rule rule1

when \[Problem :Name = ignitionKey :Status = on\]

\[Problem :Name = engine :Status = WontStart\]

\[Problem :Name = headlights :Status = DontWork\]

do

(knew Problem :Name battery :Status faulty)

)

(function troubleshooting

(new Problem :Name ignitionKey :Status on)

(new Problem :Name engine :Status WontStart)

(new Problem :Name headlights :Status DontWork)

)

(troubleshooting)

```

## SQL Comparison

Structured Query Language (SQL) is a language for programming relational database management systems (RDMS). SQL was first described by Edgar F. Codd in 1970.

### Relationships

In Structured Quey Language, entities and the relationships among them are central to the languge. Entities (and relationships) are defined by Tables which have Columns.

#### SQL

```

CREATE TABLE Region (

RegionID INTEGER NOT NULL,

Name VARCHAR(50) NOT NULL

);

CREATE TABLE Country (

CountryID INTEGER NOT NULL,

Name VARCHAR(50) NOT NULL

);

CREATE TABLE Customer (

CustomerID INTEGER NOT NULL AUTO_INCREMENT,

RegionID INTEGER NOT NULL,

CountryID INTEGER NOT NULL,

);

CREATE TABLE Order (

OrderID INTEGER NOT NULL AUTO_INCREMENT,

CustomerID VARCHAR(10)

);

CREATE TABLE Category (

CategoryID INTEGER NOT NULL AUTO_INCREMENT,

CategoryName VARCHAR(100) NOT NULL,

Description MEDIUMTEXT

);

CREATE TABLE Product (

ProductID INTEGER NOT NULL AUTO_INCREMENT,

ProductName VARCHAR(100) NOT NULL,

CategoryID INTEGER,

UnitsInStock FLOAT,

UnitPrice FLOAT

Discontinued BIT

);

CREATE TABLE Employee (

EmployeeID INTEGER NOT NULL AUTO_INCREMENT,

EmployeeName VARCHAR(100) NOT NULL,

ReportsTo INTEGER,

Sold FLOAT

);

```

#### Premise

```

(relation Region

:Name

)

(relation Country

:Name

)

(relation Customer

:Region

:Country

)

(relation Order

:CustomerId

)

(relation Category

:CategoryId

:CategoryName

:Description

)

(relation Product

:ProductId

:ProductName

:CategoryId

:UnitsInStock

:UnitPrice

:Discontinued false

)

(relation Employee

:EmployeeId

:EmployeeName

:ReportsTo

:Sold

)

```

### Select All

A select all query retrieves all attributes of an entity.

#### SQL

```

SELECT \*

FROM Category

```

#### Premise

```

(with Category)

```

### Selecting a single column

In SQL a single column is selected by specifying the name of the column in a select query.

#### SQL

```

SELECT CategoryName

FROM Category

```

#### Premise

```

(with \[Category as ?c\]

list (:CategoryName ?c))

```

```

(with \[Category :CategoryName as ?n\]

list ?n)

```

### Selecting multiple columns

In SQL multiple columns are selected by naming each column in a select query.

#### SQL

```

SELECT CategoryName, Description

FROM Category

```

#### Premise

```

(with \[Category :CategoryName as ?n :Description as ?d\]

list {?n ?d})

```

### Selecting a calculated column

A calculated column is one in which a function is applied to one or more existing columns in a table.

#### SQL

```  
SELECT LENGTH(CategoryName)

FROM Category  
```

#### Premise

```

(with \[Category :CategoryName as ?n\]

list (# ?n))

```

### Selecting distinct values

#### SQL

```

SELECT DISTINCT LENGTH(CategoryName)

FROM Category

```

#### Premise

```

(distinct

(with \[Category :CategoryName as ?n\]

list (# ?n)))

```

### Selecting a scalar value

#### SQL

```  
SELECT MAX(LENGTH(CategoryName))

FROM Category  
```

#### Premise

```

(max (with \[Category :CategoryName as ?n\]

list (# ?n)))

```

### Filtering results by Equality

#### SQL

```

SELECT \*

FROM Product

WHERE UnitsInStock = 0

```

#### Premise

```

(which Product

:UnitsInStock = 0)

```

### Filtering results by Inequality

#### SQL

```

SELECT \*

FROM Product

WHERE NOT (UnitPrice > 10)

```

#### Premise

```

(which Product

:UnitPrice as ?p

(not (> ?p 10)))

```

```

(which Product

:UnitPrice <= 10 )

```

### Filtering results by a range

#### SQL

```

SELECT \*

FROM Product

WHERE UnitPrice BETWEEN 5 AND 9

```

#### Premise

```

(which Product

:UnitPrice as ?u

(<= 5 ?u 9))

```

### Multiple filter conditions

#### SQL

```

SELECT \*

FROM Product

WHERE Discontinued = 1

AND UnitsInStock <> 0

```

#### Premise

```

(which Product

:Discontinued 1

:UnitsInStock not 0)

```

### Order by value ascending

#### SQL

```

SELECT \*\`

FROM Product

ORDER BY UnitPrice

```

#### Premise

```

(which Product

sort :UnitPrice < )

```

### Order by value descending

#### SQL

```

SELECT \*

FROM Product

ORDER BY UnitPrice DESC

```

#### Premise

```

(which Product

sort :UnitPrice > )

```

### Limit number of results

#### SQL

```

SELECT TOP 5 \*

FROM Product

ORDER BY UnitPrice

```

#### Premise

```

(top (which Product

sort :UnitPrice < )

5)

```

### Paged results

#### SQL

```

WITH part1 AS (

SELECT \*

FROM Product

ORDER BY UnitPrice)

SELECT \*

FROM part1

WHERE RRN(part1) BETWEEN 5 AND 10

```

#### Premise

```

(mid (which Product

sort :UnitPrice < )

5

10)

```

### Group by value

#### SQL

```

SELECT TOP 100 UnitPrice

FROM (SELECT Product.UnitPrice,

COUNT(\*) AS Count

FROM Product

GROUP BY Product.UnitPrice)

ORDER BY Count DESC

```

#### Premise

```

(with (top (with \[Product as ?p :UnitPrice as ?u\]

list {:UnitPrice ?u

:Count (with \[Product :UnitPrice as ?u\] tally)}

sort :Count > )

100) each ?x

list (:UnitPrice ?x))

```

### Inner Join

#### SQL

```

SELECT p.\*

FROM Product p,

Category c

WHERE c.CategoryName = "Beverages" AND

c.CategoryID = p.CategoryID

```

#### Premise

```

(with

\[Product ^ as ?p :CategoryName = "Beverages" :CategoryId as ?id\]

\[Category :Categoryid = ?id\]

list (premise ?p))

```

### Left Join

#### SQL

```

SELECT c.CustomerID, COUNT(o.OrderID)

FROM Customer c

LEFT JOIN Order o

ON o.CustomerID = c.CustomerID

GROUP BY c.CustomerID

```

#### Premise

```

(with

\[Customer :CustomerId as ?i\]

list {:CustomerId ?i :Count (with \[Order :CustomerId = ?i\] tally)}

```

```

(with

\[Customer :CustomerId as ?i\]

\[Order :OrderId as ?j\]

(left ?i ?j)

group {?i (when (any ?i) 1 0)}

by 1 into ?group

list {:CustomerId (@ ?group 1)

:Count (summation ?pair in (rest ?g) (@ ?pair 2)) }

```

### Concatenate

#### SQL

```

SELECT customer.CompanyName

FROM Customer AS customer

WHERE customer.CompanyName LIKE "A%’

UNION ALL

SELECT customer.CompanyName

FROM Customer AS customer

WHERE customer.CompanyName LIKE "E%’

```

#### Premise

```

(union

(with \[Customer :CompanyName as ?n\] (like ?n "A%") list ?n)

(with \[Customer :CompanyName as ?n\] (like ?n "E%") list ?n))

```

### Create, Update and Delete

#### SQL

```

INSERT INTO Category (CategoryName, Description)

VALUES ("Merchandising", "Cool products");

INSERT INTO Product (ProductName, CategoryID)

SELECT TOP (1) "Red Jacket", CategoryID

FROM Category

WHERE CategoryName = "Merchandising";

UPDATE Product

SET Product.ProductName = "Green Jacket"

WHERE Product.ProductName = "Red Jacket";

DELETE FROM Product

WHERE Product.ProductName = "Green Jacket";

DELETE FROM Category

WHERE Category.CategoryName = "Merchandising";

```

#### Premise

```

(new Category :CategoryName "Merchandising"

:Description "Cool Products")

(new Product :ProductName "Red Jacket"

:CategoryId (each Category ^ as ?c

:CategoryName "Merchandising"

give (:CategoryId ?c)))

(with \[Product ^ as ?p :ProductName = "Red Jacket"\]

do (put ?p :ProductName "Green Jacket"))

(with \[Product ^ as ?p :ProductName = "Green Jacket"\]

do (old ?p))

(with \[Category ^ as ?c :CategoryName = "Merchandising"\]

do (old ?c))

```

### Recursive Query

#### SQL

```

WITH EmployeeHierarchy (EmployeeID,

LastName,

FirstName,

ReportsTo,

HierarchyLevel) AS

( SELECT EmployeeID

, LastName

, FirstName

, ReportsTo

, 1 as HierarchyLevel

FROM Employees

WHERE ReportsTo IS NULL

UNION ALL

SELECT e.EmployeeID

, e.LastName

, e.FirstName

, e.ReportsTo

, eh.HierarchyLevel + 1 AS HierarchyLevel

FROM Employees e

INNER JOIN EmployeeHierarchy eh

ON e.ReportsTo = eh.EmployeeID

) SELECT \*

FROM EmployeeHierarchy

ORDER BY HierarchyLevel, LastName, FirstName

```

#### Premise

```

(relation EmployeeHierarchy

:EmployeeId :LastName :FirstName :ReportsTo :HierarchyLevel )

(with (union

(with \[Employee ^ as ?e :ReportsTo is nothing :EmployeeId as ?i

:LastName as ?n :FirstName as ?f\]

list (knew EmployeeHierarchy :EmployeeId ?i :LastName ?n

:FirstName ?f :HierarchyLevel 1))

(with

\[EmployeeHierarchy ^ as ?eh :EmployeeId as ?i :HierarchyLevel as ?h\]

\[Employee ^ as ?e :EmployeeId as ?j :LastName as ?n :FirstName as ?f

:ReportsTo ?i\]

list (knew EmployeeHierarchy :EmployeeId ?j :LastName ?n

:FirstName ?f :HierarchyLevel (+ ?h 1))))

as ?result

list (premise ?result)

sort :HierarchyLevel < :LastName < :FirstName < )

```

# 6\. Foundation Modules

The SubThought Premise is divided into several modules which contain built-in (i.e., intrinsic) functions. Each module has a particular area of responsibility. For example, the IO module facilitates communication while the knowledge base module (KB) declares storage and reasoning functions.

### Apex

This module contains the global environment.

### Base

This module provides control structures and special forms.

### IO

This module contains messaging, file, and the console functions.

### KB

This module provides access functions to knowledge bases.

### Math

This module provides arithmetic, trigonometric, and statistical functions.

### Tasks

This module has functions that manage asynchronous and concurrent tasks.

### User

This module contains the default environment.

# 7\. Quick Reference

A synopsis of each function follows.

| 1   | (\-- _number_ ) | Decrements a number by 1. |
| --- | --- | --- |
| 2   | (\- _number_ … ) | Subtraction. |
| 3   | (@ _container place_ _…_ ) | Retrieves elements from a sequence or assortment. |
| 4   | (\# _container_) | Returns the number of elements. |
| 5   | ($ _value_ _…_ ) | Creates a new string with intervening spaces . |
| 6   | ($$ _value_ _…_ ) | Creates a new string by eliding arguments. |
| 7   | (% _command arguments_ ) | Performs an operating system command |
| 8   | (& _value_ _…_ ) | Merges arguments into a new sequence. |
| 9   | (&& _value_ _…_ ) | Merges arguments into a new sequences and removes nils. |
| 10  | (\* _number number_ _…_ ) | Mulitplication. |
| 11  | (** _base exponent_) | Exponentiation. |
| 12  | (/ _dividend divisor_ _…_ ) | Division. |
| 13  | (// _number degree_) | _N_th Root. |
| 14  | (/~ _value<sub>1</sub> value<sub>2</sub>_) | Calculates the dissimilarity between two values. |
| 15  | (/= _value<sub>1</sub> value<sub>2</sub>_ _…_ ) | Returns true if any values are not equal. |
| 16  | (~ _value<sub>1</sub> value<sub>2</sub>_) | Calculates the similarity between two values. |
| 17  | ( ' _variant_ ) | Quotes a variant. |
| 18  | ( \` _variant_ ) | Expands a variant by substituting values. |
| 19  | (+ _number_ _number_ . . . ) | Addition. |
| 20  | (++ _number_ ) | Increments a number by 1. |
| 21  | (<-- _function symbol value …_ ) | The value before tying a symbol to a new value. |
| 22  | (< _value_ _value_ … ) | True if each value is less than the next. |
| 23  | (<= _value_ _value_ _…_ ) | True if each value is less or equal to the next. |
| 24  | (<== _container function place value_ _…_ ) | The value before replacement. |
| 25  | (\= _value_ _value_ _…_ ) | True if each value is equal to the next. |
| 26  | (\==> _container function place value_ _…_ ) | The value after replacement. |
| 27  | (> _value_ _value_ _…_ ) | True if each value is greater than the next. |
| 28  | (\--> _function symbol value_ … ) | The value after tying a symbol to a new value. |
| 29  | (>= _value_ _value_ _…_ ) | True if each value is greater or equal to the next. |
| 30  | (\\n _quantity_) | Returns a string containing one or more new lines. |
| 31  | (\\s _quantity_) | Returns a string containing one or more spaces. |
| 32  | (^ _thought_) | Returns a SubThought identifier. |
| 33  | (abolish _variables environment_ ) | Deletes variables from an environment. |
| 34  | (abort _tasks_ ) | Forcibly terminates one or more tasks |
| 35  | (about) | Provides system and version information. |
| 36  | (abs _number_) | Calculates the absolute value. |
| 37  | (absent _url_ ) | True if a file, folder, or ur does notl exist. |
| 38  | (acosecant number geometry metrum) | Calculates the inverse cosecant. |
| 39  | (acosine number geometry metrum) | Calculates the inverse cosine. |
| 40  | (acotangent number geometry metrum) | Calculates the inverse cotangent. |
| 41  | (actual _symbol_) | Returns the underlying symbol for a reference. |
| 42  | (add _assortment entry_ _…_ ) | Modifies an assortment by adding entries. |
| 43  | (address _url_) | Returns the address of a URL web resource. |
| 44  | (agent _job url_ _handler delay_) | Creates an agent. |
| 45  | (align _sequence_ _ordering_) | Returns a sorted list using the provided ordering. |
| 46  | (alike _value_ _value_ _…_ ) | True if each value has the same taxon. |
| 47  | (all _condition_ _…_ ) | True if all relevant knowledge satisfies all of the conditions. |
| 48  | (alphabetic-p _value_) | True if the first position of a string is alphabetic. |
| 49  | (alphanumeric-p _value_) | True if the first position of a string is whitespace. |
| 50  | (and _truth_ _truth_ _…_ ) | Logical conjunction. |
| 51  | (any _condition_ _…_ ) | True if some relevant knowledge satisfies all of the conditions. |
| 52  | (append _sequence value_ _…_ ) | Inserts values at the end of a sequence. |
| 53  | (apply _function arguments environment_) | Applies a function to a list of arguments. |
| 54  | (arity _function kind_) | Returns the number of variables in a function's parameter list. |
| 55  | (array _dimensions option_) | Returns a multi dimensional list. |
| 56  | (asecant number geometry metrum) | Calculates the inverse secant. |
| 57  | (asine number geometry metrum) | Calculates the inverse sine. |
| 58  | (ask _who message timeout default_ ) | Sends a message to a recipient and awaits a response. |
| 59  | (atangent number geometry metrum) | Calculates the inverse tangent. |
| 60  | (attach _knowledge_ ) | Registers a knowledge base. |
| 61  | (average _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ ) | The arithmetic mean of a sequence. |
| 62  | (avg _value_ _…_) | The arithmetic mean. |
| 63  | (await _task timeout_ _default_) | Returns the result of a task. |
| 64  | (before-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_) | True if an interval finishes before a second interval. |
| 65  | (beginning _interval_) | Returns the beginning instant of an interval |
| 66  | (best _probe candidates option_ _..._ ) | Returns the best matching candidates. |
| 67  | (beyond _sequence position_ ) | True if a position is outside a sequence. |
| 68  | (big _value_ ) | Converts a value to a big number. |
| 69  | (bind _container assignment_ … ) | Assigns variables to values in sequences or assortments. |
| 70  | (bion _name work_ ) | Returns a resource that hosts a cluster of cells for doing tasks. |
| 71  | (bindings _pattern_ ) | Returns a list of symbol value pairs for an environment or premise. |
| 72  | (bitwise _number op_ … ) | Performs bitwise operations. |
| 73  | (bound _function_) | Returns the variables that are bound in a function. |
| 74  | (bound-p _symbol_) | True if a symbol has a value. |
| 75  | (bracket _truth_) | Returns 1 if a truth expression is true, 0 otherwise. |
| 76  | (break _value_) | Terminates a loop. |
| 77  | (busy-p _task_) | True if a task has not completed. |
| 78  | (but _sequence quantity_) | Creates a subsequence of all except the last elements. |
| 79  | (bye) | Terminates the interpreter. |
| 80  | (call _value_ _…_ ) | Creates an unevaluated call. |
| 81  | (can _expression result error_ ) | Evaluates an expression while suppressing failures. |
| 82  | (cancel _tasks_ _option_ _…_ ) | Cooperatively cancels tasks. |
| 83  | (cancelled-p _task_) | True if a task has been cancelled. |
| 84  | (canonify _variant_ ) | Makes equal values identical. |
| 85  | (capitalize _string option_) | Capitalizes a string. |
| 86  | (case _probe clause_ _…_ _else-clause_) | Branches execution based on a value. |
| 87  | (categorize _sequence predicate_ _…_) | Creates a list of equivalence sets. |
| 88  | (cede _reference_ ) | Transfers a value between variables. |
| 89  | (ceiling _number_) | Rounds a number towards positive infinity. |
| 90  | (cell _bion work_ ) | Returns a resource that hosts tasks. |
| 91  | (char _unicode_) | Converts a Unicode value into a one position string. |
| 92  | (choose _sequence selector transform_) | Returns the arguments satisfying a function. |
| 93  | (clear _container_) | Eliminates all entries from an assortment or sequence. |
| 94  | (clip _value minimum maximum_) | Returns a value within a clipped range. |
| 95  | (clone _atom modification_ _…_ ) | Clones an atom with possible modifications. |
| 96  | (close _url_) | Closes a file or data url. |
| 97  | (closure _scope type name params expression_ _…_) | Creates a function or macro with a defined environment. |
| 98  | (coalesce _symbol_ _…_ _gate_ _expression_ _…_ ) | Returns a merged sequence. |
| 99  | (collect _symbol_ _…_ _gate_ _expression_ _…_ ) | Returns a transformed sequence. |
| 100 | (collection _element_ _…_ ) | Returns an unorderd collection of elements. |
| 101 | (combine _assortment entry_ _…_ ) | Creates a new assortment by combining entries. |
| 102 | (common _sequences_) | Creates a sequence of common elements among subsequences. |
| 103 | (comparable-p _value<sub>1</sub> value<sub>2</sub>_ ) | Returns true if the values can be compared. |
| 104 | (compare _value<sub>1</sub> value<sub>2</sub>_) | Returns &lt; (less), = (equal), or &gt; (greater). |
| 105 | (complete _expression_ _…_ ) | Runs expressions concurrently until completion. |
| 106 | (complex _real imaginary_) | Converts a value to a complex number. |
| 107 | (compose _functions arguments_) | Applies functions in reverse order using the arguments. |
| 108 | (conceive _knowledge_ ) | Creates a knowledge base. |
| 109 | (concurrent _expression_ _…_ ) | Evaluates expressions asynchronously. |
| 110 | (configuration _url association_ _..._ ) | Creates a configuration file. |
| 111 | (confirm _condition_ since _reason_ ) | Tests that a condition is true. |
| 112 | (confute _condition_ since _reason_ ) | Tests that a condition is false. |
| 113 | (connect _data_ ) | Connects to a data resource. |
| 114 | (constant _assignment_ _…_ ) | Creates a constant. |
| 115 | (contains _assortment value_ ) | True if a value is present in an assortment. |
| 116 | (continue _result_) | Continues to the next iteration of a loop. |
| 117 | (convertible-p _value taxon_) | True if the value can be converted to the taxon. |
| 118 | (copy _sequence count_ ) | Copies a sequence. |
| 119 | (copyright) | Displays copyright information. |
| 120 | (correlate _list<sub>1</sub> list<sub>2</sub>_) | Finds the correlation coefficient of two lists. |
| 121 | (cosecant number geometry metrum) | Calculates the cosecant. |
| 122 | (cosine number geometry metrum) | Calculates the cosine. |
| 123 | (cotangent number geometry metrum) | Calculates the cotangent. |
| 124 | (count _symbol_ _…_ _binding_ _sequence_ as _counter expression_ … ) | Counts the iterations and returns the last expression. |
| 125 | (critical _locks option_ _…_ _expression_ _…_) | Serializes evaluations across regions of code. |
| 126 | (cut _assortment key_ _…_ ) | Removes elements from assortments by key. |
| 127 | (data _option_ _…_ ) | Creates a data url. |
| 128 | (date _yr mth day hrs mins secs zone zmins_) | Creates a new date or returns the current date. |
| 129 | (declared-p _symbol environment_) | True if a symbol exists in an environment. |
| 130 | (decode _source format_) | Decodes a string. |
| 131 | (default _value_ _…_ ) | Returns the first non-nil value. |
| 132 | (definitions _environment_ ) | Retrieves literal value pairs in an environment. |
| 133 | (defunct _function_) | Undefines a function in a module. |
| 134 | (degrees _radians_) | Converts radians into degrees. |
| 135 | (delete _sequence value_ _…_ ) | Modifies sequence by deleting values. |
| 136 | (dependencies _module_) | Returns a module's dependencies. |
| 137 | (deq _container place option_) | Removes an element from an embedded sequence. |
| 138 | (describe _literal_) | Returns descriptions of a literal. |
| 139 | (detach _knowledge_ ) | Unregisters a knowledge base. |
| 140 | (difference _sequence<sub>1</sub> sequence<sub>2</sub> operation_) | Returns the difference of two sequences. |
| 141 | (did _expression_ ) | Evaluates an expression and surpresses failures. |
| 142 | (digit _number position_) | Returns the digit in the specified position of a number. |
| 143 | (digit-p _value_) | True if the first position of a string is a digit. |
| 144 | (digits _number_) | Returns the digits comprising a number. |
| 145 | (dimensions _sequence_) | Returns the lengths of each dimension in a sequence. |
| 146 | (discard _module_) | Discards a module. |
| 147 | (disjoint-p _sequence_ _sequence_ _…_ ) | True if no elements are common among sequences. |
| 148 | (distinct _sequence_ ) | Creates a new sequence without duplicate elements. |
| 149 | (dstribute _sequence function result_) | Applies a function to a sequence in parallel. |
| 150 | (divide _dividend_ _divisor default_) | Performs safe division. |
| 151 | (divisible-p _dividend divisor_) | True if the divisor evenly divides the dividend. |
| 152 | (do _expression_ _…_ resume _tag resumption_ _…_ finally _cleanup_ _…_ ) | Evaluates expressions and handles escapes. |
| 153 | (done) | Terminates a generator. |
| 154 | (drop _index_) | Removes a relation index. |
| 155 | (duplicate _source target option_) | Duplicates a file or contents of a folder. |
| 156 | (during-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_) | True if an interval occurs within a second interval. |
| 157 | (dynamic _assignments expression_ _…_ ) | Creates a dynamic environment for variables. |
| 158 | (e) | Returns Euler's number, 2.718281828459045. |
| 159 | (each _symbol_ _…_ _binding reversal_ _sequence_ _…_ _premises_ _option_ _…_ _action_ ) | Combines for and with to iterate over sequences to match patterns against the knowledge base. |
| 160 | (encode _source format_) | Encodes a string. |
| 161 | (enq _container place entry_) | Inserts an element into an embedded sequence. |
| 162 | (ensure c_heck_ _…_ ) | Performs type checking. |
| 163 | (entries _assortment_ ) | Retrieves key value pairs for an assortment. |
| 164 | (enum _name_ ) | Retrieves enumerated assortment. |
| 165 | (enumeration _name element_ _…_ ) | Defines an enumerated assortment. |
| 166 | (enumerations) | Returns a list of all enumerations. |
| 167 | (environment _parent entry_ _…_ ) | Creates a new context for variables and functions. |
| 168 | (epoch _time_) | Returns a Unix epoch or the current epoch. |
| 169 | (eradicate _knowledge_ ) | Deletes a knowledge base. |
| 170 | (erase _file option_ _…_ ) | Deletes files or folders. |
| 171 | (escape _tag_ ) | Escapes a do special form |
| 172 | (eval _expression environment_ ) | Evaluates an expression. |
| 173 | (even-p _number_) | True if the number is even. |
| 174 | (every _symbol_ _…_ _binding_ _sequence expression_ … _test_) | True if a predicate is true for every element in a sequence. |
| 175 | (exactly _quantity_ of _sequence_ _clause_ within _margin_ ) | True if a number of elements satisfy a clause. |
| 176 | (exchange _sequence substitution_ _…_ ) | Creates a new sequence with values swapped. |
| 177 | (excludes _sequence element option_ _…_ ) | True if a sequence does not contain an element. |
| 178 | (exists-p _value_) | True if a value is a thing.. |
| 179 | (exit _value_) | Explicitly ends a task using a return value. |
| 180 | (exponential _number significand_) | Calculates the base ten exponent of a number. |
| 181 | (expression _value_ _…_ ) | Creates an expression. |
| 182 | (extend _module_ _expression_ _…_ ) | Adds new definitions to a module. |
| 183 | (facility _name parameters expression_ _…_ ) | Creates a private function in a module. |
| 184 | (few _symbol_ _…_ _binding_ _sequence expression_ … _test_) | True if a predicate is true for less than half the elements in a sequence. |
| 185 | (file _option_ _…_ ) | Opens or creates a file. |
| 186 | (files _option_ _…_) | Returns a list of file names. |
| 187 | (fill _symbol_ from _start_ to _end_ by _increment_ with _expression_) | Fills a list with the result of an expression. |
| 188 | (filter _sequence predicate_ ) | Returns a sequence of elements that satisfy a predicate. |
| 189 | (find _features candidates option_ _..._ ) | Returns the best matching candidates. |
| 190 | (finishes-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_) | True if two intervals finish together. |
| 191 | (finishing _interval_) | Returns the finishing instant of an interval. |
| 192 | (fix _declaration_ _…_ ) | Adds variables to the current environment returns true. |
| 193 | (float _value_ ) | Converts a value to a floating number. |
| 194 | (floor _number_) | Rounds a number towards negative infinity. |
| 195 | (fold _symbol_ _…_ in _sequence_ into _expression_ _…_ ) | Tranforms a sequence into a value. |
| 196 | (folder _option_ _…_ ) | Creates or locates a folder in the file system. |
| 197 | (folders _option_ _…_ ) | Returns a list of sub folders. |
| 198 | (for _symbol_ _…_ _binding_ _reversal_ _sequence_ _…_ _expression_ _…_ ) | Iterates over the elements in a sequence. |
| 199 | (forever _expression_ _…_ ) | Repeatedly evaluates expressions. |
| 200 | (forgo _dependency module_) | Removes a dependent module. |
| 201 | (format _template value_ _…_ ) | Formats a string. |
| 202 | (fractional _number_) | Returns the fractional portion of a number. |
| 203 | (free _resources_ ) | Releases resources. |
| 204 | (full _first_ _second_ ) | True if values are equal or either value is nil. |
| 205 | (function _scope name params returning expression_ _…_ ) | Creates a public function in a module. |
| 206 | (functions _module_) | Returns a list of functions defined in a module. |
| 207 | (gather _symbol_ _…_ _binding_ _sequence expression_ … _test_) | Returns a sequence of elements that satisfy a predicate. |
| 208 | (generator _name parameters expression_ _…_ ) | Creates a series generator. |
| 209 | (get _container key_ … ) | Retrieves a value using one or more keys. |
| 210 | (given { _parameter_ _…_ } _expression_ _…_ ) | Creates an anonymous function. |
| 211 | (global _assignment_ _…_ ) | Creates global variables. |
| 212 | (go _function argument_ _…_ ) | Transfers control to a function. |
| 213 | (grok _what_) | Evaluates expressions in a url or file. |
| 214 | (group _list_ by _key_ _…_ into _symbol_ _expression_ _…_ ) | Combines sublists by position or key. |
| 215 | (halt _compute_ ) | Terminates a cell or bion. |
| 216 | (has _assortment key_ ) | True if a key is present in an assortment. |
| 217 | (hash _value option_ _…_ ) | Computes a hash code. |
| 219 | (help _function_) | Describes a function. |
| 220 | (hyperlink _option_ _…_ ) | Creates a hyperlink. |
| 221 | (id _resource_ ) | Returns a resource number. |
| 223 | (identical-p _value_ _value_ _…_ ) | True if all values occupy the same memory location. |
| 224 | (identity _value_) | Returns the value itself. |
| 225 | (idle _duration_) | Pauses for a specified interval. |
| 226 | (if _condition_ _expression_ … _or-clause_ … _else-clause_) | Branched conditional evaluation. |
| 227 | (imaginary _value_) | Converts a value to an imaginary number. |
| 228 | (in _value container option_ _…_ ) | True if a value is in a sequence or assortment. |
| 229 | (includes _sequence element option_ _…_ ) | True if a value is in a sequence. |
| 230 | (index _relation slot_ _…_ ) | Creates an index on slots of a relation. |
| 231 | (indices _relation_ ) | Returns a list of indices for a relation. |
| 232 | (infix _sequence delimeter_) | Creates a new sequence with interposed delimeters. |
| 233 | (inside _value_ ) | Creates an expression from a sequence or assortment. |
| 234 | (insert _sequence position value_ _…_ ) | Creates a new sequence by nserting values. |
| 235 | (insort _sequence value option_ … ) | Inserts a value into a sorted sequence. |
| 236 | (instantiate _expression_ ) | Creates an expression with premises in place of thoughts. |
| 237 | (integer _value_ ) | Converts a value to an integer. |
| 238 | (interleave _sequence sequence_ _…_ ) | Merges arguments into a new sequence. |
| 239 | (intersection _sequence_ _sequence_ _…_ ) | Creates a sequence of common elements. |
| 240 | (intersects-p _sequence_ _sequence_ _…_ ) | True if any elements are common among sequences. |
| 241 | (interval _start finish_) | Creates a time interval. |
| 242 | (into _relation thoughts_) | Creates new thoughts based on existing thoughts. |
| 243 | (invoke _call environment_) | Invokes a call. |
| 244 | (is _value_ _predicate_) | True if the value is true or if the applied predicate returns true. |
| 245 | (junction _scope name params expression_ _…_ ) | Creates a public function where arguments are evaluaed in parallel. |
| 246 | (key _assortment value_ ) | Finds the key for a value in an assortment. |
| 247 | (keys _assortment_ ) | Creates a list of keys for an assortment. |
| 248 | (keywords) | Creates the list of Premise keywords. |
| 249 | (knew _relation_ _criterion_ _…_ ) | Finds or creates a thought. |
| 250 | (knowledge _option_ _…_ ) | Finds or creates a knowledge base. |
| 251 | (known _pattern_ _…_ _option_ _…_ ) | True if the patterns match. |
| 252 | (lacks _assortment key_ ) | True if a key is absent from an assortment. |
| 253 | (last _sequence count_) | Creates a subsequence of the last elements. |
| 254 | (left _first_ _second_ ) | True if values are equal or the second value is nil. |
| 255 | (let _assignment_ _..._ ) | Adds variables to the current environment returning true. |
| 256 | (lexemes _string_) | Creates an uppercase string with spaces between words. |
| 257 | (lexicon _association_ _…_ ) | Creates a lexicon. |
| 258 | (lexicons) | Creates a list of all lexicons. |
| 259 | (license) | Prints the software license. |
| 260 | (like _sequence pattern_) | Compares a pattern to a sequence. |
| 261 | (list _value_ _…_ ) | Creates a list. |
| 262 | (literal _value_) | Creates a literal. |
| 263 | (local _assignments expression_ _…_ ) | Creates a task level scope. |
| 264 | (location _symbol_) | Sets a symbol to the current location. |
| 265 | (log _number base_) | Logarithm. |
| 266 | (long _value_) | Converts a value to a long number. |
| 267 | (loop _expression_ _…_ _gate_ ) | Repeatedly evaluates expressions. |
| 268 | (lowercase _string_) | Converts a string to lower case. |
| 269 | (macro _name parameters expression_ _…_ ) | Creates a public macro in a module. |
| 270 | (macros _module_) | Creates a list of macros defined in a module. |
| 271 | (make _prototype_ _term_ _…_ ) | Creates a record by creating a relationship if it does not exist. |
| 272 | (map _sequence_ _..._ _function_) | Applies a function to elements across sequences. |
| 273 | (max _value_ _…_ ) | Finds the maximum element. |
| 274 | (maximum _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ ) | Finds the maximum element. |
| 275 | (may _expression_ ) | Evaluates an expression while surpressing failures. |
| 276 | (median _value_ _…_) | Finds the middle value of a sequence. |
| 277 | (meets-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_) | True if an interval finishes when a second interval starts. |
| 278 | (meron _value_) | Returns the meronomic prototype of a value. |
| 279 | (meron-p _value meron_) | True if the value is a meron or is of the specific meronomic type. |
| 280 | (meronomy _value_) | Returns the meronomic prototypes of a value. |
| 281 | (method _scope name params expression_ _…_ ) | Creates a public method in a prototype. |
| 282 | (mid _sequence start stop skip_ ) | Copies a subsequence of a sequence. |
| 283 | (min _value_ _…_ ) | Finds the minimum element. |
| 284 | (minimum _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ ) | Finds the minimum element. |
| 285 | (missing _assortment value_ ) | True if a value is absent from an assortment. |
| 286 | (mod _dividend_ _modulus_) | Finds the remainder after division. |
| 287 | (modular _module expression_ _…_ ) | Evaluates expressions in module's scope. |
| 288 | (module _name definition_ _…_ ) | Creates a module. |
| 289 | (modules) | Creates a list of known modules. |
| 290 | (moment _units secs mins hours days year_ ) | Creates a moment or returns the current moment. |
| 291 | (more-p _sequence_) | True if a container has more than zero elements. |
| 292 | (morph _arguments functions_) | Applies functions in succession using the arguments. |
| 293 | (most _symbol_ _…_ _binding_ _sequence expression_ … _test_) | True if the predicate is true for more than half of the elements in a sequence. |
| 294 | (move _source destination_) | Moves or renames one or more files. |
| 295 | (my) | Returns the current cell resource. |
| 296 | (nall _condition_ … ) | True if not all relevant knowledge satisfies all of the conditions. |
| 297 | (nand _truth truth_ … ) | Negated logical conjunction. |
| 298 | (negative-p _number_) | True if a number is negative. |
| 299 | (nevery _symbol_ _…_ _binding_ _sequence expression_ … _test_) | True if the predicate is false for any element in the sequence. |
| 300 | (new _prototype_ _term_ _…_ ) | Creates a record. |
| 301 | (next _series_) | Advances a series to the next element. |
| 302 | (ngrams _string_ _length_) | Creates a list of substrings. |
| 303 | (nil-p _value_) | True if a value is nil. |
| 304 | (nix _prototype_) | Deletes a prototype. |
| 305 | (no _condition_ _…_ ) | True if no relevant knowledge satisfies all of the conditions. |
| 306 | (none _symbol_ _…_ _binding_ _sequence expression_ … _test_) | True if the predicate is false for all sequence elements. |
| 307 | (nor _truth truth_ _…_ ) | Negated logical disjunction. |
| 308 | (not _value_ _predicate_) | True if a value is false, or if the applied predicate returns false. |
| 309 | (nothing) | Returns nothing. |
| 310 | (null-p _value_) | True if a value is nothing, nil, or void. |
| 311 | (odd-p _number_) | True if a number is odd. |
| 312 | (old _thought_) | Deletes a thought. |
| 313 | (omit _sequence value_ _…_ ) | Creates a new sequence with values removed. |
| 314 | (on _condition_ _true-case_ _false-case_ ) | Branched conditional evaluation. |
| 315 | (only _variables_ _expression_ _…_ ) | Creates a restricted scope. |
| 316 | (open _url_) | Opens a file or data url. |
| 317 | (or _truth truth_ _…_ ) | Logical disjunction. |
| 318 | (out _value sequence option_ _…_ ) | True if a value is absent from a sequence. |
| 319 | (overlaps-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_) | True if an interval finishes after a second interval starts. |
| 320 | (pad _sequence length value side_ ) | Creates a new padded sequence. |
| 321 | (partition _sequence pivot comparer_) | Creates a list of equivalence sets for a pivot element. |
| 322 | (path _folder separator file_) | Concatenates a folder and file name. |
| 323 | (pattern _expression_ _…_ ) | Creates a pattern containing the supplied expressions. |
| 324 | (perform _environment method instance_ _…_ ) | Invokes a method within an environment. |
| 325 | (pi) | Returns 3.141592653589793. |
| 326 | (pick _sequence quantity_) | Creates a list of randomly selected elements. |
| 327 | (pipe _option_ _…_ ) | Creates a pipe. |
| 328 | (pop _sequence position_ ) | Returns the element removed from a sequence. |
| 329 | (posit _module url_) | Writes module expressions to a url. |
| 330 | (position _sequence element option_ _…_ ) | Finds the position of an element or subsequence in a sequence. |
| 331 | (positions _sequence_) | Returns positions of an element in a sequence or position value pairs. |
| 332 | (positive-p _number_) | True if a number is greater than zero. |
| 333 | (premise _value_ ) | Creates a premise representation of a value. |
| 334 | (probability _events A operation B_) | Calculates the probability over a series. |
| 335 | (procedure _scope name params expression_ _…_ ) | Creates a public function that returns \\%Nothing within a module. |
| 336 | (proceed _location_ set _assignment_ _…_ ) | Transfers control to a location. |
| 337 | (product _symbol_ _…_ _binding_ _sequence_ _expression_ _…_) | Multiplies an expression over a range of values. |
| 338 | (punctuation-p _string_) | True if the first position of a string is punctuation. |
| 339 | (push _sequence value position_ ) | Modifies a sequence by inserting a value. |
| 340 | (put _container entry_ _…_ ) | Updates values in an assortment or sequence. |
| 341 | (qualified _module function_) | Prepends a module to a function name. |
| 342 | (qualifiers _identifier_) | Creates a list of modules associated with an identifier. |
| 343 | (quantify _sequence predicate option_ _…_ ) | Returns a quantifier for elements satisfying a test. |
| 344 | (quantity _symbol_ _…_ _binding_ _sequence expression_ … _test_) | Returns the number of elements satisfying a test. |
| 345 | (radians _degrees_) | Converts degrees to radians. |
| 346 | (radix _number base_ ) | Converts a number to a base. |
| 347 | (random _lower_ to _upper precision_) | Creates a random number. |
| 348 | (range _first_ to _last_ by _increment_) | Creates a list of numbers. |
| 349 | (rational _numerator denominator_) | Converts values to a rational number. |
| 350 | (read _file count bits_) | Creates a string or stream. |
| 351 | (ready-p _task_) | True if a task has completed. |
| 352 | (real _value_) | Converts a value to a real number. |
| 353 | (reasoning _toggle_) | Toggles asynchronous rule execution. |
| 354 | (reclaim) | Performs garbage collection. |
| 355 | (reduce _sequence function_) | Converts a sequence into a value. |
| 356 | (reference _symbol_) | Returns a reference to a symbol. |
| 357 | (relation _name_ _inclusion_ _…_ _definition_ _…_ ) | Creates a relation. |
| 358 | (relations) | Returns a list of defined relations. |
| 359 | (release _locks_) | Releases locks on critical sections. |
| 360 | (remove _assortment value_ _…_ ) | Creates a new assortment by removing values. |
| 361 | (repeat _count_ _expression_ _…_ ) | Loops a specified number of times. |
| 362 | (replace _container entries option_ ) | Modifies an assortment or sequence by with replacement values. |
| 363 | (require _module_ as _moniker_ from _url_ _…__options_ _…_) | Retrieves an absent module from a url. |
| 364 | (reset _series_) | Resets a series for reuse. |
| 365 | (resize _sequence length default_) | Modifies the length of a sequence. |
| 366 | (rest _sequence skip_) | Creates a subsequence of all except the first elements. |
| 367 | (retract _rules_) | Eliminates rules. |
| 368 | (return _value_ from _function_) | Terminates a function call. |
| 369 | (reverse _sequence_) | Creates a reversed sequence. |
| 370 | (right _first_ _second_ ) | True if values are equal or the first value is nil. |
| 371 | (rip _assortment_ _value_ _…_ ) | Removes elements from assortments by value. |
| 372 | (round _number_) | Rounds a number to the nearest integer. |
| 373 | (rule _name_ _properties_ when _premises option_ _…_ _action_ _…_ ) | Creates a rule. |
| 374 | (rules) | Creates a list of all rules. |
| 375 | (same _value_ _value_ _…_ ) | True if all values are equal or contain equal elements. |
| 376 | (scale _list scalar_ _…_ _function_) | Applies a function to a list of numbers and scalar values. |
| 377 | (scatter _arguments functions_) | Applies functions in parallel returning a list of results. |
| 378 | (scope _keyval_ _..._ ) | Finds an environment or gets the current environment. |
| 379 | (seal _prototype_) | Prohibits new records. |
| 380 | (secant number geometry metrum) | Calculates the secant of the number. |
| 381 | (seconds _seconds_) | Creates a seconds value or returns seconds since year zero. |
| 382 | (seek _file position_) | Repositions a file resource to a new read/write location. |
| 383 | (self) | Returns the currently executing task resource. |
| 384 | (separator _kind_) | Creates a separator string. |
| 385 | (series _iterable_) | Creates a series. |
| 386 | (service _url_ _handler_) | Creates and starts a web service. |
| 387 | (set _manner assignment_ _..._ ) | Assigns variables to values in tandem returning true. |
| 388 | (settings _url association_ _..._ ) | Creates a configuration file.. |
| 389 | (sever _assortment key_ _…_ ) | Creates a new assortment by removing keys. |
| 390 | (shuffle _sequence seed_) | Creates a reordered sequence. |
| 391 | (sigma _list_ ) | Calculates the sigma of a sequence. |
| 392 | (signal _condition_ ) | Signals a condition. |
| 393 | (significand _number kind_) | Calculates the modified significand as zero, or a number from 1 to 10. |
| 394 | (signum _number option_ _…_ ) | Returns the sign of a number as a number, sigil, or word. |
| 395 | (sine number geometry metrum) | Calculates the sine of a number. |
| 396 | (so _bindings_ _expression_ _…_ ) | Creates a scope with bindings. |
| 397 | (socket _option_ _…_ ) | Creates a TCP socket. |
| 398 | (some _symbol_ _…_ _binding_ _sequence expression_ … _test_) | True if the test is true for any element in the sequence. |
| 399 | (sort _sequence ordering option_ _…_ ) | Creates a sorted sequence. |
| 400 | (split _sequence delimiter_) | Creates a list of subsequences divided at a delimiter. |
| 401 | (starts-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_) | True if two intervals start together. |
| 402 | (statistics _numbers_ ) | Finds the mean, median, sigma, and count of a list of numbers. |
| 403 | (step _symbol_ from _i_ _limit_ _j_ by _k expression_ … ) | Loops a symbol over a numeric range to evaluate expressions. |
| 404 | (stream _streamable_ ) | Creates a stream. |
| 405 | (string _value_ _…_ ) | Converts a value to a string. |
| 406 | (structure _name_ _inclusion_ _…_ _definition_ _…_ ) | Creates a structure. |
| 407 | (structures) | Creates a list of all structures. |
| 408 | (sub _sequence entry_ _…_ ) | Replaces a subsequence within a sequence. |
| 409 | (subset-p _subset superset_ ) | True if all elements in a subset are in a superset. |
| 410 | (substitute _sequence entries_ ) | Modifies a sequence replacing subsequences. |
| 411 | (subsumes-p _superset subset_ _…_) | True if all elements in each subset are in the superset. |
| 412 | (sum _value_ _…_) | Calculates the arithmetic sum. |
| 413 | (summation _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ ) | Adds an expression over a set of values. |
| 414 | (supply _arguments function environment_) | Applies a function to an argument list. |
| 415 | (suppose _knowledge_ facts _facts_ action _goals_<br><br>by _strategies_ via _operators_ limit _quantity_<br><br>gate _condition_ within _timeframe_<br><br>before _timepoint_ options _options_) | Performs hypothetico-deductive reasoning from facts to goals. |
| 416 | (survey _format_ _relation slot_) | Creates a list of referents or referent-count pairs. |
| 417 | (swap _sequence substitution_ _…_) | Modifies a sequence by interchanging values. |
| 418 | (symbol _name_ ) | Creates a symbol. |
| 419 | (symbols _environment ancestors_ ) | Lists the symbols in an environment. |
| 420 | (take _readable count_) | Creates an expression from a readable sequence. |
| 421 | (takeable _readable desired_) | Calculates the number of expressions that can be read. |
| 422 | (tally _pattern_ ) | Returns the number of matches in the knowledge base. |
| 423 | (tangent number geometry metrum) | Calculates the tangent. |
| 424 | (tarry _tasks expression_ _…_ ) | Allows tasks to complete on their own. |
| 425 | (task _scope_ _expression_ _…_ ) | Creates a list of tasks for deferred evaluation. |
| 426 | (tasks) | Creates a list of all tasks. |
| 427 | (taxon _value_) | Returns the datatype of a value. |
| 428 | (taxon-p _value taxon_) | True if the value is of the specific taxonomic type. |
| 429 | (taxonomy _value_) | Returns a list of datatypes for a value. |
| 430 | (tell _who message timeout_) | Sends a message to a recipient. |
| 431 | (there _url_ ) | True if a file, folder, or url exists. |
| 432 | (this _series_) | The current element of a series. |
| 433 | (thought _relation id_ ) | Finds an extant thought. |
| 434 | (thunk _expression_ _…_ ) | Creates a thunk in a module. |
| 435 | (thunks _module_) | Returns a list of thunks defined in a module. |
| 436 | (tick _nanoseconds_) | Creates a tick or returns nanoseconds since year zero. |
| 437 | (tie _manner_ _assignment_ _..._ ) | Assigns variables to values returning the last assigned value. |
| 438 | (time _unit operation time_ _…_ ) | Performs time operations. |
| 439 | (top _sequence count_) | Creates a subsequence of the first elements. |
| 440 | (transfer _source destination option_ _…_ ) | Transfers a value from one sequence to another. |
| 441 | (traverse _symbol binding sequence_ limit _dimensions expression_ _…_ ) | Loops through the coordinates of a sequence. |
| 442 | (trim _sequence_ _option_ _…_ ) | Creates a sequence without front and rear delimiters. |
| 443 | (truncate _number_) | Rounds a number towards zero. |
| 444 | (try _expression_ _…_ learn _symbol_ _recovery_ _…_ finally _cleanup_ _…_ ) | Evaluates expressions and handles signals. |
| 445 | (tuple _value_ _…_ ) | Creates a tuple. |
| 446 | (uid) | Creates a unique identifier. |
| 447 | (unbound _function_) | Creates a list of free variables for a function. |
| 448 | (unbound-p _symbol_) | True if a symbol is unbound. |
| 449 | (unicode _string_) | The Unicode of a string’s first position. |
| 450 | (union _sequence_ _sequence_ … ) | Concatenates sequences removing duplicates. |
| 451 | (union _sequence_ _sequence_ … ) | Concatenates sequences removing duplicates. |
| 452 | (unique _prefix_) | Creates a unique literal based on a prefix. |
| 453 | (unless _condition_ _false-case true-case_ ) | Branched conditional execution. |
| 454 | (unlike _sequence pattern_) | True if a pattern does not match a sequence. |
| 455 | (unqualified _function_) | The function literal without the module prefix. |
| 456 | (unseal _prototype_) | Permits new records for a protoytpe. |
| 457 | (unsigned _value_ ) | Converts a value to an unsigned number. |
| 458 | (until _condition_ _expression_ _…_ ) | Loops expressions until a condition is true. |
| 459 | (unwrap _module_) | Permits modifications to a module. |
| 460 | (uppercase _string_) | Converts a string to uppercase. |
| 461 | (uppercase-p _value_) | True if a string's first position is upper case. |
| 462 | (url _option_ _…_ ) | Creates a URL resource. |
| 463 | (use _knowledge expression_ _…_) | Evaluates expressions in a knowledge base scope. |
| 464 | (using _scope expression_ _…_) | Accesses a scope. |
| 465 | (values _assortment_) | Creates a list of values for an assortment. |
| 466 | (var _assignment_ _..._ ) | Adds variables to the current environment returning last value. |
| 467 | (vector _atom_ _…_ ) | Creates a vector of atoms. |
| 468 | (version) | Provides version information. |
| 469 | (void-p _sequence_) | True if a container has zero elements. |
| 470 | (wait _tasks timeout_ ) | Waits for tasks to end. |
| 471 | (which _pattern options_ _..._) | Creates a list of thoughts for a pattern. |
| 472 | (while _condition_ _expression_ _…_ ) | Loops expressions while a condition is true. |
| 473 | (whitespace-p _value_) | True if the first position of a string is whitespace. |
| 474 | (with _premises_ _option_ _…_ _action expression_ ) | Matches patterns against the knowledge base. |
| 475 | (within _sequence position_ ) | True if a position is inside a sequence. |
| 476 | (wrap _module_) | Prohibits modifications to a module. |
| 477 | (write _writeable value_ _…_ ) | Writes values to a writeable resource. |
| 478 | (xnor _truth truth_) | Logical equivalance. |
| 479 | (xor _truth truth_) | Logical exclusive disjunction. |
| 480 | (yield _value_) | Returns a result from a series generator. |
| 481 | (zap _container place_ _…_ ) | Updates associations and sequences with nil values. |
| 482 | (zero-p _number_) | True if a number is zero. |

Table . Function Quick Reference

# 8\. Function Reference

This chapter outlines each function in detail.

## \-- _decrement_

Decrements a number by 1.

##### Syntax

(\-- _number_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1   | A number or list to be decremented by 1. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The decremented number. |

##### Remarks

This function decrements the argument by 1. If an argument is a list, then each element of the list is decremented.

##### Example

```

> (-- 1)

.:  0

> (-- -1)

.:  -2

> (-- -1000+i)

.:  -1001+i

> (-- {5 -8 90 32})

.:  {4 -9 89 31}

```

##### Related

++ increment

## \- _subtraction_

Subtraction.

##### Syntax

(\- _number_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1+  | A number or list to be subtracted. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The difference of all supplied numbers as a number or a list of differences. |

##### Remarks

If there is one argument, the sign is reversed. If there are two or or more arguments, all arguments are subtracted from the first. If any of the arguments are unknown, infinity or ninfinity (i.e. negative infinity), the result shall respectively be unknown, infinity, or ninfinity. If an argument is a list, then each element of the list is subtracted. If a scalar and a list are subtracted, then the scalar is subtracted from each element of the list.

##### Example

```

> (- 1 2 3 4 5)

.:  -13

> (- 1)

.:  -1

> (- (- 1))

.:  1

> (- {3 4 5} 2 {1 0 2})

.:  {0 2 1}

```

##### Related

\+ addition, / division , \* multiplication

## @ _element_

Retrieves elements from a sequence or assortment.

##### Syntax

(@ _container place_ _…_ )

_place_ ::= _integer_

_place_ ::= #

_place_ ::= { _integer …_ }

_place_ ::= _key_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | A sequence, assortment, or record. |
| place | variant | 0+  | An integer position, the literal # for the last item, or a list of positions designating a coordinate, or an assortment key. |

##### Results

| Data Type | Description |
| --- | --- |
| expression | Returns the item(s) at the position(s). |

##### Remarks

For sequences, this function returns the element(s) at the one-based position in the sequence. If place is not specified, the first element is returned. If place is the literal #, then the last item is returned. If place is a number or list of numbers, the item at the place within the sublist is returned. If the sequence is empty, or if a coordinate or position does not exist, the function fails. For assortments, the place is a required parameter and must correspond to a key within the assortment, otherwise the function fails.

##### Example

```

> (@ "abcde")

.:  "a"

> (@ {{{a}{b}}{{c}{d}}} {1 2 1})

.:  b

> (@ (lexicon a 1 b 2 c 3) a c)

.:  1 3

```

##### Related

# _size_, add, append, cut, put, enq, deq, has, lacks

## # _size_

Returns the number of elements.

##### Syntax

(\# _container_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | A sequence, assortment or resource. |

##### Results

| Data Type | Description |
| --- | --- |
| integer | The number of elements. |

##### Remarks

Returns the number of elements in a sequence or assortment. If a file resource is provided, then it returns the file size in bytes.

##### Example

```

> (# {a b c d e})

.:  5

> (# "she sells sea shells")

.:  20

> (# (lexicon a b c d))

.:  2

> (# (environment (scope) ?a 1 ?b 2 ?c 3 ?d 7))

.:  4

> (# (entries (enumeration Colors red orange yellow)))

.:  3

> (# (file (path "." "/" "premise.out")))

.:  436

```

##### Related

@ _element_

## $ _concatenate_

Creates a new string with intervening spaces .

##### Syntax

($ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| string | The concatenated string. |

##### Remarks

Returns the concatenation of all values presented. All values are converted to strings, then concatenated. A space is preserved between each argument. Leading and trailing spaces are omitted. Any occurrence of the literal \\s is replaced with a space. Any occurrence of the literal \\n is replaced with a newline.

##### Example

```

> ($ the quick "brown" fox)

.:  "the quick brown fox"

> ($ "the quick" \\s "brown fox")

.:  "the quick brown fox"

> ($ {the quick} {} {brown fox})

.:  "{the quick} {} {brown fox}"

> ($ atom \\n molecule)

.:  "atom

molecule"

> ($)

.:  ""

```

##### Related

$$ _elide_, string

## $$ _elide_

Creates a new string by eliding arguments.

##### Syntax

($$ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| string | The concatenated string without spaces. |

##### Remarks

Returns the elision of all values presented. All values are converted to strings, then concatenated. Spaces are removed between arguments as are leading and traling spaces. Any occurrence of the literal \\s is replaced with a space. Any occurrence of the literal \\n is replaced with a newline.

##### Example

```

> ($$ the quick "brown" fox)

.:  "thequickbrownfox"

> ($$ the quick \\s \\s brown fox)

.:  "thequick brownfox"

> ($$ {the quick} {} {brown fox})

.:  "{the quick}{}{brown fox}"

> ($$ atom \\n molecule)

.:  "atom

molecule"

> ($$)

.:  ""

```

##### Related

$ _concatenate_, string

## % _shell_

Executes a shell command.

##### Syntax

(% _command_ _argument_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| command | literal | 1   | A shell command. |
| argument | Expression | 0+  | An argument to the command |

##### Results

| Data Type | Description |
| --- | --- |
| expression | The output of the command as a list of strings and an integer result. |

##### Remarks

Returns an expression containing a list of strings from the output of the command and an integer result.

##### Example

```

> (% pwd)

.:  {"/user/moi"} 0

> (% mkdir tmp)

.:  {} 0

> (% ls)

.:  {"tmp"} 0

> (% rmdir tmp)

.:  {} 0

```

##### Related

files, folders

## & _merge_

Merges arguments into a new sequence.

##### Syntax

(& _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The merged sequence. |

##### Remarks

Returns a flattened sequence merging all subsequences of the same type. If the first element is not a sequence, then a list is returned. The sequence type shall be that of the first element.

##### Example

```

> (& {1 2 3} 4 5 {6} {7} {8 9} 10)

.:  {1 2 3 4 5 6 7 8 9 10}

> (& \[1 2 3\] 4 5 \[6\] \[7\] \[8 9\] 10)

.:  \[1 2 3 4 5 6 7 8 9 10\]

> (& |1 2 3| |4 5| |6| |7| |8 9| |10|)

.:  |1 2 3 4 5 6 7 8 9 10|

> (& {the quick} {} \[brown fox\])

.:  {the quick brown fox}

> (& atom)

.:  {atom}

> (&)

.:  {}

```

##### Related

&& _abridge_, mid, insert, pop, push, swap, transfer

## && _abridge_

Merges arguments into a new sequences and removes nils.

##### Syntax

(&& _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The merged sequence without nils. |

##### Remarks

The && function returns a flattened sequence concatenating all values except nils.

##### Example

```

> (&& {} the quick brown fox {} nil nil jumped)

.:  {the quick brown fox jumped}

> (&& \[the quick\] nil \[\] nil \[brown \[fox\]\])

.:  \[the quick brown \[fox\]\]

> (&&)

.:  {}

> (&& nil nil nil)

.:  {}

```

##### Related

& _merge_, mid, insert, pop, push, swap, transfer

## \* _multiplication_

Multiply.

##### Syntax

(\* _number number_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 2+  | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The product of all factors or a list of products. |

##### Remarks

Returns the product of the arguments. If an argument is a list, then each element of the list is multiplied. If a scalar and a list are multiplied, then the scalar is multiplied with each element of the list. All lists must be of the same length.

##### Example

```

> (\* 1 2 3)

.:  6

> (\* {1 2 3} 5 {2 4 6})

.:  {10 40 90}

```

##### Related

/ division, % _modulo_, + addition, - subtraction, ** _exponent_

## ** _exponentiation_

Raises a base number to an exponent.

##### Syntax

(** _root exponent_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| root | variant | 1   | A number or list of numbers. |
| exponent | variant | 1   | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The root raised to the indicated power or list of the same. |

##### Remarks

If (** _root_ _exponent_ ) = _number_ , and (/ 1 _exponent_) = _degree_ then (// _number_ _degree_) = _root_. If no denominator is specified, this function returns the square root of the number..

##### Example

```

> (** 2 3)

.:  8

> (** (e) 2)

.:  7.3890461484

> (** {2 4 6} 2)

.:  {4 16 36}

> (** 2 {2 3 4})

.:  {4 8 16}

> (** {2 3 4} {2 3 4})

.:  {4 27 256}

> (** 4 0.5)

.:  2

```

##### Related

\* multiplication, / division, root

## / _division_

Division.

##### Syntax

(/ _dividend divisor_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number or list of numbers. |
| divisor | .aogalk | 0+  | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the quotient of the numbers or a list of quotients. |

##### Remarks

Returns the quotient of the values. If there is one value presented, this function returns the reciprocal of the value. If there are two values, it divides the first value by the second. If there are more than two values, it divides the result by each successive number. Division by zero shall result in the literal unknown being returned. All list arguments must be the same length. If an argument is a list, then each element of the list is divided. If a scalar and a list are divided, then the scalar is divided by each element of the list.

##### Example

```

> (/ 5.0 2)

.:  2.5

> {/ {4 5 6} 4.0)

.:  {1 1.25 1.5}

> (/ {4 5 6} {1.0 2.0 3.0})

.:  {4 2.5 2}

> (/ 5 0)

.:  undefined

```

##### Related

divide safe divide, \* multiplication, + addition, - subtraction, % modulo, // nth root

## // _nth root_

Returns the _n_th root of a number.

##### Syntax

(// _number_ _degree_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| degree | number | 0-1 | A number (Default is 2) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The root. |

##### Remarks

If (** _root_ _exponent_ ) = _number_ , and (/ 1 _exponent_) = _degree_ then (// _number_ _degree_) = _root_. If no denominator is specified, this function returns the square root of the number.

##### Example

```

(// 866020)

.:  930.6019557254326

(// 9)

.:  3

(// 8 3)

.:  2

(// 27 3)

.:  3

```

##### Related

** _exponentiation_, log

## /~ _dissimilarity_

Calculates the dissimilarity between two values.

##### Syntax

(/~ _value<sub>1</sub> value<sub>2</sub>_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | Any value |

##### Results

| Data Type | Description |
| --- | --- |
| real | The degree of dissimilarity between the two arguments. |

##### Remarks

Returns a number between 0 and 1, which identifies how dissimilar two numbers are.

Returns a number between 0 and 1. For numbers the following formula is used:

(- 1 (/ 1 (+ 1 (abs (- ?v1 ?v2)))))

If the values are of different types, they are treated as strings. For strings, lists of trigrams (ngrams of size 3) are generated and compared. For lists in general the following formula is used:

(- 1 (- (/ (# (intersection ?v1 ?v2)) (min (# ?v1) (# ?v2)))

(\* 0.1 (/ (# (difference ?v1 ?v2)) (min (# ?v1) (# ?v2))))))

If either list is empty, zero is returned.

##### Example

```

> (/~ {a b c} {a d e})

.:  0.73333333333333334

> (/~ "a b c" "a d e")

.:  0.21428571428571425

> (/~ 57 890)

.:  0.9988009592326139

```

##### Related

~ similarity, like, unlike, = equal, /= unequal

## /= _unequal_

Returns true if any values are not equal.

##### Syntax

(/= _value<sub>1</sub> value<sub>2</sub>_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if all values are not the same |

##### Remarks

Returns true if any values are not the same. Once two values are determined to be equal, the function short circuits and no further processing occurs.

For example (/= 1 2 3 5 3 6). Since 1≠2, we need to keep looking. Since 2≠3, we need to keep looking. Since 3≠5, we need to keep looking. Since 5≠3, we need to keep looking. However, since 3=3 (positions 3 and 5), false can be returned.

In the case of (/= (f ?x) (g ?x) (h ?x)), if f(?x) ≠ g(?x), h(?x) gets called. But, if f(x) = g(x), h(x) does not get called and false is returned.

##### Example

```

> (/= 1 2 3)

.:  true

> (/= 1 1 1)

.:  false

```

##### Related

\= _equal_, ~ _similarity_, /~ _dissimilarity_

## ~ similarity

Calculates the similarity between two values.

##### Syntax

(~ _value<sub>1</sub> value<sub>2</sub>_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | Any value |

##### Results

| Data Type | Description |
| --- | --- |
| float | A similarity measure between 0 and 1. |

##### Remarks

Returns a number between 0 and 1. For numbers the following formula is used:

(/ 1 (+ 1 (abs (- ?v1 ?v2))))

If the values are of different types, they are treated as strings. For strings, lists of trigrams (ngrams of size 3) are generated and compared. For lists in general the following formula is used:

(- (/ (# (intersection ?v1 ?v2)) (min (# ?v1) (# ?v2)))

(\* 0.1 (/ (# (difference ?v1 ?v2)) (min (# ?v1) (# ?v2)))))

If either list is empty, zero is returned.

##### Example

```

> (~ {a b c} {a d e})

.:  0.26666666666666666

> (~ "a b c" "a d e")

.:  0.21428571428571425

> (~ 57 890)

.:  0.001199040767386091

```

##### Related

/~ _dissimilarity_, = _equal_, /= _unequal_, like, unlike  

## ' _quote_

Quotes a variant.

##### Syntax

( ' _variant_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| variant | variant | 1   | A variant to be quoted |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The value after quoting. |

##### Remarks

The quote character signifies the quote function. All arguments are returned unevaluated.

##### Example

```

> (' foo)

.:  foo

> (' (+ 1 2 3))

.:  (+ 1 2 3)

> (' "a string")

.:  "a string"

> (' (foo))

.:  (foo)

> (' (+ 1 , (\* 2 3)))

.:  (+ 1 , (\* 2 3))

```

##### Related

\` _expand_, eval, function, macro, quote, unquote

## \` _expand_

Expands a variant by substituting values.

##### Syntax

( \` _variant_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| variant | variant | 1   | A variant to be expanded |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The argument after expansion. |

##### Remarks

The backquote character is the expand function. The argument is returned unevaluated unless it is preceded by or contains a comma (and underscore), in which case the value following the comma shall be evaluated in the present scope (or in which case the value following the underscore must evaluate to a list which shall be merged into the existing expression).

##### Example

```

> (\` (+ 1 2 "3"))

.:  (+ 1 2 "3")

> (so {?a 1 ?b 2 ?c {3 4 5}} (\` {, ?a , ?b , ?c}))

.:  {1 2 {3 4 5}}

> (so {?a 1 ?b 2 ?c {3 4 5}} (\` {, ?a , ?b ,_ ?c}))

.:  {1 2 3 4 5}

> (\` (foo))

.:  (foo)

> (\` (+ (+ 1 1) ,(\* 2 3)))

.:  (+ (+ 1 1) 6)

```

##### Related

' _quote_, eval, function, macro

## + _addition_

Addition.

##### Syntax

(+ _number_ _number_ . . . )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 2+  | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The sum or a list of sums. |

##### Remarks

Calculates the sum of the values. The values must all be numbers or lists containing numbers. If an argument is a list, then each element of the list is added. If a scalar and a list are added, then the scalar is added to each element of the list. All lists must be the same length.

##### Example

```

> (+ 1 2 3)

.:  6

> (+ 5 {6 7 8 9 10})

.:  {11 12 13 14 15}

> (+ {1 2 3} {4 5 6} 8)

.:  {13 15 17}

```

##### Related

\- minus, \* multiply, / divide

## ++ _increment_

Increments a number by 1.

##### Syntax

(++ _number_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1   | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The incremented number or list of numbers. |

##### Remarks

This function increments the argument by 1. If the argument is a list then each number in the list Is incremented by one.

##### Example

```

> (++ 1)

.:  2

> (++ 100)

.:  101

> (++ {99 -101 0})

.:  {100 -100 1}

```

##### Related

\-- decrement

## <-- _before tie_

The value before tying a symbol to a new value.

##### Syntax

(<-- _function symbol value …_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 1   | A function |
| symbol | symbol | 1   | A symbol |
| value | value | 0+  | A value used in the function call. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the value bound to the symbol before the function is applied. |

##### Remarks

None

##### Example

```

> (let ?n 0)

.:  true

> (<-- + ?n 7)

.:  0

> ?n

.:  7

```

##### Related

\--> _after tie_, assume, assign, global, local, put, set, swap, tie

## < _less_

True if each value is less than the next.

##### Syntax

(< _value_ _value_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if values are increasing. |

##### Remarks

Returns true if each value is less than its successor from left to right, and false otherwise. All values must be of the same type (either a literal, number, or string)

##### Example

```

(< a b c)

.:  true

(< "johnny" "ralph" "sam")

.:  true

(< 3 6 2 8)

.:  false

(< Amanda Samantha Zelda)

.:  true

```

##### Related

&lt;= less or equal, &gt; greater, >= greater or equal , = equal , /= unequal

## <= _less or equal_

True if each value is less or equal to the next.

##### Syntax

(<= _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if values are increasing. |

##### Remarks

Returns true if each value is less than its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings.

##### Example

```

> (<= a b b c)

.:  true

> (<= "johnny" "ralph" "sam")

.:  true

> (<= 3 6 2 8)

.:  false

```

##### Related

< _less_, > _greater_, >= _greater or equal_ , = _equal_ , /= _unequal_

## <== _before put_

The value before replacement.

##### Syntax

(<== _container function place value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment. |
| function | function | 1   | A function |
| place | variant | 1   | A key or position. |
| value | value | 0+  | a value used in the function call. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the new place value |

##### Remarks

None

##### Example

```

> (relation Q :X 0)

.:  Q

> (global ?Q (new Q))

.:  true

> (<== ?Q + :X 1)

.:  0

> (<== ?Q ++ :X)

.:  1

> (:X ?Q)

.:  2

```

##### Related

\==> _after put_

## \= _equal_

True if each value is equal to the next.

##### Syntax

(\= _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are the same |

##### Remarks

Returns true if each value is the same as its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equal if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical) or if their printed representation is the same (e.g., true and \\%True are equal since the printed representation of \\%True is true).

##### Example

```

> (= a a a a)

.:  true

> (= "johnny" "ralph" "sam")

.:  false

> (= 3 3)

.:  true

> (= 1 1/1 1.0)

.:  true

> (= true \\%True)

.:  true

```

##### Related

< _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal_, alike, identical

## \==> _after put_

The value after replacement.

##### Syntax

(\==> _container function place value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment. |
| function | function | 1   | A function |
| place | variant | 1   | A key or position. |
| value | value | 0+  | a value used in the function call. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the new place value |

##### Remarks

None

##### Example

```

> (relation Q :X 0)

.:  Q

> (global ?Q (new Q))

.:  true

> (==> ?Q + :X 1)

.:  1

> (==> ?Q ++ :X)

.:  2

> (:X ?Q)

.:  2

```

##### Related

<== _before put_

## > _greater_

True if each value is greater than the next.

##### Syntax

(> _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | value | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if values are decreasing. |

##### Remarks

Returns true if each value is greater than its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings.

##### Example

```

> (> c b a)

.:  true

> (> "johnny" "ralph" "sam")

.:  false

> (> 3 6 2 8)

.:  false

```

##### Related

< _less_ , <= _less or equal_, >= _greater or equal_ , = _equal_ , /= _unequal_

## \--> _after tie_

The value after tying a symbol to a new value.

##### Syntax

(\--> _function symbol value_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 1   | A function |
| symbol | symbol | 1   | A symbol |
| value | value | 0+  | A value used in the function call. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last value bound to the symbol. |

##### Remarks

None

##### Example

```

> (so {?length 0}

(for ?m in (modules)

(--> + ?length (# ?m))))

.:  23

> (# (reduce (modules) $))

.:  23

```

##### Related

<-- _before tie_, constant, dynamic, global, local, put, set, swap, tie, use

## >= _greater or equal_

True if each value is greater or equal to the next.

##### Syntax

(>= _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | value | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if values are increasing. |

##### Remarks

Returns true if each value is greater or equal to its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings.

##### Example

```

> (>= c b a)

.:  true

> (>= "johnny" "ralph" "sam")

.:  false

> (>= "sam" "ralph" "johnny")

.:  true

> (>= 8 7 6 3)

.:  true

```

##### Related

< _less_ , <= _less or equal_, > _greater_, = _equal_ , /= _unequal_

## \\n _newline_

Returns a string containing one or more new lines.

##### Syntax

(\\n _quantity_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| quantity | number | 0-1 | The number of new lines to create. Default is 1. |

##### Results

| Data Type | Description |
| --- | --- |
| string | A string containing a single new line character. |

##### Remarks

None.

##### Example

```

> (\\n)

.:  "

"

> (\\n 3)

.:  "

"

```

##### Related

$ _concatenate_, $$ _elide_, \\s _space_, string

## \\s _space_

Returns a string containing one or more spaces.

##### Syntax

(\\s _quantity_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| quantity | number | 0-1 | The number of spaces to create. Default is 1. |

##### Results

| Data Type | Description |
| --- | --- |
| string | A string containing a single space. |

##### Remarks

None.

##### Example

```

> (\\s)

.:  " "

> (\\s 15)

.:  " "

```

##### Related

$ _concatenate_, $$ _elide_, \\n _newline_, string

## ^ _thought id_

Returns a SubThought identifier.

##### Syntax

(^ _thought_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| thought | variant | 1   | A SubThought premise or SubThought identifier |

##### Results

| Data Type | Description |
| --- | --- |
| thought | Returns the SubThought identifier. |

##### Remarks

Returns the identifier for a thought.

##### Example

```

> (relation A :S1 0 :S2 1)

.:  A

> (new A)

.:  A_1

> (premise A_1)

.:  \[A ^ A_1 :S1 0 :S2 1\]

> (^ (premise A_1))

.:  A_1

> (^ A_1)

.:  A_1

> (^ FOO)

.:  nil

```

##### Related

id, instantiate, premise, type

## abolish

Deletes variables from an environment.

##### Syntax

(abolish _smybols environment_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| variables | variant | 1   | A symbol or a list of variables. |
| environment | environment | 0-1 | The environment containing the symbol(s). |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns the literal abolished. |

##### Remarks

Disassociates the symbol or variables from their respective values in the specified environment. If unspecified, each symbol is sought in the current scope or an ancestor environment, all the way up to the global environment. If the symbol is found, it is disassociated, then deleted. If the symbol is not found, it is ignored..

##### Example

```

> (var ?person DrWho)

.:  DrWho

> ?person

.:  DrWho

> (abolish ?person)

.:  abolished

> ?person

.:  \[Failure :Name UnboundSymbol :Text "The symbol ?person is unbound"\]

```

##### Related

<-- _before tie_, --> _after tie_, assign, assume, constant, dynamic, global, let, local, only , set, tie

## abort

Forcibly terminates one or more tasks.

##### Syntax

(abort _tasks_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| tasks | variant | 1   | A single task resource or a list of task resources. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the tasks or list of tasks. |

##### Remarks

Immediately terminates an executing task.

##### Example

```

> (concurrent (step ?i from 1 to 100000 (if (cancelled-p (self)) (break oops)) finished)

(step ?i from 1 to 100000 finished))

.:  {Task-57 Task-58}

> (cancel task-57)

.:  task-57

> (await task-57)

.:  oops

> (abort task-58)

.:  task-58

> (free {task-57 task-58})

.:  freed

```

##### Related

await, cancel, cancelled-p, complete, critical, do, done-p, reclaim , start, task, task-p, tasks

## about

Provides system and version information.

##### Syntax

(about)

##### Module

Base

##### Parameters

None

##### Results

None

##### Remarks

Returns system and version information.

##### Example

```

> (about)

.:  \[Premise :Version 1.1.0 :Build 20200430.001 :OS Win64 :Edition Community\]

```

##### Related

bye, eval, quote

## abs

Returns the absolute value.

##### Syntax

(abs _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1   | A number or a list. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | A non-negative number or a list of non-negative numbers. |

##### Remarks

Returns a non-negative number or a list of non-negative numbers. If the number is negative it is multiplied by -1. If the number is positive no change occurs.

##### Example

```

> (abs 100)

.:  100

> (abs -100)

.:  100

> (abs ninfinity)

.:  ninfinity

> (abs unkown)

.:  unknown

> (abs {0 -2 -99 24 56 infinity})

.:  {0 2 99 24 56 infinity}

```

##### Related

\- subtraction , + addition , % _modulo_, / _division_, \* _multiplication_

## absent

True if a file, folder, or url does not exist.

##### Syntax

(absent _url_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the url does not exist. |

##### Remarks

This function checks whether or not the url exists.

##### Example

```

> (let ?url (ul path "quick.txt"))

.:  true

> (if (absent ?url)

(let ?file (file url ?url seek 1 mode write erase yes))

(write ?file "The quick brown fox")

(close ?file))

.:  closed

```

##### Related

file, folder, there, url

## acosecant

Returns the inverse cosecant.

##### Syntax

(acosecant _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The inverse cosecant of the number. |

##### Remarks

##### Example

```

> (acosecant 0.3927)

.:  1.570796326-1.58686085i

> (acosecant 0.3927 cir radians)

.:  1.570796326-1.58686085i

> (acosecant 135 cir degrees)

.:  0.438313704

> (acosecant (pi) hyp radians)

.:  0.31316588045

> (acosecant 45 hyp degrees)

.:  1.06202877524

```

##### Related

cosine, tangent

## acosine

Returns the inverse cosine.

##### Syntax

(acosine _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The inverse cosine of the number. |

##### Remarks

None.

##### Example

```

> (acosine 1.570796326794)

.:  0+1.0322747855i

> (acosine cir 1.570796326794 radians)

.:  0+1.0322747855i

> (acosine cir 22.5 degrees)

.:  1.1672317198

> (acosine hyp 4.712388980384 radians)

.:  2.23188925305

> (acosine hyp 90 degrees)

.:  0.9136433572987  
```

##### Related

cosine, tangent

## acotangent

Returns the inverse cotangent.

##### Syntax

(acotangent _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The inverse cotangent of the number. |

##### Remarks

##### Example

```

> (acotangent 0.785398163397)

.:  0.905022576

> (acotangent cir 0.785398163397 radians)

.:  0.905022576

> (acotangent cir 180 degrees)

.:  0.3081690711

> (acotangent hyp 2.356194490192 radians)

.:  0.453062565662

> (acotangent hyp 120 degrees)

.:  0.519695325409

```

##### Related

cosine, tangent

## actual

Returns a the underlying symbol for a reference.

##### Syntax

(actual _reference_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| Reference | reference | 1   | A symbol reference |

##### Results

| Data Type | Description |
| --- | --- |
| symbol | Returns the symbol referenced. |

##### Remarks

The convention for denoting reference variables is to use two question marks: ??name.

##### Example

```

> (structure ListNode :Val :Next)

.:  ListNode

> (function IsPalindrome2 {ListNode ?tail reference ??head}

(ensure ListNode (actual ??head))

(if (null-p ?tail)

(return true)

or (and (IsPalindrome2 (:Next ?tail)) (= (:Val ?tail) (:Val ??head)))

(set ??head (:Next ??head))

(return true)

else (return false)))

.:  IsPalindrome2

> (function IsPalindrome {?head}

(ensure ListNode ?head)

(return (IsPalindrome2 ?head (reference ?head))))

.:  IsPalindrome

> (IsPalindrome  
(new ListNode :Val a :Next (new ListNode :Val b :Next (new ListNode :Val a))))

.:  true

```

##### Related

assume, dynamic, given, global, let, reference, scope, set, tie

## add

Modifies an assortment by adding entries.

##### Syntax

(add _assortment entry_ _…_ )

_entry ::=_ _key value_

_entry ::=_ _key_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment or sequence |
| entry | expression | 1+  | A key, or key value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The modified assortment. |

##### Remarks

Collections require only a key for each entry. Assortments require a key and value for each entry.

##### Example

```

> (entries (add (lexicon) a 1 b 2 c 3))

.:  {{a 1}{b 2}{c 3}}

> (entries (add (collection) 1 2 3 4 5))

.:  {{1 1}{2 2}{3 3}{4 4}{5 5}}

```

##### Related

\# _size_, cut, deq, enq, get, insert, key, keys, push, put, rip, values, zap

## address

Returns the address of a URL web resource.

##### Syntax

(address _url_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | URL | 1   | A url web resource. |

##### Results

| Data Type | Description |
| --- | --- |
| string | A valid URL in a string. |

##### Remarks

If no arguments are provided, then this function returns the universal resource locator for the SubThought Premise interpreter running on the current cell.

##### Example

```

> (address (url))

.:  "http://localhost"

> (address (url scheme https))

.:  "https://localhost"

> (url scheme https host "www.youtube.com" path "watch" query "v=ja76cnLKSL4")  
<br/>.: Url-3

> (address Url-3)

.:  "https://www.youtube.com/watch?v=ja76cnLKSL4"

```

##### Related

url, url-p

## agent

Creates an agent.

##### Syntax

(agent _job url_ _handler delay_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| job | function | 1   | A niladic function for the agent to repeatedly perform. |
| url | url | 1   | A Universal Resource Locator.. |
| handler | function | 1   | An message handler function. |
| delay | time | 0-1 | The delay between job executions. Default is 1 second. |

##### Results

| Data Type | Description |
| --- | --- |
| agent | The agent task. |

##### Remarks

This function creates an asynchronous agent task that repeatedly performs a job and also processes incoming messages. The message handler function should receive a sender url and a message string.

##### Example

```

> (let ?url (url scheme tcp port 5001))

.:  true

> (function reply {url ?sender string ?message} (tell ?sender "OK"))

.:  reply

> (function job {} (tell user ($ 1)))

.:  job

> (agent job ?url reply \\@s0.5)

.:  Agent-1

> (do (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1))

111111.: freed

```

##### Related

ask, cancel, service, pause, perform, start, tell

## align

Returns a sorted list using the provided ordering.

##### Syntax

(align _sequence_ _ordering_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence of unordered elements. |
| ordering | sequence | 1   | An ordered sequence. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | An ordered sequence. |

##### Remarks

Places items in the sequence in the specified ordering. If items in the sequence do not appear in the ordering, they are appended to the result in the order of appearance.

##### Example

```

> (align {b d c f} {a b c d})

.:  {b c d f}

> (align "72qaj8x" "zyx123a")

.:  "x2a7qj8"

```

##### Related

insort, sort

## alike

True if each value has the same taxon.

##### Syntax

(alike _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are the same |

##### Remarks

Returns true if each value has the same taxon as its successor from left to right, and false otherwise.

##### Example

```

> (alike a a a a)

.:  true

> (alike 1 1/1 1.0)

.:  false

> (alike "johnny" "ralph" "sam")

.:  true

> (alike true \\%True)

.:  false

> (alike 1 five "three")

.:  false

```

##### Related

< _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal_, identical

## all

True if all relevant knowledge satisfies all the premises.

##### Syntax

(all _premise_ _…_ )

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= as _symbol_

_binding_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _value_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| premise | variant | 1+  | A pattern, call, or truth value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are not nil. |

##### Remarks

True if all values are not nil, false otherwise. Evaluates values one at a time. If a vaue is nil then it returns immediately, ignoring remaining values. . If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.  

##### Example

```

> (all one two three)

.:  true

> (all a b nil)

.:  false

```

##### Related

any, no, nall

## alphabetic-p

True if the first position of a string is alphabetic.

##### Syntax

(alphabetic-p _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is a string and the first position is alphabetic. |

##### Remarks

Can be upper case or lower case.

##### Example

```

> (alphabetic-p {a b c})

.:  false

> (alphabetic-p "a b c")  


.:  true

> (alphabetic-p " a b c")

.:  false

> (alphabetic-p 450)

.:  false

> (alphabetic-p "450")

.:  false

> (alphabetic-p "Hello World.")

.:  true

```

##### Related

capitalized-p, letter-p, lowercase-p, uppercase-p

## alphanumeric-p

True if the first position of a string is a number or a letter.

##### Syntax

(alphanumeric-p _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is a string and the first position is alphanumeric. |

##### Remarks

True if the first position of the value is an upper or lower case alphabetic character or a digit.

##### Example

```

> (alphanumeric-p {a b c})

.:  false

> (alphanumeric-p "a b c")  


.:  true

> (alphanumeric-p " a b c")

.:  false

> (alphanumeric-p 450)

.:  false

> (alphanumeric-p "450")

.:  true

```

##### Related

capitalized-p, letter-p, lowercase-p, uppercase-p

## and

Logical conjunction.

##### Syntax

(and _truth_ _truth_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 2+  | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all arguments are true. |

##### Remarks

Evaluates the values presented one at a time. If any of the values is false, this function returns false immediately, ignoring any remaining values. This function fails if any argument is not truth.

##### Example

```

> (and (is 234 (given {?x} (= (taxon ?x) number)))

(is abc (given {?x} (= (taxon ?x) literal))))

.:  true

> (and true true true true false)

.:  false

```

##### Related

exists, nand, nil, nor, not, or, xor

## any

True if any relevant knowledge satisfies all the premises.

##### Syntax

(any _premise_ _…_ )

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= as _symbol_

_binding_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _value_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| premise | variant | 1+  | A pattern, call, or truth value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if any value is not nil. |

##### Remarks

True if any value is not nil. Returns immediately upon encountering the first non-nil value. If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.

##### Example

```

> (any nil nil apple)

.:  true

> (any one two three four)

.:  true

> (any nil nil)

.:  false

```

##### Related

all, default, is, nall, no

## append

Inserts values at the end of a sequence.

##### Syntax

(append _sequence value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| value | variant | 1+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The modified sequence. |

##### Remarks

Inserts the value into the end of a sequence.

##### Example

```

> (let ?s {})

.:  true

> (append ?s a b c)

.:  {a b c}

> (append ?s d e f)

.:  {a b c d e f}

> ?s

.:  {a b c d e f}

```

##### Related

@, add, fix, insert, pop, push, swap

## apply

Applies a function to a list of arguments.

##### Syntax

(apply _function arguments environment_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | The name of a function to invoke |
| arguments | list | 1   | A list containing actual parameters. |
| environment | environment | 0-1 | An optional environment. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The result from applying the function. |

##### Remarks

Applies the function to the list using the supplied environment, or the current scope if no environment is provided. The function is applied to the entire list and the result is returned.

##### Example

```

> (apply + {1 2 3})

.:  6

> (so { ?x 9

?s (scope) }

(so { ?x 3 }

(apply + {1 2 ?x} ?s)))

.:  12

```

##### Related

count, gather, invoke, map, morph, reduce, supply

## arity

Returns the number of variables in a function's parameter list.

##### Syntax

(arity _function kind_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function or function name . |
| kind | literal | 0-1 | One of required, optional, variadic, or all (default). |

##### Results

| Data Type | Description |
| --- | --- |
| integer | Returns the number of variables matching the parameter kind. |

##### Remarks

None

##### Example

```

> (function foo {?a + ?b ?c & ?d}

(tell user ($ (&& ?a ?b ?c ?d))))

.:  foo

> (arity foo)

.:  4

> (arity foo required)

.:  1

> (arity foo optional)

.:  2

> (arity foo variadic)

.:  1

```

##### Related

has, in, member, within

## array

Returns a multi dimensional list.

##### Syntax

(array _dimensions option_)

_dimensions_ ::= _size_

_dimensions_ ::= { _size_ _…_}

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| dimensions | variant | 1   | A number or list of numbers for each dimension |
| option | expression | 1   | A key value pair, either<br><br>of expression (default), or<br><br>each function. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list. |

##### Remarks

If option is of then all elements of the list are initialized to the same value. If option is each, during initialization, the function receives the current coordinate and the value is used for the position.

##### Example

```

> (array 5)

.:  {nil nil nil nil nil}

> (array 5 of 0)

.:  {0 0 0 0 0}

> (array 5 each (given {?x}(random 0 to 9))

.:  {7 5 8 2 4}

> (array {2 2} each (given {?coordinate}(reduce ?coordinate +)))

.:  {{2 3}{3 4}}

```

##### Related

@, bind, edit, make

## asecant

Returns the inverse secant.

##### Syntax

(asecant _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The inverse secant of the number. |

##### Remarks

##### Example

```

> (asecant 2.356194490192)

.:  1.13248262224

> (asecant cir 2.356194490192 radians)

.:  1.13248262224

> (asecant cir 120 degrees)

.:  1.0730291831

> (asecant hyp 0.3927 radians)

.:  1.58686

> (asecant hyp 45 degrees)

.:  0.72336752453

```

##### Related

cosecant, secant

## asine

Returns the inverse sine.

##### Syntax

(asine _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The inverse sine of the number. |

##### Remarks

##### Example

```

> (asine 0.3927)

.:  0.403566

> (asine cir 0.3927 radians)

.:  0.403566

> (asine cir 95 degrees)

.:  1.570796326+1.092133189i

> (asine hyp 3.141592653589 radians)

.:  1.862295743311

> (asine hyp 120 degrees)

.:  1.4850704719

```

##### Related

cosine, sine

## ask

Sends a message to a recipient and awaits a response.

##### Syntax

(ask _who message option_ _..._ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| who | literal | 1   | A URL or the literal user for the console. |
| message | string | 0-1 | A message or query. |
| option | expression | 0+  | Key value pairs<br><br>timeout _instant_ – delay before terminating request,  <br>default _value_ – value to return upon timeout,<br><br>columns _list_ – a column list is the first record,  <br>if omitted then no columns are listed. (default).<br><br>skip number – skips a number of records<br><br>limit number – number of records or #. (default is 1).  <br>meta where – either before or within. (default is before). |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The response. The value nil is returned if no response was given. |

##### Remarks

Sends a message to the recipient and waits for a response. If user is specified for who, then the input is taken from the console. If the url is a data url, then this function retrieves query results from the data url. If the option columns is provided along with a list of columns, and the option meta is provided along with a location (before or within) then each column name is inserted either in the list element before the data, or within each data list.

##### Example

```

> (ask user "What is your name?")

What is your name? Michael

.:  "Michael"

> (service (url scheme tcp port 5950)

(function reply {?sender ?message}

(tell ?sender ($ received ?message))))

.:  Service-1

> (start Service-1)

.:  Service-1

> (ask (url scheme tcp port 5950) "secret" timeout \\@s5 default NobodyHome)

.:  "received secret"

> (var ?data (data driver sqlserver server "//servername" port 1433

database mydata user "myUid" password "123456")

.:  Data-1

> (open ?data)

.:  Data-1

> (ask Data-1 "select top 10 empid, name, salary from employee" record values)

.:  {{1 "John Smith" 10.50}{2 "Jane Johnson" 12.00} …}

> (ask ?data

"select empid, name, wage from employee limit 2”

columns {empid name wage}

limit 2)

.:  {{empid name wage} {1 "John Smith" 10.50} {2 "Jane Johnson" 12}}

> (ask ?data "select empid, name, wage from employee" limit 2)

.:  {{1 "John Smith" 10.50}{2 "Jane Johnson" 12}}

> (ask ?data "select top 2 empid, name, wage from employee" meta within

columns {:Id :Name :Rate})

.:  {{:Id 1 :Name "John Smith" :Rate 10.50}

{:Id 2 :Name "Jane Johnson" :Rate 12}}

> (ask ?data "select top 2 empid, name, wage from employee"  
columns {:Id :Name :Rate} meta before)

.:  {{:Id :Name :Rate} {1 "John Smith" 10.50} {2 "Jane Johnson" 12}}

> (close ?data)

.:  Data-1

```

##### Related

cancel, free, Service, start, tell

## atangent

Returns the inverse tangent.

##### Syntax

(atangent _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The inverse tangent of the number. |

##### Remarks

None.

##### Example

```

> (atangent 2.356194490192)

.:  1.4691228248

> (atangent 2.356194490192 cir radians)

.:  1.4691228248

> (atangent 120 cir degrees)

.:  1.12533883288

> (atangent 0.785398163397 hyp radians)

.:  1.05930617082

> (atangent 85 hyp degrees)

.:  0.8181615399-1.5707963267i

```

##### Related

tangent

## attach

Registers a knowledge base.

##### Syntax

(attach _knowledege_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base |

##### Results

| Data Type | Description |
| --- | --- |
| knowledge | The opened knowledge base. |

##### Remarks

Enables lookup and modification of a knowledge base.

##### Example

```

> (var ?kb (knowledge url "file:///c:/premise/kb/defultKb.mdb"))

.:  Knowledge-1

> (attach ?kb)

.:  Knowledge-1

> (relation Fact :All :Are)

.:  Fact

> (detach ?kb)

.:  Knowledge-1

> (free (cede (reference ?kb)))

.:  freed

```

##### Related

conceive, detach, each, eradicate, get, knowledge, knowing, put, using, which, with

## average

The arithmetic mean of a sequence.

##### Syntax

(average _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 1   | The literal in or per. |
| sequence | sequence | 1   | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result of applying the plus function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the variables then the function fails. The last expression shall be evaluated and the average function shall be applied to both that expression and any prior result. The final value returned is the sum of all expressions divided by the length of the sequence.

##### Example

```

> (average ?x in (range 1 to 4) ?x)

.:  2.5

> (average ?fruit ?count per {{apple 1}{pear 2}{banana 3}{coconut 4}} ?count)

.:  2.5

```

##### Related

fold, product, summation

## avg

The arithmetic mean.

##### Syntax

(avg _value_ _…_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | An number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The arithmetic mean of all elements in the sequence. |

##### Remarks

Returns the arithmetic mean. If the list or expression is empty, it returns zero. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared

##### Example

```

> (avg {1 2 3 4 5})

.:  3

> (avg {})

.:  0

> (avg 1 2 3 4 5)

.:  3

> (avg {1 2 3} 4 {6 3 2})

.:  {3.66667 3 3}

```

##### Related

max, median, min, statistics, sigma, sum

## await

Returns the result of a task.

##### Syntax

(await _task timeout_ _default_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource |
| timeout | instant | 0-1 | The amount of time to wait for the task. The default is eternity which implies to wait indefinitely |
| default | variant | 0-1 | The value to return once the timeout is reached. If unspecified, then nil is returned. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The task result, or nil. |

##### Remarks

The await function waits for either the timeout duration or the task to complete.

##### Example

```

> (concurrent (repeat 10000000 foo))

.:  Task-2

> (await Task-2 \\@t100000 timed-out)

.:  timed-out

> (await Task-2)

.:  foo

```

##### Related

wait, busy-p, complete, do, done-p, free, task, tarry

## before-p

True if an interval finishes before a second interval.

##### Syntax

(before-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if interval1 finishes some time before interval2. |

##### Remarks

None.

##### Example

```

> (before-p \\@i{\\@s1 \\@s2} \\@i{\\@s2 \\@s4})

.:  false

> (before-p \\@i{\\@s1 \\@s5} \\@i{\\@s6 \\@s8})

.:  true

> (before-p \\@i{\\@s1 \\@s9} \\@i{\\@s4 \\@s6})

.:  false

> (before-p \\@i{\\@s4 \\@s6} \\@i{\\@s8 \\@s9})

.:  true

> (before-p \\@i{\\@s4 \\@s6} \\@i{\\@s6 \\@s9} \\@s1)

.:  false

```

##### Related

during-p, finishes-p, meets-p, overlaps-p, starts-p  

## beginning

Returns the instant an interval begins.

##### Syntax

(beginning _interval_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval | interval | 1   | An interval |

##### Results

| Data Type | Description |
| --- | --- |
| instant | The beinning value of the interval. |

##### Remarks

None.

##### Example

```

> (beginning \\@i{\\@s1 \\@s2})

.:  \\@s1

> (beginning \\@i{\\@s1 \\@s5})

.:  \\@s1

> (beginning \\@i{\\@s4 \\@s6})

.:  \\@s4

```

##### Related

finishing

## best

Returns the best matching candidates.

##### Syntax

(best _probe candidates option_ _..._ )

_option ::= key value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| probe | variant | 1   | The value to compare to the candidates |
| candidates | list | 1   | The candidates to be compared |
| option | expression | 0+  | Key value pairs , where a key is one of:<br><br>limit - The number of matches to return.  <br>(default is 1)<br><br>minscore - value below which candidates shall not be considered. Default is ninfinity<br><br>maxscore – Value above which candidates are acceptable. Default is 1.<br><br>transform – The literal name of a value transformation function.<br><br>comparer - The literal name of a comparison function |

##### Results

| Data Type | Description |
| --- | --- |
| list | A sorted list of lists containing candidate - score pairs. |

##### Remarks

Best compares a probe to candidates and returns the best matching candidate(s) with match score(s). It uses the similarity function (~) as the default comparer. If provided, transforms are applied before comparison. Finally, a comparer can accept two values and returns a score representing the degree of similarity where higher means more similar.

##### Example

```

> (best "this" {"there" "that" "though" "thin"})

.:  {{"thin" 0.142857}}

> (best 345 (range 1 to 1000000) limit 5 minscore -1 maxscore 1 comparer ~)

.:  {{345 1}{344 0.5}{346 0.5}{343 0.333333}{347 0.3333333}}

```

##### Related

~ _similarity_, /~ _dissimilarity_

## beyond

True if a position is outside a sequence.

##### Syntax

(beyond _sequence position_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| position | variant | 1   | A number or coordinate (i.e. a list of numbers). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the position is not in the sequence, false otherwise. |

##### Remarks

None.

##### Example

```

> (beyond "not empty" 5)

.:  false

> (beyond {not empty} 1)

.:  false

> (beyond "" 1)

.:  true

> (beyond {{a b}{c d}{e f}} {3 2})

.:  false

> (beyond {{a b}{c d}{e f}} {7 4})

.:  true

```

##### Related

@ _element_, length, void, more, within

## big

Converts a value to a big number.

##### Syntax

(big _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Data Type | Description |
| --- | --- |
| monadic | An monadic number. |

##### Remarks

A big number is bounded by memory. if the value cannot be converted to a big number, the function fails. The fractional part of the number is truncated. A suffix b denotes a big number.

##### Example

```

> (big {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (big "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not a number."\]

> (big 500.3)

.:  500b

> (big "23.4")

.:  23b

> (big "2982039842304982039842187591823741209250293823978298234187235897234234237429387903984203948203984209813719875209856087197129871")

.:  2982039842304982039842187591823741209250293823978298234187235897234234237429387903984203948203984209813719875209856087197129871b

```

##### Related

ceiling, complex, floor, integer, long, radix, rational, real, round, truncate, unsigned

## bind

Assigns variables to values in sequences or assortments.

##### Syntax

(bind _container assignment_ … )

_assignment_ ::= _slot symbol_

_assignment_ ::= _function symbol_

_assignment_ ::= _position symbol_

_assignment_ ::= {_slot_ … } as _symbol_

_assignment_ ::= {_function_ … } as _symbol_

_assignment_ ::= {_position_ … } as _symbol_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment |
| assignment | expression | 1+  | A key symbol, or position symbol, or list symbol pair. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

The key may be a position, function, slot, method, list of functions, or other value.

##### Example

```

> (relation Node :Data :Next)

.:  Node

> (new Node :Data C :Next (new Node :Data B :Next (new Node :Data A)))

.:  Node_3

> (bind Node_3 :Data ?last {:Next :Next :Data} ?first)

.:  true

> (bind {a b {c {d e}}} 1 ?a {3 2 2} ?e (given {?x} (uppercase ($ (@ ?x)))) ?a)

.:  true

```

##### Related

dynamic, given, global, scope, set, tie

## bindings

Returns a list of symbol value pairs for a pattern.

##### Syntax

(bindings _pattern option …_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| pattern | variant | 1   | A premise or pattern |
| option | expression | 0+  | An option for retrieving the bindings.<br><br>limit n - the number of results to return. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of all symbol value pairs |

##### Remarks

Returns a series containing binding lists that match the pattern. If no variables are in the pattern, then a premise is returned for each match and nil is specified for the symbol.

##### Example

```

> (relation Poll :Response)

.:  Poll

> (step ?i from 1 to 1000

(new Poll :Response (on (> (radom 0 to 1) 0) Yes No)))

.:  Poll_1000

> (for ?bindings in (bindings \[Poll :Respones as ?response\] limit 5)

(tell user ($ ?bindings))

{?response yes} {?response no} {?response yes} {?response no} {?response no}

.:  told

> (for ?bindings in (bindings \[Poll :Respones yes\] limit 4)

(tell user ($ ?bindings))

{nil \[Poll ^ Poll_1 :Response yes\]} {nil \[Poll ^ Poll_3 :Response yes\]}

{nil \[Poll ^ Poll_8 :Response yes\]} {nil \[Poll ^ Poll_9 :Response yes\]}

.:  told

```

##### Related

tally, using, which, with

## bion

Returns a resource that hosts a cluster of cells for doing tasks.

##### Syntax

(bion _name work_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | string | 0-1 | The name of the bion |
| work | string | 0-1 | The work to be done. |

##### Results

| Data Type | Description |
| --- | --- |
| bion | A bion resource. |

##### Remarks

None.

##### Example

```

> (function main {}

(let ?bion (bion) ?cell (cell ?bion))

(start ?cell)

(let ?task (task ?cell (scope) (given {string ?name} ($ Hello, ?name))))

(tell user (await (start ?task "World")))

(halt ?cell)

(halt ?bion)

(free ?cell)

(free ?bion)

)

.:  main

> (main)

Hello World

.:  freed

```

##### Related

cell, halt, start, task

## bitwise

Performs bitwise operations.

##### Syntax

(bitwise _number op_ _…_ )

_op ::= operation number_

_op ::=_ not

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| op  | expression | 1+  | an operation or operation value pair where the operation is either and, or, not, nand, nor, xor, <<, >>, or count and where the value is a number _y_ such that:<br><br>and y – performs logical and<br><br>or y – performs logical or<br><br>not – performs complement<br><br>nand y – performs logical nand<br><br>nor y – performs logical nor<br><br>xor y – performs exclusive or<br><br>xnor y – performs exclusive or<br><br><< y – performs left shift of x for y iterations<br><br>>> y – performs right shift of x for y iterations<br><br>count y – returns the number of bits that = y<br><br>(where y is either 1 or 0) |

##### Results

| Data Type | Description |
| --- | --- |
| number | Result depends on the operation. |

##### Remarks

Each operation is performed in succession and the final result is returned.

##### Example

```

> (bitwise 2 and 3)

.:  2

> (bitwise 31 or 14)

.:  31

> (unsigned (bitwise 31 or 14 and 2))

.:  2

> (function countOneBits {?a}

(bitwise ?a count 1))

.:  countOneBits

> (countOneBits 255)

.:  8

> (bitwise 31 xor 14 count 1)

.:  2

> (function countConversionBits {?a ?b}

(bitwise ?a xor ?b count 1))

.:  countConversonBits

```

##### Related

\+ _plus_, - _minus_, unsigned

## bound

Returns the variables that are bound in a function.

##### Syntax

(bound _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | variant | 1   | A function. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of variables. |

##### Remarks

None.

##### Example

```

> (function foo {?x ?y + ?z}

(bar ?x ?y)

(baz ?z ?a))

.:  foo

> (bound foo)

.:  {?x ?y ?z}

> (unbound foo)

.:  {?a}

> (bound (' (given {?s} (@ ?s ?p))))

.:  {?s}

> (unbound (' (given {?s} (@ ?s ?p))))

.:  {?p}

```

##### Related

unbound

## bound-p

True if a symbol has a value.

##### Syntax

(bound-p _symbol_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol. |

##### Results

| Data Type | Description |
| --- | --- |
| bool | True if the symbol is bound. |

##### Remarks

None.

##### Example

```

> (let ?a 1 ?b 2)

.:  true

> (bound-p ?a)

.:  true

> (bound-p ?b)

.:  true

> (bound-p ?c)

.:  false

```

##### Related

unbound-p

## bracket

Returns 1 if a truth expression is true, 0 if false, and -1 if unknown.

##### Syntax

(bracket _truth_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 1   | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| integer | Returns 1 if the truth value is true, 0 if false, and -1 if unknown.. |

##### Remarks

None.

##### Example

```

> (bracket true)

.:  1

> (bracket false)

.:  0

> (bracket banana)

.:  \[Failure :Name InvalidType :Text "A truth was expected instead of banana."\]

> (bracket unknown)

.:  -1

```

##### Related

all, any, convert, every, nall, nevery, no, none, some,

## break

Terminates a loop.

##### Syntax

(break _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | Any value to be returned. Default is nil. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the value if provided, otherwise returns nil |

##### Remarks

Exits a loop with a return value or nil if no return value is specified. Can be used for a do loop.

##### Example

```

> (for ?item in (range 1 to 1000000)

(if (= ?item 123456) (break))

done)

.:  nil

> (for ?item in (range 1 to 1000000)

(if (= ?item 123456) (break foo))

done)

.:  foo

```

##### Related

fail, resume, return, try

## busy-p

True if a task has not completed.

##### Syntax

(busy-p _task_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the task has not completed |

##### Remarks

Returns true if the task has not completed, false otherwise. The opposite of this function is ready-p.

##### Example

```

> (let ?task (@ (concurrent (idle \\@s100))))

.:  true

> (do (idle \\@s20)

(if (busy-p ?task)

running

else

(free ?task)))

.:  running

```

##### Related

cancel, cancelled-p, wait, await, complete, ready-p, reclaim, tarry, task

## but

Creates a subsequence of all except the last elements.

##### Syntax

(but _sequence quantity_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |
| quantity | number | 0-1 | The number of elements to omit. Defaults to 1. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The selected sub sequence |

##### Remarks

If quantity is omitted, then all but the last item is returned. This is the opposite of rest.

##### Example

```

> (but {a b c d e f})

.:  {a b c d e}

> (but {a b c d e f} 3)

.:  {a b c}

> (but "abcde" 2)

.:  "abc"

```

##### Related

@ _element_, last, rest, top

## bye

Terminates the interpreter.

##### Syntax

(bye)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| code | integer | 0-1 | An integer exit code. (Default is zero.) |

##### Results

None

##### Remarks

Terminates the read-eval-print loop.

##### Example

```

> (bye)

Bye!

```

##### Related

exit

## call

Creates a call.

##### Syntax

(call _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| call | The concatenated call. |

##### Remarks

Returns an unevaluated call. Note the call must have at least one value, preferably a literal. Note that an empty call cannot be invoked.

##### Example

```

> (call foo {})

.:  (foo {})

> (call tell me "hello world")

.:  (tell user "hello world"))

> (call)

.:  \[Failure :Name ArgumentRequired :Text "A required argument was not supplied."\]

> (call given {?x} (+ ?x ?x))

.:  (given {?x} (+ ?x ?x))

```

##### Related

$, &, closure, eval, invoke, list, tuple, quote

## can

Evaluates an expression while suppressing failures.

##### Syntax

(can _expression result error_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | An expression to evaluate. |
| result | reference | 0-1 | A symbol reference. |
| error | reference | 0-1 | A symbol reference |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if no failure occurred;. result and error shall contain respective values |

##### Remarks

If the expression succeeds, the result symbol shall contain the result the evaluated expression and the error symbol shall be nil. If the expression fails, the result shall be nil and the error symbol shall contain the failure.

##### Example

```

> (let ?result nil ?error nil)

.:  true

> (can (string x) (reference ?result) (reference ?error))

.:  true

> ?result ?error

.:  "x" nil

.:  (can (integer x) (reference ?result) (reference ?error))

.:  false

> ?result ?error

.:  nil \[Failure :Name TypeConversion :Text "Cannot convert x to Integer."\]

```

##### Related

assert, did, ensure, fail, finally, may, try

## cancel

Cooperatively ancels tasks.

##### Syntax

(cancel _tasks_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| tasks | variant | 1   | A single task resource or a list of task resources. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the tasks or list of tasks. |

##### Remarks

Cancels an executing task. The task shall be signaled to terminate. The task must call cancelled-p to determine whether to terminate, and if so, call exit or return.

##### Example

```

> (concurrent (step ?i from 1 to 100000 (if (cancelled-p (self)) (break oops)) finished)

(step ?i from 1 to 100000 finished))

.:  {Task-57 Task-58}

> (cancel task-57)

.:  task-57

> (await task-57)

.:  oops

> (abort task-58)

.:  task-58

> (free {task-57 task-58})

.:  freed

```

##### Related

wait, abort, await, cancelled-p, complete, critical, do, done-p, reclaim , start, task, task-p, tasks

## cancelled-p

True if a task has been cancelled.

##### Syntax

(cancelled-p _task_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the task has been cancelled. |

##### Remarks

The task may be cancelled using the cancel function. The cancel function sets a flag which must be recognized by the running task so that it can cooperatively terminate itself. Therefore all tasks should routinely invoke the cancelled-p function to determine whether they must terminate.

##### Example

```

> (concurrent (step ?i from 1 to infinity

(if (cancelled-p (self)) (break quitting))

finished))

.:  {Task-57}

> (idle \\@s5)

.:  ready

> (cancel task-57)

.:  cancelled

> (await task-57)

.:  quitting

```

##### Related

wait, abort, await, cancel, cancelled-p, complete, do, reclaim, self, task

## canonify

Makes equal values identical.

##### Syntax

(canonify _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | A thing.. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The canonified value. |

##### Remarks

Calling canonify with no arguments shall clear the canon of all stored values.

##### Example

```

> (global ?Original "The quick brown fox" ?Clone (clone ?Original))

.:  true

> (= ?Original ?Clone)

.:  true

> (identical-p ?Original ?Clone)

.:  false

> (set ?Original (canonify ?Original) ?Clone (canonify ?Clone))

.:  true

> (identical-p ?Original ?Clone)

.:  true

```

##### Related

\=, clone, copy, make, identical-p, identity, same

## capitalize

Capitalizes a string.

##### Syntax

(capitalize _string option_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A string to capitalize |
| option | expression | 0-1 | A key value pair<br><br>words _which_\- where _which_ is all or first (default). |

##### Results

| Data Type | Description |
| --- | --- |
| string | The capitalized string |

##### Remarks

Capitalizes the string.

##### Example

```

> (capitalize "the quick brown fox")

.:  "The quick brown fox"

> (capitalize "the quick brown fox" words all)

.:  "The Quick Brown Fox"

> (capitalize "the quick brown fox" words first)

.:  "The quick brown fox"

```

##### Related

lowercase, uppercase

## case

Branches execution based on a value.

##### Syntax

(case _probe clause_ _…_ _else-clause_)

_clause_ ::= of _value expression_ _…_

_clause_ ::= in {_value_ _…_ } _expression_ _…_

_else-clause_ ::= else _expression_ _…_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| probe | variant | 1   | a value to compare |
| clause | expression | 1+  | Test value and expressions to be evaluated |
| else-clause | expression | 0-1 | A default case and expressions to be evaluated |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value in the successful clause |

##### Remarks

The first expression is evaluated and its result is matched against the of or in values. The comparison stops as soon as the first match is made. When that happens, the various expressions following the value are evaluated, one at a time. If no of or in expression is matched, then if an else clause exists, the expressions are evaluated, otherwise nil is returned.

##### Example

```

> (global ?Value a)

.:  true

> (case ?Value

of b nope

in {c d} nope

else not-found)

.:  not-found

```

##### Related

and, if, not, or, unless

## categorize

Returns a list of equivalence sets.

##### Syntax

(categorize _sequence predicate_ _…_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| predicates | function | 1+  | Unary truth predicates. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of sublists each containing elements partitioned by a predicate.. |

##### Remarks

A result sublist is returned for each predicate which determines if each item belongs in the respective equivalence set. If the predicate is true for the item, it is added to the result sublist.

##### Example

```

> (categorize (3 5 2 0 5 8 9} even odd zero)

.:  {{even 2 0 8}{odd 3 5 5 9}{zero 0}}

> (categorize "abcdefghijk" (given {?x} (< ?x "e")))

.:  {{(given {?x} (< ?x "e")) "a" "b" "c" "d"}}

```

##### Related

partition

## cede

Transfers a value between variables.

##### Syntax

(cede _reference_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| reference | reference | 1   | A symbol reference |

##### Results

| Data Type | Description |
| --- | --- |
| variant | the value formerly held by the symbol . |

##### Remarks

Transfers a value from one symbol to another, ensuring only one symbol is pointing to a value.

##### Example

```

> (function matrix+ {??a ??b}

(ensure reference ??a reference ??b)

(let ?r (cede ??a))

(traverse ?i into ??b limit (dimensions ?r)

(==> ?r + ?i (@ ??b ?i)) )

(set ??b nil)

(return ?r))

.:  matrix+

> (let ?x (array {9000 9000} each (given {?c}(random 0 to 1)))

?y (array {9000 9000} each (given {?c}(random 0 to 1)))

?z (matrix+ (reference ?x)(reference ?y)))

.:  true

> (is ?x null-p) (is ?y null-p) (is ?z null-p)

.:  true true false

```

##### Related

copy, new, relation

## ceiling

Rounds a number towards positive infinity.

##### Syntax

(ceiling _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| number | The next higher positive integer. |

##### Remarks

Returns the next highest positive integer.

##### Example

```

> (ceiling 100.5)

.:  101

> (ceiling -100.5)

.:  -100

```

##### Related

floor, round, truncate

## cell

Creates a resource for performing tasks.

##### Syntax

(cell _bion work_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| bion | bion | 1   | A bion resource. |
| work | string | 0-1 | The work to be done. |

##### Results

| Data Type | Description |
| --- | --- |
| cell | A cell resource. |

##### Remarks

None.

##### Example

```

(function main {}

(let ?bion (bion) ?cell (cell ?bion))

(start ?cell)

(let ?task (task ?cell (scope) (given {string ?name} ($ Hello, ?name))))

(tell user (await (start ?task "World")))

(halt ?cell)

(halt ?bion)

(free ?cell)

(free ?bion)

)

.:  main

> (main)

Hello World

.:  freed

```

##### Related

bion, halt, start, task

## char

Converts a Unicode value into a one position string.

##### Syntax

(char _unicode_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| unicode | variant | 1   | A unicode value between 0 and 65535 or the literal maximum or minimum. |

##### Results

| Data Type | Description |
| --- | --- |
| string | A string containing the character. |

##### Remarks

None.

##### Example

```

> (char 65)

.:  "A"

```

##### Related

unicode

## choose

Returns the elements of a sequence that satisfies a function.

##### Syntax

(choose _sequence selector transform_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence of values. |
| selector | function | 1   | The function to be applied. |
| transform | function | 0-1 | A function that returns a key given a sequence element prior to computing the selector. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of elements satisfying the function. |

##### Remarks

Returns the elements in the sequence that satisfy the function. If the sequence is empty, it returns an empty list. The transform function takes elements of the sequence and returns numbers before computing the function of the transformed sequence.

##### Example

```

> (choose {1 2 3 4 5} max)

.:  {5}

> (choose {a b c d e} max)

.:  {e}

> (choose {} max)

.:  {}

  
\> (choose {{a 0}{b 1}{c 2}{d 0}} min (given {?item} (@ ?item 2)))

.:  {{a 0}{d 0}}

```

##### Related

max, min, partition

## clear

Eliminates all entries from an assortment or sequence.

##### Syntax

(clear _container_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |

##### Results

| Data Type | Description |
| --- | --- |
| thing | The modified assortment or sequence. |

##### Remarks

This function clears dynamic assortments and sequences. The clear function shall fail on fixed assortments (i.e. enumerations, records, and prototypes) . For fixed assortments use zap to set slots values to nil.

##### Example

```

> (var ?s (lexicon a 1 b 2 c 3 d 4) ?list {a b c})

.:  {a b c}

> (entries ?s)

.:  {{a 1}{b 2}{c 3}{d 4}}

> (entries (clear ?s))

.:  {}

> (clear ?list)

.:  {}

> ?list

.:  {}

```

##### Related

add, includes, item, items, keys, reclaim, #, tie, values

## clip

Returns a value within a clipped range.

##### Syntax

(clip _number minimum maximum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| minimum | number | 1   | A number (default is ninfinity) |
| maximum | number | 1   | A number (default is infinity) |

##### Results

| Data Type | Description |
| --- | --- |
| number | Returns the number constrained to the range. |

##### Remarks

If the value is greater than the maximum, the maximum is returned. If the value is less than the minimum, the minimum is returned, otherwise the value is returned.

##### Example

```

> (clip 3 0 5)

.:  3

> (clip 7 0 5)

.:  5

> (clip -4 0 5)

.:  0

> (clip 84 ninfinity 100)

.:  84

>(clip 84 0 infinity)

.:  84

```

##### Related

max, min

## clone

Clones an atom with possible modifications.

##### Syntax

(clone _atom modification_ _…_ )

_modification_ ::= _key value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| atom | atom | 1   | An atomic value.. |
| modification | expression | 0+  | A key value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| thing | The copy. |

##### Remarks

A duplicate or shallow copy of the original value is made. Zero or more modifications may be specified and applied after the value is cloned. If the value is a SubThought and the relation has an !onNew method defined, that method is first run on the clone. If an !onClone event method is defined, then the onClone method is invoked thereafter. The clone event (!onClone) requires two parameters {?clone ?original}. To clone sequences use the copy function.

##### Example

```

> (relation Car

:Make :Model :Year :Version 1

!onClone (function Car_clone {?m ?o}(==> ?m ++ :Version (:Version ?o))))

.:  Car

> (premise (new Car :Make oole :Model civic :Year 2000))

.:  \[Car ^ Car_1 :Make oole :Model civic :Version 1 :Year 2000 !onClone Car_clone\]

> (premise (clone Vehicle_1 :Year 2016))

.:  \[Car ^ Car_2 :Make oole :Model civic :Version 2 :Year 2016 !onClone Car_clone\]

```

##### Related

copy, new, relation

## close

Closes a file or data url.

##### Syntax

(close _url_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A file or data url. |

##### Results

| Data Type | Description |
| --- | --- |
| url | The url. |

##### Remarks

Closes an open url.

##### Example

```

> (var ?file (file name "kwikfox.txt"))

.:  File-1

> (open ?file)

.:  File-1

> (let ?contents (read ?file #))

.:  true

> ?contents

.:  "The quick brown fox jumped over the lazy dogs."

> (close ?file)

.:  File-1

```

##### Related

close, data, file, open

## closure

Creates a public function in a module.

##### Syntax

(closure _scope type name parameters expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment or module name. |
| type | literal | 1   | The literal function or macro |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

The closure intrinsic defines a function or macro with an explicit scope. a new scope shall be constructed for the function (or macro) using variables and function definitions contained in the ancestral scopes. If the name is supplied, then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided. The first variables in the parameter list are required. If a plus sign is provided, then those variables following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example

```

> (closure (scope) function {?n} (+ 1 ?n))

.:  fn-1

> (closure (scope) function plusN {?n + ?i = 1} (+ ?n ?i))

.:  plusN

> (fn-1 100)

.:  101

> (plusN 100)

.:  101

> (closure (scope go -1)

function tryParseNum {?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

.:  tryParseNum

> (tryParseNum "foo")

.:  {false nil}

> (tryParseNum "123")

.:  {true 123}

> (closure (scope of User)

macro set2 {?value ?var1 ?var2}

"puts value into two variables in parallel"

(eval (\` (set , ?var1 , ?value , ?var2 , ?value))))

.:  set2

> (let ?x1 nil ?x2 nil) ?x1 ?x2

.:  true nil nil

(set2 (+ 2 2) ?x1 ?x2)

> ?x1 ?x2

.:  4 4

```

##### Related

arguments, call, extend, function, macro, module, modules, parameters

## coalesce

Returns a merged sequence.

##### Syntax

(coalesce _symbol_ _…_ _gate_ _expression_ _…_ )

_gate ::=_ in _sequence_

_gate ::=_ per _sequence_

_gate ::=_ from _expression_ _…_ until _predicate_

_gate ::=_ from _expression_ _…_ while _predicate_

_gate ::=_ from _i_ _limit_ _j_ by _k_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| gate | expression | 1   | One of the gates expressions listed above.<br><br>where i is the initial value of the symbol,<br><br>limit is any of to, above, below or go.<br><br>where j is the final value of the symbol,<br><br>and k is the optional increment. |
| expression | variant | 1+  | An expression that potentially transforms the iteration symbol |

##### Results

| Data Type | Description |
| --- | --- |
| list | A new merged list after the transformation is applied |

##### Remarks

In the case of in or per For each element in the sequence, the element is stored in the symbol, and then the expressions are evaluated. If from is specified, each symbol is bound to the initally evaluated expression. If to is specified, the symbol is assumed to be a number, and the last number is included in the iteration. If below or above is specified the last number is excluded from the iteration. If go is specified, then the j value is the number of iterations. On each iteration the expressions are evaluated, and the last expression is collected into a merged result list.

##### Example

```

> (collect ?n in {1 2 3 4} {(\* ?n 3) (\* ?n 2)})

.:  {{3 2}{6 4}{9 6}{12 8}}

> (coalesce ?n from 1 while (<= ?n 4) {(\* ?n 3) (\* ?n 2)}))

.:  {3 2 6 4 9 6 12 8}

> (collect ?x ?y per {{1 1}{1 2}{2 5}} {(/ ?x ?y) (\* ?x y)})

.:  {{1 1}{0.5 2}{0.4 10}}

> (coalesce ?x ?y per {{1 1}{1 2}{2 5}} {(/ ?x ?y) (\* ?x y)})

.:  {1 1 0.5 2 0.4 10}

> (coalesce ?n in {1 2 3 4} {(\* ?n 3)})

.:  {3 6 9 12}

> (coalesce ?i from 1 to 9 by 2 {?i})

.:  {1 3 5 7 9}

> (coalesce ?n from 1 below 5 {(\* ?n 3)})

.:  {3 6 9 12}

> (coalesce ?i from 1 go 4 (pick {a b c d e f g h i j} ?i))

.:  {c h b e a c d j c f e b h j c}

```

##### Related

collect, filter, map , reduce, scale

## collect

Returns a transformed sequence.

##### Syntax

(collect _symbol_ _…_ _gate_ _expression_ _…_ )

_gate ::=_ in _sequence_

_gate ::=_ per _sequence_

_gate ::=_ from _expression_ _…_ until _predicate_

_gate ::=_ from _expression_ _…_ while _predicate_

_gate ::=_ from _i_ _limit_ _j_ by _k_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| gate | expression | 1   | One of the gates expressions listed above.<br><br>where i is the initial value of the symbol,<br><br>limit is any of to, above, below or go.<br><br>where j is the final value of the symbol,<br><br>and k is the optional increment. |
| expression | variant | 1+  | An expression that potentially transforms the iteration symbol |

##### Results

| Data Type | Description |
| --- | --- |
| list | A new list after the transformation is applied |

##### Remarks

In the case of in or per For each element in the sequence, the element is stored in the symbol, and then the expressions are evaluated. If from is specified, each symbol is bound to the initally evaluated expression. If to is specified, the symbol is assumed to be a number, and the last number is included in the iteration. If below or above is specified the last number is excluded from the iteration. If go is specified, then the j value is the number of iterations. On each iteration the expressions are evaluated, and the last expression is collected into a result list.

##### Example

```

> (collect ?n in {1 2 3 4} (\* ?n 3))

.:  {3 6 9 12}

> (collect ?x ?y per {{1 1}{1 2}{2 5}} (/ ?x ?y))

.:  {1 0.5 0.4}

> (collect ?i from 1 to 9 by 2 ?i)

.:  {1 3 5 7 9}

> (collect ?n from 1 below 5 (\* ?n 3))

.:  {3 6 9 12}

> (collect ?i from 1 go 4 (pick {a b c d e f g h i j} ?i))

.:  {{c} {h b} {e a c} {d j c f} {e b h j c}}

```

##### Related

coalesce, filter, map , reduce, scale

## collection

Returns an unorderd collection of elements.

##### Syntax

(collection _element_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| element | variant | 0+  | A key. |

##### Results

| Data Type | Description |
| --- | --- |
| collection | A collection. |

##### Remarks

A collection is an unordered set of elements.

##### Example

```

> (collection

{a b c} "foo" bar 500 \[Fruit :Name Apple\])

.:  Collection-1

> (has Collection-1 foo)

.:  false

> (has Collection-1 "foo")

.:  true

```

##### Related

enumeration, environment, lexicon

## combine

Creates a new assortment by combining entries.

##### Syntax

(combine _assortment entry_ _…_ )

_entry ::=_ _key value_

_entry ::=_ _key_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment or sequence |
| entry | expression | 1+  | A key, or key value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The modified assortment. |

##### Remarks

Collections require only a key for each entry. Assortments require a key and value for each entry.Use the add function to modify an assortment.

##### Example

```

> (entries (add (lexicon) a 1 b 2 c 3))

.:  {{a 1}{b 2}{c 3}}

> (entries (add (collection) 1 2 3 4 5))

.:  {{1 1}{2 2}{3 3}{4 4}{5 5}}

```

##### Related

add

## common

Creates a sequence of common elements among subsequences.

##### Syntax

(common _sequences_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequences | sequence | 1   | A sequence containing sequences |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A list of common items |

##### Remarks

Returns the intersection of the subsequences, i.e., the elements common to all subsequences.

##### Example

```

> (common {{1 2 3 4} {2 3 4 5}})

.:  {2 3 4}

> (common {{2 3 4 5} {4 5 6 7}})

.:  {4 5}

> (common (map {\[Data :A {1 2 3 4}\] \[Data :A {2 3 4 5}\]} (given {?d} (:A ?d))))

.:  {4}

> (common {"abc" "bcd" "cde"})

.:  "c"

```

##### Related

difference, intersection, union

## comparable-p

Returns true if the values can be compared.

##### Syntax

(comparable-p _value<sub>1</sub> value<sub>2</sub>_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | A value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the values can be compared. |

##### Remarks

Returns true if the values are of the same type and their elements are of the same type, false otherwise.

##### Example

```

(comparable-p 1 2)

.:  true

(comparable-p 2 x)

.:  false

(comparable-p {1 2 3 4}{2 3 4 5})

.:  true

(comparable-p {1 2 3 4}{a b c d})

.:  false

(comparable-p b a)

.:  true

(comparable-p z {a b c})

.:  false

```

##### Related

\= _equal_, /= _unequal_

## compare

Returns less, equal, or greater.

##### Syntax

(compare _value<sub>1</sub> value<sub>2</sub>_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | A value |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns < (less than), \= (equals), or > (greater than). |

##### Remarks

Returns the less than literal if the first value is less than the second value, the equal literal if the values are equal, and the greater than literal if the first value is greater than the second value. The function fails if the values are not comparable (i.e., of the same type).

##### Example

```

(compare 1 2)

.:  <

(compare 2 1)

.:  >

(compare {1 2 3 4}{2 3 4 5})

.:  <

(compare a a)

.:  =

(compare b a)

.:  >

```

##### Related

\= _equal_, /= _unequal_

## complete

Runs expressions concurrently.

##### Syntax

(complete _expression_ _…_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of task resources. |

##### Remarks

Executes the expressions concurrently, and returns after the last expression completes, returning a list of task handles. If expression is not a task, then the expression is converted to a task prior to execution.

##### Example

```

> (complete

(step ?i from 0 to 50000000 (do nothing))

(step ?i from 1 to 10000000 (do something))))

.:  {task-1 task-2}

> (free (wait {task-1 task-2}))

.:  freed

```

##### Related

abort, await, concurrent, do, busy-p, free, ready-p, start, tarry, task, tasks, wait

## complex

Converts a value to a complex number.

##### Syntax

(complex _real imaginary_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| real | real | 1   | A number value or the literal minimum or maximum |
| imaginary | imaginary | 1   | A number value or the literal minimum or maximum |

##### Results

| Data Type | Description |
| --- | --- |
| complex | A complex number. |

##### Remarks

If the values cannot be converted to a complex number, the function fails.

##### Example

```

> (complex {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (complex "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not a number."\]

> (complex 500 8i)

.:  500+8i

> (complex 500.3 0)

.:  500.3+0i

> (complex "23.4" "0i")

.:  23.4+0i

```

##### Related

ceiling, complex, floor, long, rational, real, round, truncate,

## compose

Applies functions in reverse order using the arguments.

##### Syntax

(compose _functions arguments_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| functions | list | 1   | A list of functions to be applied in reverse order. |
| arguments | variant | 0-1 | The arguments to the last function in the functions list. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The result of the last call |

##### Remarks

If the arguments parameter is an empty list, the rightmost function is assumed to be niladic (requiring no arguments). The rightmost function is applied to the arguments parameter, then the second from rightmost is applied to the result, and so on, until all functions are applied. The final result is returned. The opposite function is morph. The scatter function applies functions in parallel.

##### Example

```

> (function double {?x} (\* ?x 2))

.:  double

> (compose {double ++ ++ ++} {0})

.:  6

> (compose {rest but rest but}

{{the quick brown fox jumped over the lazy dogs}})

.:  {brown fox jumped over the}

> (compose {double ++ ++ +} {2 3 4})

.:  22

```

##### Related

apply, map, morph, scatter

## conceive

Creates a knowledge base.

##### Syntax

(conceive _knowledege_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base |

##### Results

| Data Type | Description |
| --- | --- |
| knowledge | The opened knowledge base. |

##### Remarks

Constructs a new knowledge base if one does not already exist.

##### Example

```

> (conceive (var ?kb (knowledge name defaultKB path "c://premise/kb/")))

.:  defaultKB

> (attach ?kb)

.:  defaultKB

> (relation Fact :All :Are)

.:  Fact

> (detach ?kb)

.:  defaultKB

> (free (cede (reference ?kb)))

.:  freed

```

##### Related

attach, detach, each, eradicate, get, knowing, knowledge, put, using, which, with

## concurrent

Evaluates expressions asynchronously.

##### Syntax

(concurrent _expression_ _…_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| list | The executing task resources. |

##### Remarks

If expression is not a task, then the expression is converted to a task. Each taks is then started asynchronous and a list of the executing tasks is returned.

##### Example

```

> (concurrent (+ 1 2 3 4) (/ 1000 57) (** 4 20))

.:  {Task-1 Task-2 Task-3}

> (await task-1)

.:  10

> (await task-2)

.:  17.54385964912281

> (await task-3)

.:  1099511627776

> (free task-1 task-2 task-3)

.:  nil

> (free (tarry (concurrent (+ 1 2 3 4) (/ 1000 57) (** 4 20))))

.:  freed

```

##### Related

await, busy-p, cancel, cancelled-p, conclude, critical, is, free , ready-p, self, tarry, task, tasks, wait

## configuration

Creates a configuration file.

##### Syntax

(configuration _url association_ _..._ )

_association_ ::= _section settings_

_settings_ ::= { _setting setting_ }

_setting_ ::= _key value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url. |
| association | expression | 0+  | A section literal and list of key value pairs. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The value associated with the key. |

##### Remarks

This function creates a configuration file at the specified URL. The file constis of sections that have key value pairs.

##### Example

```

> (configuration "c$/apps/premise/myApp.cfg" security {User John password "foo"}))

.:  :Configuration-1

> (get Configuration-1 security password)

.:  "foo"

> (put (get Gonfiguration-1 security) password "bar")

.:  Lexicon-248

> (get Configuration-1 security password)

.:  "bar"

```

##### Related

add, cut, erase, get, put

## confirm

Tests that a condition is true.

##### Syntax

(confirm _condition_ since _reason_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | The test. If it evaluates to false the function fails |
| since | literal | 0-1 | The literal since. |
| reason | string | 0-1 | The failure text to display. Defaults to "Assertion failure." if not supplied. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if test is true. |

##### Remarks

If the since keyword and reason are omitted, the failure text shall be "Failed condition." The failure name is always "Confirmation" .

##### Example

```

> (confirm (= red blue) since "colors must be the same")

.:  \[Failure :Name Assertion :Text "colors must be the same"\]

> (function reducing {?sequence ?function}

(ensure sequence ?sequence function ?function)

(confirm (> (# ?sequence) 1) since "Two or more elements are required.")

(let ?result (@ ?sequence))

(for ?element in (rest ?sequence) (--> ?function ?result ?element)))

.:  reducing

> (reducing {1} +)

.:  \[Failure :Name Confirmation :Text "Two or more elements are required."\]

```

##### Related

confute, ensure, fail, signal, try

## confute

Tests that a condition is false.

##### Syntax

(confute _condition_ since _reason_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | The test. If it evaluates to false the function fails |
| since | literal | 0-1 | The literal since. |
| reason | string | 0-1 | The failure text to display. Defaults to "Rejection failure." if not supplied. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns false if test is false. |

##### Remarks

If the since keyword and reason are omitted, the failure text shall be "Failed condition." The failure name is always "Confutation." .

##### Example

```

> (confute (= red blue) since "colors must be different")

.:  false

> (function reducing {?sequence ?function}

(ensure sequence ?sequence function ?function)

(confute (<= (# ?sequence) 1) since "Two or more elements are required.")

(let ?result (@ ?sequence))

(for ?element in (rest ?sequence) (--> ?function ?result ?element)))

.:  reducing

> (reducing {1} +)

.:  \[Failure :Name Confutation :Text "Two or more elements are required."\]

```

##### Related

confirm, ensure, fail, signal, try

## constant

Creates a constant.

##### Syntax

(constant _assignment_ _…_ )

_assignment_ ::= _symbol value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assignment | expression | 1+  | Symbol and value pairs. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates constant variables in the current environment. Any attempts to put a different value into the symbol shall create a failure. Calling constant again on the variables is allowed.

##### Example

```

> (constant ?SECRET "mysecret")

.:  true

> ?SECRET

.:  "mysecret"

> (constant ?MIN_ENTRIES 300

?MAX_ENTRIES 400)

.:  true

> ?MAX_ENTRIES

.:  400

```

##### Related

<-- _before tie_, --> _after tie_, global, dynamic, modular, local

## contains

True if a value is present in an assortment.

##### Syntax

(contains _assortment value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | A sequence or assortment |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the key is present. or false if the key is absent. |

##### Remarks

None

##### Example

```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.:  Lexicon-1

> (contains Lexicon-1 3)

.:  true

> (contains Lexicon-1 X_foo)

.:  true

> (contains Lexicon-1 elephant)

.:  false

```

##### Related

has, lacks, missing

## continue

Continues to the next iteration of a loop.

##### Syntax

(continue _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | A return value for the next iteration. |

##### Results

| Data Type | Description |
| --- | --- |
| value | Returns the value if provided, otherwise returns nil |

##### Remarks

If this is executed within a loop, then the next iteration resumes until the loop is completed. If this is executed outside of a loop, then the value is returned. If no value is supplied, nil is returned.

##### Example

```

> (for ?item in (range 1 to 1000000)

(if (< ?item 123456)

(continue)

else

(break)))

.:  nil

> (for ?item in (range 1 to 1000000)

(if (< ?item 123456)

(continue)

else

(break foo)))

.:  foo

```

##### Related

break, fail, return, try

## convertible-p

True if the value can be converted to the datatype.

##### Syntax

(convertible-p _value taxon_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | The value to be converted |
| taxon | literal | 1   | The name of the target data type |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the value can be converted to the data type. |

##### Remarks

If the value can be converted converted to the given data type, then this function returns true, otherwise it returns false.

##### Example

```

> (convertible-p {a b c} string)

.:  true

> (convertible-p "500" number)

.:  true

> (convertible-p "500" literal)

.:  false

> (convertible-p "{wxy}" number)

.:  false

```

##### Related

datatype, datais, relation-p, type, is

## copy

Copies a sequence.

##### Syntax

(copy _sequence count_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| count | integer | 0-1 | The number of times to repeat the sequence. Default is 1. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The copied sequence. |

##### Remarks

A shallow copy of the original sequence is made and replicated. All elements of the sequence are repeated the specified number of times.

##### Example

```

> (copy "a" 5)

.:  "aaaaa"

> (copy {the quick brown fox} 3)

.:  {the quick brown fox the quick brown fox the quick brown fox}

> (copy "hello")

.:  "hello"

> (copy ($ hello world \\s) 2)

.:  "hello world hello world"

```

##### Related

copy, new, relation

## copyright

Displays copyright information.

##### Syntax

(copyright)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| nil | The value nil. |

##### Remarks

Prints copyright information.

##### Example

```

> (copyright)

(c)2014-2020 Michael S P Miller All Rights Reserved

.:  nil

```

##### Related

bye, help, license

## correlate

Finds the correlation coefficient of two lists.

##### Syntax

(correlate _list<sub>1</sub> list<sub>2</sub>_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| list | list | 2   | Lists. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The correlation coefficient. |

##### Remarks

Compares only the number of elements in the shorter of the two lists.

##### Example

```

(correlate {1 2 3 4 5} {4 3 2 1 0})

.:  -1

(correlate {1 2 3 4 5} {6 7 8 9 10})

.:  1

(correlate {1 2 3 4 5} {6 3 8 2 10})

.:  0.33071891

```

##### Related

probability, statistics, survey

## cosecant

Returns the cosecant.

##### Syntax

(cosecant _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The cosecant of the number. |

##### Remarks

##### Example

```

> (cosecant 0.785398)

.:  1.414213793

> (cosecant cir 0.785398 radians)

.:  1.414213793

> (cosecant cir 45 degrees)

.:  1.4142135623

> (cosecant hyp 1.5708 radians)

.:  0.434535467

> (cosecant hyp 90 degrees)

.:  0.434537208

```

##### Related

asecant, secant

## cosine

Returns the cosine.

##### Syntax

(cosine _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The cosine of the number. |

##### Remarks

None.

##### Example

```

> (cosine 0.785398)

.:  0.707106896

> (cosine cir 0.785398 radians)

.:  0.707106896

> (cosine cir 45 degrees)

.:  0.707106896

> (cosine hyp 1.5708 radians)

.:  2.50918693

> (cosine hyp 90 degrees)

.:  2.509178478

```

##### Related

asine, sine

## cotangent

Returns the cotangent.

##### Syntax

(cotangent _number geometry metrum_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The cotangent of the number. |

##### Remarks

##### Example

```

> (cotangent 0)

.:  infinity

> (cotangent cir 1.5708 radians)

.:  0

> (cotangent cir 45 degrees)

.:  1

> (cotangent hyp 1.5708 radians)

.:  1.09033

> (cotangent hyp 90 degrees)

.:  1.0903314107

```

##### Related

atangent, tangent

## count

Counts the iterations and returns the last expression.

##### Syntax

(count _symbol_ _…_ _binding_ _sequence_ as _counter expression_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A sequence (string or list) |
| as | literal | 1   | The literal as |
| counter | symbol | 1   | A counter symbol |
| expression | expression | 0+  | An expression. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last expression in the sequence. |

##### Remarks

None.

##### Example

```

> (count ?word in {the quick brown fox} as ?n

(tell user ($ ?n ?word \\n)) ?n)

1 the

2 quick

3 brown

4 fox

.:  4

```

##### Related

collect, exactly, filter, gather, quantify, quantity

## critical

Serializes evaluations across regions of code.

##### Syntax

(critical _locks option_ _…_ _expression_ _…_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| locks | list | 0-1 | A list of literals representing critical section locks |
| option | expression | 0+  | A key value pair:<br><br>retries _integer_ - number of times to retry any lock.<br><br>(default is 0)<br><br>lockwait _time_ - how long to wait for a lock.  <br>(default is 2,000,000 ticks)<br><br>within _time_ - the overall time to obtain all locks  <br>(default is1 second) |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The value of the last expression. |

##### Remarks

The critical section is used to serialize the execution of the contained expressions. Any other sections with the same tags shall be blocked. Generates failure if the locks cannot be obtained on the tags under the default or indicated conditions, or if a lock was forcibly released during execution.

##### Example

```

> (function sayHello {}

(critical {printing}

(for ?c in "hello " (tell user ?c))))

.:  sayHello

> (free (wait (concurrent (sayHello) (sayHello) (sayHello))))  


hello hello hello .: freed

```

##### Related

release

## cut

Removes elements from assortments by key.

##### Syntax

(cut _assortment key_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment. |
| key | variant | 0+  | A key. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The modified assortment or sequence. |

##### Remarks

Assortments are modified destructively. To delete nondestructively use the remove function.

##### Example

```

> (entries (collection a b c d))

.:  {{a a} {b b} {c c} {d d}}

> (entries (cut (lexicon a 1 b 2 c 3 d 4) b d))

.:  {{a 1}{c 3}}

```

##### Related

rip, remove

## data

Creates a data url.

##### Syntax

(data _option_ _…_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 1+  | Any key value pair of the following:<br><br>connect _string_ - use the specified connection string.<br><br>poolsize _poolsize_ \- maximum # of connections<br><br>provider _platform_ - either mssql, odbc, maria, pgsql<br><br>or build the connection string from the following elements.<br><br>driver _name_ - the driver<br><br>server _address_ - server address<br><br>version _number_ - server version<br><br>class _class_ - class name of driver<br><br>host _address_ \- host address<br><br>port _port_ \- server port for database service<br><br>instance _instance_ \- server instance name<br><br>integratedSecurity _truth_ \- true or false<br><br>database _name_ - database name<br><br>user _username_ - user name<br><br>password _password_ - user password<br><br>trusted _yesorno_ - trusted connection yes or no.<br><br>source _name_ - data source name<br><br>protocol _protocol_ - database protocol<br><br>subprotocol _subprotocol_ - database sub protocol<br><br>subname _subname_ - sub name |

##### Results

| Data Type | Description |
| --- | --- |
| url | A data url. |

##### Remarks

None

##### Example

```

> (open (data driver sqlserver server "//servername" port 1433

database mydata user "myUid" password "123456"))

.:  Data-1

> (ask Data-1 "select top 2 empid, name, salary from employee"

format row columns {name wage})

.:  {{1 "John Smith" 10.50}{2 "Jane Johnson" 12.00} }

> (close Data-1)

.:  Data-1

> (open (data host "localhost" database "sample" user "username"

password "secret" connections 3)))

.:  Data-2

> (tell Data-2 "update employee set wage = wage + 1.00;")

.:  executed

> (close Data-2)

.:  Data-2

> (global ?data

(open (data class "com.microsoft.jdbc.sqlserver.SQLServerDriver"

subprotocol "sqlserver"

subname "//serverName:port;database=db;user=uid;password=pwd")))

.:  true

> (function valueslist {?rows}

($ (inside (infix (map (collect ?row in ?rows (inside (infix ?row ,)))

call)

, ))))

.:  valuelist

> (tell ?data ($ "insert Employee (name, hours, wage) values "

(valueslist {{"Jane Johnson" 40 10.50}

{"John Smith" 5 10.50}})))

.:  2

> (close ?data)

.:  Data-3

```

##### Related

disconnect, tell, fetch, store

## date

Creates a new date or returns the current date.

##### Syntax

(date _yr mth day hrs mins secs zone zmins_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| yr  | integer | 0-1 | Four digits: The year (e.g., 2018, 2024) |
| mth | integer | 0-1 | A number between 1 and 12 |
| day | integer | 0-1 | A number between 1 and 31 |
| hrs | integer | 0-1 | A number between 0 and 23 |
| mins | integer | 0-1 | A number between 0 and 59 |
| secs | real | 0-1 | A real number between 0 and 59 |
| zone | integer | 0-1 | A number between -12 and 12. |
| zmins | integer | 0-1 | A number between -12 and 12. |

##### Results

| Data Type | Description |
| --- | --- |
| date | The UTC date. |

##### Remarks

If no arguments are provided, this function returns the current date in Coordinated Universal Time. Otherwise, it attempts to construct a date from the supplied arguments.

##### Example

```

> (date)

.:  \\@d2014-09-16T02:15:51.97152+00:00

> (date 2018 5 18 0 0 0 0 0)

.:  \\@d2018-05-18T00:00:00.00000+00:00

```

##### Related

epoch, moment, tick

## declared-p

True if a symbol exists in an environment.

##### Syntax

(declared-p _symbol environment_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol |
| environment | environment | 0-1 | An environment. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the symbol has been declared. |

##### Remarks

If location is omitted, the symbol is sought in the current environment.

##### Example

```

> (extend Example

(modular ?hello World))

.:  bar

> (declared-p ?User.hello)

.:  false

> (declared-p ?Example.hello)

.:  true

```

##### Related

function-p, symbol-p,

## decode

Decodes a string.

##### Syntax

(decode _source format_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| source | string | 1   | A string to decode. |
| format | literal | 1   | One of { base16, base32, base64, utf8, none } |

##### Results

| Data Type | Description |
| --- | --- |
| string | The encoded string |

##### Remarks

Each entry in the elements list may be a literal or a list containing a literal and an index.

##### Example

```

> (encode "The quick brown fox" base16)

.:  "54686520717569636B2062726F776E20666F78"

> (encode "The quick brown fox" base64)

.:  "VGhlIHF1aWNrIGJyb3duIGZveA=="

> (encode "The quick brown fox" none)

.:  "The quick brown fox"

> (decode "54686520717569636B2062726F776E20666F78" base16)

.:  "The quick brown fox"

> (decode "VGhlIHF1aWNrIGJyb3duIGZveA==" base64)

.:  "The quick brown fox"

> (decode "The quick brown fox" none)

.:  "The quick brown fox"

```

##### Related

encode

## default

Returns the first non-nil value.

##### Syntax

(default _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value to be returned. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The first value that is not nil. |

##### Remarks

Returns the first value which is not nil. If all values are nil, then nil is returned.

##### Example

```

> (default nil 1 2 3)

.:  1

> (default nil a b c)

.:  a

> (default nil)

.:  nil

> (default nil nil nil nil 1)

.:  1

```

##### Related

any, is , no

## definitions

Retrieves literal value pairs in an environment.

##### Syntax

(definitions _environment_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| environment | environment | 1   | An environment |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of all symbol value pairs |

##### Remarks

Returns a list containing all literal value pairs.

##### Example

```

> (using User

(definitions (scope)))

.:  {}

> (extend User

(function foo {} hello)

(function bar {} world))

.:  User

> (using User

(definitions (scope)))

.:  {{foo "(function foo {} hello)"}

{bar "(function bar {} world)"}}

```

##### Related

variables

## defunct

Undefines a function in a module.

##### Syntax

(defunct _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 1   | A fully qualified function name. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function. |

##### Remarks

Undefines a function or causes a failure if the function does not exist. Returns the name of the function if successful. Looks for the function in the current module if module is omitted.

##### Example

```

> (function foo bar)

.:  foo

> (describe foo)

.:  {"(function User.foo {} bar)"}

> (defunct foo)

.:  foo

> (describe foo)

.:  nil

```

##### Related

defined, describe, function, macro, nix, relation

## degrees

Converts radians into degrees.

##### Syntax

(degrees _radians_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| radians | real | 1   | a number in radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The number of degrees. |

##### Remarks

The radians are multiplied by 180 / π, or roughly 57.29578049044297, for the conversion.

##### Example

```

> (round (degrees (\* (/ 4 9) (pi))))

.:  80

> (round (degrees 1.4))

.:  80

> (round (degrees 0.7864815))

.:  45

```

##### Related

cosine, radians, sine, tangent

## delete

Modifies a sequence by deleting values.

##### Syntax

(delete _sequence value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| value | variant | 0+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The modified assortment |

##### Remarks

Destructively modifies a sequence by deleting the values. To create a new sequence with values omitted use the omit function.

##### Example

```

> (delete {a b c d e f g} a b)

.:  {c d e f g}

> (delete {a 1 nil b 2 c 3 nil nil d nil 4} nil)

.:  {a 1 b 2 c 3 d 4}

```

##### Related

pop, push,

## dependencies

Returns a module's dependencies.

##### Syntax

(dependencies _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | A module |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of modules upon which the argument depends. |

##### Remarks

Returns dependencies of a module.

##### Example

```

> (module a

(function foo bar))

.:  a

> (module b

(function bar baz))

.:  b

> (module c

(require a)

(require b)

(function baz {}

{(foo) (bar)}))

.:  c

> (dependencies c)

.:  {a b}

```

##### Related

discard, extend, forgo, module, require, grok, using

## deq

Removes an element from an embedded sequence.

##### Syntax

(deq _container place option_)

_option ::=_ all _value_

_option ::=_ at _position_

_option ::=_ the _value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |
| place | variant | 1   | A key or position. |
| option | expression | 0-1 | One of<br><br>all value - Removes all occurrences of the value.<br><br>at position - A number or the literal #. Default is 1.  <br>the value - Removes the first occurrence of the value. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the container. |

##### Remarks

If no options are provided, the last item of the sequence is removed.

##### Example

```

> (deq (lexicon 1 {a a b} 2 {d e f}) 2)

.:  Lexicon-1

> (get Lexicon-1 2)

.:  {d e}

> (get (deq Lexicon-1 1 all a) 1)

.:  {b}

```

##### Related

add, cut, enq, get, has, key, keys, peek, put, values

## describe

Returns descriptions of a literal.

##### Syntax

(describe _literal_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| literal | literal | 1   | A function, module, relation, or other defined item. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A possibly empty list of descriptions. |

##### Remarks

Returns a list of string descriptions.

##### Example

```

> (describe foo)

.:  {}

> (relation Foo :Bar :Baz)

.:  Foo

> (function foo {} bar)

.:  foo

> (describe foo)

.:  {"(function User.foo {} bar)" "(relation Foo :Bar nil :Baz nil)"}

```

##### Related

defined, defunct, function, macro, nix, relation

## detach

Unregisters a knowledge base.

##### Syntax

(detach _knowledge_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base. |

##### Results

| Data Type | Description |
| --- | --- |
| knowledge | The knowledge base. |

##### Remarks

Unregisters an attached knowledge base.

##### Example

```

> (var ?kb (knowledge url "file://c:/premise/kb/esoteric.mdb"))

.:  Knowledge-1

> (attach ?kb)

.:  Knowledge-1

> (use ?kb)

.:  Knowledge-1

> (relation Fact :All :Are)

.:  Fact

> (detach ?kb)

.:  Knowledge-1

> (free (cede (reference ?kb)))

.:  freed

```

##### Related

attach, conceive, each, eradicate, knowledge, knowing, get, put, using, which, with

## difference

Returns the difference of two sequences.

##### Syntax

(difference _sequence<sub>1</sub> sequence<sub>2</sub> operation_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2   | A list or string |
| operation | literal | 0-1 | One of :<br><br>set - returns the set difference. (default)<br><br>sym - returns symmetric difference |

##### Results

| Data Type | Description |
| --- | --- |
| list | Set difference of sequence1 and sequence2 |

##### Remarks

If the operation is set, this function returns a sequence containing elements from the first sequence not in the second. If the operation is symmetric, it returns items that are not in the intersection of the provided sequences. Sequences must be of the same data type, e.g., either all lists or all strings.

##### Example

```

> (difference "abcd" "abef" set)

.:  "cd"

> (difference {1 2 3 4} {2 3 4 5} sym)

.:  {1 5}

> (difference {1 2 3} {5 4 3 2})

.:  {1}

```

##### Related

common, intersection, union

## did

Evaluates an expression and surpresses failures.

##### Syntax

(did _expression_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | An expression to evaluate. |

##### Results

| Data Type | Description |
| --- | --- |
| expression | Returns a truth success value, the result , and a possible failure |

##### Remarks

If the expression fails, success shall be false, the result shall be nil, and the failure shall contain the generated failure.

##### Example

```

> (did (string x))

.:  true "x" nil

> (did (integer x))

.:  false nil \[Failure :Name TypeConversion :Text "Cannot convert x to Integer."\]

> (bind ?success ?result ?error (did (string "hello world")))

.:  true

> ?success ?result ?error

.:  true "hello world" nil

```

##### Related

assert, can, ensure, fail, finally, may, try

## digit

Returns the digit in the specified position of a number.

##### Syntax

(digit _number position_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |
| position | number | 1   | The position of the digit within the number |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The indicated digit (a number between 0 an 9) or nil. |

##### Remarks

Returns the digit in the position of the fractional normed significand (0.nnnnn) of a number. If the position is out of range, nil is returned.

##### Example

```

> (digit 500 1)

.:  5

> (digit 500 2)

.:  0

> (digit 500 3)

.:  0

> (digit 500 4)

.:  nil

> (digit (pi) 7)

.:  2

```

##### Related

digits, exponential, fractional, sign, significand,

## digit-p

True if the first position of a string is a digit.

##### Syntax

(digit-p _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A variant. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the first position is a digit. |

##### Remarks

None

##### Example

```

> (digit-p "The Quick BROWN fox")

.:  false

> (digit-p "100")

.:  true

> (digit-p foo)

.:  false

> (digit-p 100)

.:  false

```

##### Related

alphabetic-p, alphanumeric-p, capitalized-p, lowercase-p, uppercase-p

## digits

Returns the digits comprising a number.

##### Syntax

(digits _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |

##### Results

| Data Type | Description |
| --- | --- |
| string | The digits. |

##### Remarks

Returns the fractional digits in the normed significand (0.nnnnn) of a number as a string. Trailing zeros are deleted while leading fractional zeros are preserved.

##### Example

```

> (digits 500)

.:  "500"

> (digits 0.00465)

.:  "00465"

> (digits -1050.064)

.:  "1050064"

> (digits -2302.023900)

.:  "23020239"

> (digits 000.003500)

.:  "0035"

```

##### Related

digit, exponential, fractional, sign, significand

## dimensions

Returns the lengths of each dimension in a sequence.

##### Syntax

(dimensions _sequence_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Data Type | Description |
| --- | --- |
| list | The length of each dimension in a sequence. |

##### Remarks

This function returns the length of each nested sequence as a list. The function assumes that the entire sequence has a uniform number of elements in each dimension.

##### Example

```

> (dimensions {{{a}{b}{c}}{{d}{e}{f}}})

.:  {2 3 1}

> (dimensions {a b c d})

.:  {4}

> (dimensions {{a b c}{d e f}})

.:  {2 3}

> (dimensions "abc")

.:  {3}

```

##### Related

array

## discard

Discards a module.

##### Syntax

(discard _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | A module |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The literal discarded |

##### Remarks

Removes an unwrapped module from the modules collection if no functions are defined in the module, causes a failure otherwise.

##### Example

```

> (module module1

(function foo {} bar))

.:  module1

> (for ?fn in (functions module1)

(defunct (qualified module1 ?fn)))

.:  nil

> (discard module1)

.:  discarded

```

##### Related

dependencies, discard, extend, forgo, module, require, grok, use

## disjoint-p

True if no elements are common among sequences.

##### Syntax

(disjoint-p _sequence_ _sequence_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | A sequence |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if no elements are common to any sequences. |

##### Remarks

Returns true if, for the provided sequences, no elements are common to any sequences.

##### Example

```

> (disjoint-p {1 2 3 4}{2 3 4 5)

.:  false

> (disjoint-p {2 3 4 5}{1 6 7 8})

.:  true

> (disjoint-p {1 2 3 4}{2 3 4 5}{3 4 5 6}{4 5 6 7})

.:  false

> (disjoint-p "abc" "def" "ghi")

.:  true

```

##### Related

intersects-p, subset-p

## distinct

Creates a new sequence without duplicate elements.

##### Syntax

(distinct _sequence_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A new sequence with duplicates removed |

##### Remarks

Creates a new sequence containing unique items.

##### Example

```

> (distinct {1 2 2 2 3 4 2 3 4 5})

.:  {1 2 3 4 5}

> (distinct "abcbcdcde")

.:  "abcde"

```

##### Related

difference, intersection, union

## distribute

Applies a function in parallel to a sequence.

##### Syntax

(distribute _sequence function result_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | list | 1   | A list containing the arguments to each function. |
| function | function | 1   | The function to be distributed and processed in parallel. |
| result | literal | 0-1 | The literal tasks or values (default). |

##### Results

| Data Type | Description |
| --- | --- |
| list | If tasks is specified, a list of tasks is returned immediately, otherwise a list of values are returned upon completion of all the tasks. |

##### Remarks

Returns a list of tasks for each element of the sequence by applying the function to each elment.

##### Example

```

> (distribute {5 6 7} (given {?x} (\* ?x 2)))

.:  {10 12 14}

> (distribute {5 6 7} (given {?x} (\* ?x 2)) tasks)

.:  {task-1 task-2 task-3}

> (map {task-1 task-2 task-3} await)

.:  {10 12 14}

> (distribute {2 3 4} (given {?x} (morph {?x} {++ ++ ++})) values)

.:  {5 6 7}

```

##### Related

apply, concurrent, complete, compose,map, mete, morph, scatter

## divide

Safe division.

##### Syntax

(divide _dividend_ _divisor default_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number.or a list. |
| divisor | variant | 1   | A number.or a list. |
| default | variant | 0-1 | A number or a list. If not supplied, unknown is returned. |

##### Results

| Data Type | Description |
| --- | --- |
| number | Returns the quotient of the numerator and denominators or the default. |

##### Remarks

Returns the quotient of the values or the default. It divides the dividend by the divisor. If the default is not supplied, unknown is returned. All list arguments must be the same length. If an argument is a list, then each element of the list is divided. If a scalar and a list are divided, then the scalar is divided by each element of the list.

##### Example

```

> (divide 1.0 2)

.:  0.5

> (divide 5 0 0)

.:  0

> {divide {4 5 6} 0)

.:  {undefined undefined undefined}

> {divide {4 5 6} {1 2 0} -1)

.:  {4 2.5 -1}

```

##### Related

/ division, \* multiplication, + addition, - subtraction, % modulo , // nth root

## divisible-p

True if the divisor evenly divides the dividend.

##### Syntax

(divisible-p _dividend divisor_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| dividend | number | 1   | The value to be divided |
| divisor | number | 1   | The value to divide by |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the modulus of the dividend and divisor equals zero. |

##### Remarks

Causes a failure if the arguments are not numbers, or if the arguments cannot be converted to the same type for comparison (for example, an imaginary compared to an integer).

##### Example

```

> (divisible-p 501 10)

.:  false

> (divisible-p 500 10)

.:  true

> (divisible-p 28 7)

.:  true

```

##### Related

datatype, type, is

## do

Evaluates expressions and handles escapes.

##### Syntax

(do _expression_ _…_ resume _tag_ _recovery_ _…_ finally _cleanup_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1+  | Expressions to do some processing |
| resume | literal | 1   | The literal resume |
| tag | literal | 0-1 | A literal location name (often here) |
| resumption | expression | 0+  | Expressions for resuming after the escape |
| finally | literal | 0-1 | The literal finally |
| cleanup | expression | 0+  | Expressions to do some clean up |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the value of the last executed expression. |

##### Remarks

The do special form performs escape handling. The escape function shall return to the resume tag and check if the location matches the intended location of the escape. If the location is correct, the do will resume, otherwise it will throw to an encompassing resume. If no location is provided, it will simply resume at the encompassing do form.

##### Example

```

> (do foo)

.:  foo

> (do foo bar baz)

.:  baz

> (do (step ?x from 1 to 500 nothing)

(step ?y from 501 to 1000 nothing)

(step ?z from 1000 to 2000 nothing)

done)

.:  done

(function main {& ?args}

(tell user ($ \\n Attempting dangerous operation... \\n))

(do

(do

(tell user "Escaping...")

(escape outer)

(tell user ($ \\n Never gonna happen!! \\n))

resume here

(tell user ($ \\n Wrong Location.)))

resume outer

(tell user ($ \\n Resumed.))

finally

(tell user ($ \\n Goodbye \\n))

)

)

.:  main

> (main)

Escaping...

Resumed.

Goodbye

.:  told

```

##### Related

wait, abort,, await, complete, done-p, reclaim, use, for, iterate, loop, step, task, try, until, while

## done

Terminates a generator.

##### Syntax

(done)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| escape | Returns an escape. |

##### Remarks

None.

##### Example

```

> (generator myGenerator {?interrupt}

(yield 1)

(yield 2)

(if ?interrupt (done))

(yield 3)

(yield 4)

(done))

.:  myGenerator

> (collect ?x in (myGenerator true) ?x)

.:  {1 2}

> (collect ?x in (myGenerator false) ?x)

.:  {1 2 3 4}

```

##### Related

generator, generator-p, yield

## drop

Removes a relation index.

##### Syntax

(drop _index_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| index | index | 1+  | A relation index or list of indicies |

##### Results

| Data Type | Description |
| --- | --- |
| expression | The literal dropped and the number of indices dropped. |

##### Remarks

Removes an index from a relation if one exists, otherwise causes a failure.

##### Example

```

> (relation Car :Make :Model :Year)

.:  Car

> (index Car :Make :Model)

.:  Car_Index_1

> (index Car :Year)

.:  Car_Index_2

> (drop Car_Index_1)

.:  dropped 1

> (drop Car_Index_2)

.:  dropped 1

```

##### Related

relation, index, indices

## duplicate

Duplicates a file or contents of a folder.

##### Syntax

(duplicate _source target option_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| source | url | 1   | A source url. |
| target | url | 1   | A target url. |
| option | expression | 0-1 | A key value pair, one of<br><br>overwrite yes \| no – (default is no). |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The literal duplicated. |

##### Remarks

Duplicates files on a file system.

##### Example

```

> (let ?f (file name "foo.txt"))

.:  true

> (write ?f "The quick brown fox")

.:  File-1

> (close ?f)

.:  closed

> (duplicate (url ?f) (url path "bar.txt"))

.:  duplicated

> (duplicate (url ?f) (url path "baz.txt") overwrite yes)

.:  duplicated

```

##### Related

erase, move

## during-p

True if an interval occurs within a second interval.

##### Syntax

(during-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if interval1 occurs within interval2. |

##### Remarks

None.

##### Example

```

> (during-p \\@i{\\@s1 \\@s2} \\@i{\\@s3 \\@s4})

.:  false

> (during-p \\@i{\\@s1 \\@s5} \\@i{\\@s1 \\@s8})

.:  true

> (during-p \\@i{\\@s1 \\@s9} \\@i{\\@s4 \\@s6})

.:  false

> (during-p \\@i{\\@s4 \\@s6} \\@i{\\@s1 \\@s9})

.:  true

> (during-p \\@i{\\@s7 \\@s9} \\@i{\\@s3 \\@s8} \\@s1)

.:  true

```

##### Related

before-p, finishes-p, meets-p, overlaps-p, starts-p

## dynamic

Creates a dynamic environment for variables.

##### Syntax

(dynamic _assignments expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assignments | list | 1   | A list of symbol value pairs |
| expression | variant | 0+  | An expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates temporary global variables existing only for the duration of the scope.

##### Example

```

> (function appendToFile {& ?messages}

(dynamic {?file nil}

(try

(set ?file (file name "myfile.out"))

(seek ?file #)

(for ?s in ?messages (write ?file ?s))

(close ?file)

appended

learn ?f

?f))

)

.:  appendToFile

```

##### Related

<-- _before tie_, --> _after tie_, assume, assign, constant, global, local, modular

## e

Returns Euler's number, 2.718281828459045.

##### Syntax

(e)

##### Module

Math

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| real | Returns the constant 2.718281828459045 . |

##### Remarks

None.

##### Example

```

> (e)

.:  2.7182818284590451

```

##### Related

pi

## each

Combines for and with to iterate over sequences matching patterns to the knowledge base.

##### Syntax

(each _symbol_ _…_ _binding reversal_ _sequence_ _…_ _premises_ _option_ _…_ _action_ )

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= in

_binding_ ::= per

_binding_ ::= over

_binding_ ::= across

_reversal_ ::= across

_condition ::= slot_ _\=_ _value_

_condition ::= slot_ _/=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _unary-predicate_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

_option_ ::= scan _number_

_option_ ::= limit _number_

_option_ ::= group _slot_ _…_ by _slot_ _…_ into _symbol_

_option_ ::= merge _value_ _…_

_option_ ::= sort _ordering_ _…_

_action_ ::= deem _value1_ else _value2_

_action_ ::= do _expression_ _…_

_action_ ::= give _expression_

_action_ ::= list _value_ _…_

_action_ ::= tally

_action_ ::= yield _expression_

_ordering_ ::= _term comparator_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, over, or across. |
| reversal | literal | 0-1 | The literal reverse. |
| sequence | sequence | 1+  | A list or string |
| premises | expression | 1+  | O­ne or more premises |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |
| action | literal | 0-1 | Either deem, do, give, list, tally, yield. |
| expression | expression | 0+  | An expression |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value returned on the last iteration. |

##### Remarks

Variables and sequences are required for in, per, and over. If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If the binding across is specified, each symbol is bound to elements of the corresponding sequence (i.e, first symbol to the first sequence, second to the second, etc.). If there are insufficient elements to bind to the variables then the function fails. If the literal reverse is present, the sequence is traversed in reverse. On each iteration, all the premises are evaluated. Note that a predicate is a truth function, scan tells the number of matches to attempt (default is infinity), and limit tells how many results to return (default is infinity). If the action is deem, then the subsequent value is returned if the final descriptor is matched, otherwise the else value is returned. If the action is do, then for each match the expressions are run, and for the last match, the last value of the last expression is returned, or nil is returned if all descriptors were false or had no matches. If the action is give, then the expression is immediately returned from the each call on the first match, akin to return from each. If the action is yield, then the expression is immediately returned from the each call, but may be resumed with a next function call. When all matches are completed, the done function is implicitly called to terminate the generator. If the action is group, followed by a list of slots and values from which the group is picked, then the literal by and a set of slots and values that determines the grouping inclusion , and finally the literal into followed by a symbol to which the group shall be bound on each iteration. If the action is either list (or merge), then a (merged) list is returned or an empty list if nothing matched. If the action is sort then the list of slots and comparators should follow. (Note that list is required if the sort action is selected.) If the action is tally, then the number of matched premises is returned, or zero if no matches.

(each _symbol_ _…_ _binding reversal_ _sequence_ _…_ _premises_ _option_ _…_ _action expression_ _…_ ))

Is equivalent to  

(for _symbol_ _…_ _binding reversal_ _sequence_ _…_ (with _premises_ _option_ _…_ _action expression_ _…_ ))

The difference between for and each is that in a for expression, on every iteration, all the expressions following the sequence(s) are evaluated and the return value is the result of the last expression evaluated on the last iteration. In the each expression, the premises following the sequence(s) are evaluated, and if any premise is false, the next iteration occurs, otherwise, if all the premises are true, the action is taken, and the action expressions are evaluated.

##### Example

```

> (relation Sport

:Name

:PlayersPerTeam)

.:  Sport

> (relation Team

:Name

:Sport

:Players {})

.:  Team

> (relation Person

:Name

:Skills

:Teams {})

.:  Person

> (relation Skill

:Sport

:Level)

.:  Skill

> (repeat (random 1 to 10)

(let ?sport (new Sport :Name (unique "sport")

:PlayersPerTeam (random 1 to 12)))

(repeat (\* (random 1 to 10) 2) ; even number of teams

(let ?team (new Team :Name (unique "team") :Sport ?sport)))

Leagues)

.:  Leagues

> (so {?sports (which Sport)

?sportCount (# ?sports)

?teams (which Team)}

(do

(let ?abilities (pick ?sports (random 1 to ?sportCount))

?player (new Person :Name (unique "person")

:Skills (collect ?sport in ?abilities

(new Skill

:Sport ?sport

:Level (random 1 to 10)))))

(each ?sport in ?abilities

(let ?team (@ (sort (which ?teams :Sport = ?sport)

(given {?a ?b} (<= (# (:Players ?a))

(# (:Players ?b)))))))

do

(enq ?team :Players ?player)

(enq ?player :Teams ?team))

until (every ?team in ?teams

(>= (# (:Players ?team)) (# (:PlayersPerTeam (:Sport ?team))))))

Players)

.:  Players

> (collect ?sport in (which Sport)

{?sport (avg (which Skill :Sport = ?sport :Level as ?level list ?level))}))

.:  {{sport3 4.9} {sport1 7.898} {sport2 6.382} {sport4 8.452}}

```

##### Related

which, with

## encode

Encodes a string.

##### Syntax

(encode _source format_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| source | string | 1   | A string to encode. |
| format | literal | 1   | One of { base16, base64, utf8, utf16, none } |

##### Results

| Data Type | Description |
| --- | --- |
| string | The encoded string |

##### Remarks

Converts a string to the specified format.

##### Example

```

> (encode "The quick brown fox" base16)

.:  "54686520717569636B2062726F776E20666F78"

> (encode "The quick brown fox" base64)

.:  "VGhlIHF1aWNrIGJyb3duIGZveA=="

> (encode "The quick brown fox" none)

.:  "The quick brown fox"

> (decode "54686520717569636B2062726F776E20666F78" base16)

.:  "The quick brown fox"

> (decode "VGhlIHF1aWNrIGJyb3duIGZveA==" base64)

.:  "The quick brown fox"

> (decode "The quick brown fox" none)

.:  "The quick brown fox"

```

##### Related

decode

## enq

Inserts an element into an embedded sequence.

##### Syntax

(enq _container place entry_)

_entry ::=_ _position value_

_entry ::=_ unique _value_

_entry ::=_ _value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | assortment | 1   | An assortment or tuple |
| place | variant | 1   | A key or position. |
| entry | expression | 1   | Any of the following:<br><br>value - appends the value to the sequence.<br><br>position value - inserts the value at the position.<br><br>coordinate value - inserts the value in the list coordinate.<br><br>unique value - appends value if it is not already present. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The modified container. |

##### Remarks

If only a single value is provided for _entry_, then the value is appended to the sequence. If an integer position and value is provided, then the value is inserted at the position. If the keyword unique is provided, then the value is appended to the sequence if it does not already exist

##### Example

```

> (let ?a {{}{1 2 3}{}})

.:  true

> (enq ?a {2 2} 8)

.:  {{}{1 8 2 3}{}}

```

##### Related

add, cut, deq,get,has, key, keys, peek, put, values

## ensure

Performs type checking.

##### Syntax

(ensure c_heck_ _…_ )

_check_ ::= _kind value_

_check_ ::= _{kind_ _…_ _} value_

_kind_ ::= _taxon_

_kind_ ::= _meron_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| check | expression | 1+  | A datatype, prototype, or list containing datatypes and prototypes. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if all values correspond to their indicated types. |

##### Remarks

If any of the values do not correspond to their designated types, then the function fails; otherwise the function returns true.

##### Example

```

> (function multiply {?a ?b + ?c}

(ensure number ?a number ?b {number nil} ?c)

(\* ?a ?b (default ?c 1)))

.:  multiply

> (multiply 10 banana)

.:  \[Failure :Name InvalidArg :Text "Expected a number, encountered banana."\]

> (multiply 10 5)

.:  50

```

##### Related

assert, can, did, fail, may, try

## entries

Retrieves key value pairs for an assortment.

##### Syntax

(entries _assortment_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of all key value pairs |

##### Remarks

Returns a list containing key value pairs for an association.

##### Example

```

> (entries (lexicon a 1 b 2 c 3 d 4))

.:  {{a 1} {b 2} {c 3} {d 4}}

> (entries (structure Foo :X :Y :Z apple))

.:  {{relation Foo} {:X nil} {:Y nil} {:Z apple}}

```

##### Related

bindings, definitions, positions

## enum

Retrieves an enumerated assortment.

##### Syntax

(enum _name_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of a defined enumeration |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the enumeration |

##### Remarks

Each entry in the elements list may be a literal or a list containing a literal and a number. If a number is present, the number shall be assigned to the preceding literal as the index of that literal, and the next literal shall have an index of the number plus one, unless another index is present. For example, the arguments a, b 7, c: a shall be assigned the value 1, b shall be assigned the value 7, and c shall be assigned the value 8. An enumeration is an immutable assortment so it cannot be modified.

##### Example

```

> (enumeration MySimpleType a b 7 c)

.:  Enumeration-1

> (keys Enumeration-1)

.:  {a b c}

> (entries (enum MySimpleType))

.:  {{a 1}{b 7}{c 8}}

> (values (enum MySimpleType))

.:  {1 7 8}

```

##### Related

add, cut, elem, enumerations, elems, entries, size

## enumeration

Defines an enumerated assortment.

##### Syntax

(enumeration _name element_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of an enumeration |
| element | expression | 1+  | A literal or literal number pair. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the enumeration |

##### Remarks

Each entry in the elements list may be a literal or a list containing a literal and a number. If a number is present, the number shall be assigned to the preceding literal as the index of that literal, and the next literal shall have an index of the number plus one, unless another index is present. For example, the arguments a, b 7, c: a shall be assigned the value 1, b shall be assigned the value 7, and c shall be assigned the value 8. An enumeration is an immutable assortment so it cannot be modified.

##### Example

```

> (enumeration MySimpleType a b 7 c)

.:  Enumeration-1

> (keys Enumeration-1)

.:  {a b c}

> (entries Enumeration-1)

.:  {{a 1}{b 7}{c 8}}

> (values Enumeration-1)

.:  {1 7 8}

```

##### Related

add, cut, elem, enum, enumerations, elems, entries, size

## enumerations

Returns a list of all enumerations.

##### Syntax

(enumerations)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list of enumerations. |

##### Remarks

None.

##### Example

```

> (enumerations)

.:  {}

> (enumeration MySimpleType {a b c})

.:  MySimpleType

> (enumerations)

.:  {MySimpleType}

```

##### Related

enumeration

## environment

Creates a new context for variables and functions.

##### Syntax

(environment _parent entry_ _…_ )

_entry_ ::= _symbol_ _value_

_entry_ ::= _function definition_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| parent | environment | 0-1 | An environment or the value nil. |
| entry | expression | 0+  | A symbol and value pair or function and definition pair. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | A resource to the environment |

##### Remarks

Entries with literal keys are retrieved via the definitions function, while entries with symbol keys are retrieved with the bindings function. All entries may be retrieved using the entries function.

##### Example

```

> (environment nil (symbol A) "hello world")

.:  Environment-1

> (add Environment-1 foo (given {?x}(+ ?x 1)))

.:  Environment-1

> (add Environment-1 bar (function bar {?x} (\* ?x 2)))

.:  Environment-1

> (entries Environment-1)

.:  {{?A "hello world"} {foo (given {?x}(+ ?x 1))} {bar (fn bar {?x} (\* ?x 2))}}

```

##### Related

@, add, includes, cut, entries, environment-p, keys, reclaim, #, values

## epoch

Returns a Unix epoch or the current epoch.

##### Syntax

(epoch _time_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| time | time | 0-1 | A date, moment, seconds or tick value. |

##### Results

| Data Type | Description |
| --- | --- |
| epoch | The Unix time in seconds since January 1, 1970 (UTC). |

##### Remarks

Converts the supplied time to a Unix epoch.

##### Example

```

> (epoch 2014-11-29T23:39:29.741)

.:  \\@e1417333169

> (epoch \\@m2014939313515537)

.:  \\@e1481565910

> (epoch \\@t63573798191026000)

.:  \\@e1481565910

> (epoch (date))

.:  \\@e1533235279

> (epoch)

.:  \\@e1533235284

> (epoch (tick))

.:  \\@e1533235295

```

##### Related

date, moment, tick

## eradicate

Deletes a knowledge base.

##### Syntax

(eradicate _knowledege_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base |

##### Results

| Data Type | Description |
| --- | --- |
| knowledge | The opened knowledge base. |

##### Remarks

Deletes an existing knowledge base.

##### Example

```

> (conceive (var ?kb (knowledge name defaultKB path "c://premise/kb/")))

.:  defaultKB

> (attach ?kb)

.:  defaultKB

> (relation Fact :All :Are)

.:  Fact

> (detach ?kb)

.:  defaultKB

> (eradicate ?kb)

.:  defaultKB

> (free (cede (reference ?kb)))

.:  freed

```

##### Related

attach, conceive, detach,each, get, knowledge, knowing, put, using, which, with

## erase

Deletes files or folders.

##### Syntax

(erase _file option_ _…_ )

_option_ ::= _key value_

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| file | file | 1   | A file resource. |
| option | expression | 0-1 | Key value pairs where a key is one of<br><br>force yes\|no - forcibly erase the file. Default is no.<br><br>type {file or folder} - what to erase. Default is file. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The literal erased. |

##### Remarks

This function attempts to delete a file. If successful it returns erased, otherwise it causes a failure.

##### Example

```

> (let ?path (file path (path "quick.txt")))

.:  true

> (erase ?path force yes)

.:  erased

> (erase (url scheme folder path (folder "c:/foo")) type folder)

.:  erased

```

##### Related

close, file-p, files, folders, file, read, seek, write

## escape

Escapes to the next resume location in the call graph, matching the location if provided.

##### Syntax

(escape _tag_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| tag | literal | 0-1 | A location name. |

##### Results

| Data Type | Description |
| --- | --- |
| Failure | A failure. |

##### Remarks

Returns control to superordinate do .. resume special form. If a tag is provided, it will compare the tag and throw again if the tag does not match.

##### Example

```

> (do

(do

(escape proceed)

(try

(signal \[Failure :Name User :Text "A big problem"\])

learn ?e

(tell user ($ Learned ?e \\n))

(tell user ($ Rethrowing... \\n)))

resume

(tell user ($ This is ignored)))

resume proceed

(tell user ($ Resuming \\n))

finally

done)

Resuming

.:  done

```

##### Related

confirm, confute, ensure, fail, signal, try

## eval

Evaluates an expression.

##### Syntax

(eval _expression environment_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1   | An expression to be evaluated |
| environment | environment | 0-1 | An environment |

##### Results

| Data Type | Description |
| --- | --- |
| value | The result of evaluating the expression |

##### Remarks

Evaluates the expression and returns the resulting value. If no environment is provided, the current scope is used. The environment parameter is always evaluated in the current scope while the expression is evaluated in the provided scope, or the current scope if argument 2 is omitted.

##### Example

```

> (eval (+ 1 2 3 4))

.:  10

> (' (+ 1 2 3 4))

.:  (+ 1 2 3 4)

> (eval (' (' (+ 1 2 3 4))) (scope))

.:  (+ 1 2 3 4)

> (eval (eval (' (' (+ 1 2 3 4))))

.:  10

```

##### Related

' _quote_, _\`_ _expand_, apply, call, invoke

## even-p

True if the number is even.

##### Syntax

(even-p _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the number is even. |

##### Remarks

None.

##### Example

```

> (even-p 500)

.:  true

> (even-p 0)

.:  true

> (even-p -23)

.:  false

```

##### Related

odd-p, negative-p, positive-p, zero-p

## every

True if a predicate is true for every element in a sequence.

##### Syntax

(every _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if every element satisfies the predicate, else false. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example

```

> (every ?n in {1 2 3 4} (= number (taxon ?n)))

.:  true

> (every ?m ?n per {{1 2} {3 4}} (< ?m ?n))

.:  true

> (every ?m ?n over {4 3 2 1} (divisible-p ?m ?n))

.:  false

```

##### Related

few, most, nevery, none, some

## exactly

True if a number of elements satisfy a clause.

##### Syntax

(exactly _quantity_ of _sequence_ _clause_ within _margin_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| quantity | number | 1   | A number |
| of  | literal | 1   | The literal of |
| sequence | sequence | 1   | A sequence |
| clause | expression | 1   | A key value pair. One of<br><br>is _value_ - a sequence element,<br><br>are _value_ - a sequence element,<br><br>satisfies _predicate_ - a unary truth function.<br><br>satisfy _predicate_ - a unary truth function. |
| within | literal | 0-1 | The literal within |
| margin | number | 0-1 | A number. (default is zero). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if exactly quantity elements satisfies the predicate |

##### Remarks

The predicate must return true or false.

##### Example

```

(exactly 4 of {1 2 3 4} satisfies number-p)

.:  true

(exactly 1 of {1 a 3 4} is a)

.:  true

(exactly 3 of {1 2 3 4} satisfy odd-p within 1)

.:  true

```

##### Related

\= _equal_,

## exchange

Creates a new a sequence with values swapped.

##### Syntax

(exchange _sequence substitution_ _…_ )

_substitution_ ::= _prior-position later-position_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or a string. |
| substitution | expression | 1+  | A prior and later position pair.  <br>A position may be a number or a list of numbers.. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The modified sequence |

##### Remarks

Returns a copy of the original sequence with substitutions made. For destructive modification of a sequence use the swap function.

##### Example

```

> (exchange {A B C} 1 3)

.: {C B A}

> (exchange "ABCD" 1 3)

.: 'CBAD'

> (exchange {{1 2 3}{4 5 6}} {2 1} {1 3})

.:  {{1 2 4}{3 5 7}}

```

##### Related

@ _element_, append, fix, push, pop, swap

## excludes

True if a sequence does not contain an element.

##### Syntax

(excludes _sequence element option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| element | variant | 1   | A value |
| option | expression | 0-2 | A key value pair. Any of<br><br>depth _number_ \- Number or # (for any depth). Default is 1.<br><br>transform _function_ \- A function to transform the element.. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the element is not in the sequence. |

##### Remarks

If the element and sequence are strings, then a string search is performed.

##### Example

```

> (excludes {a b c d e f g} x)

.:  true

> (excludes "cbazyx" "a")

.:  false

```

##### Related

includes, excludes, in, occurences, out, pick, position

## exists-p

True if a value is a thing.

##### Syntax

(exists-p _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the values is a thing. |

##### Remarks

None.

##### Example

```

> (exists-p yes)

.:  true

> (exists-p nil)

.:  false

> (exists-p (nothing))

.:  false

> (exists-p 3.1415926)

.:  true

```

##### Related

null-p

## exit

Explicitly ends a task using a return value.

##### Syntax

(exit _value_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | A return value. Defaults to nil if not specified. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The argument value |

##### Remarks

Forcibly ends a task. Calling exit from the interpreter shall not exit the interpreter. The bye function must be called to exit the interpreter.

##### Example

```

> (concurrent (step ?x from 1 to 999999999

(if (> ?x 1000000) (exit exited)))) ;

.:  {Task-343}

> (await task-343)

.:  exited

> (free task-343)

.:  freed

> (exit done)

.:  done

```

##### Related

wait, abort, await, complete, do, task

## exponential

Returns the base ten exponent of a number.

##### Syntax

(exponential _number significand_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |
| significand | literal | 0-1 | One of normed, scientific, integer. Default is scientific. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The exponent. |

##### Remarks

The normed significand represents the number as a fraction (0.nnnn). The scientific significand represents the number as a decimal between 1.0 and 10.0 (n.nnnn). The integer significand represents the number as an integer (nnnn). The exponential represents the power of 10 to which the significand must be raised to accurately reflect the number.

##### Example

```

> (exponential 500)

.:  2

> (exponential 0)

.:  1

> (exponential -1000 normed)

.:  4

> (exponential -2302.023900 integer)

.:  -4

> (exponential 0.003500 scientific)

.: -3

```

##### Related

digit, digits, fractional, sign, significand,

## expression

Creates an expression.

##### Syntax

(expression _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | Any value |

##### Results

| Data Type | Description |
| --- | --- |
| expression | Returns a expression containing the values. |

##### Remarks

Expressions are lists without delimiters. An empty expression has no printed representation.

##### Example

```

> (expression a b c {d})

.:  a b c {d}

> (expression "a b c")

.:  "a b c"

> (let ?a 1 ?b 2)

.:  true

> (bind ?a ?b (expression ?b ?a))

.:  true

> ?a ?b

.:  2 1

> (void-p (expression))

.:  true

```

##### Related

inside, is, void-p  

## extend

Adds new definitions to a module.

##### Syntax

(extend _module_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | The module containing the extended definitions |
| expression | expression | 0+  | An expression. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The module literal. |

##### Remarks

Allows new definitions to occur in the target module. The module must be unwrapped.

##### Example

```

> (use User)

.:  User

> (extend MyModule (function foo {} 100))

.:  MyModule

> (MyModule.foo)

.:  100

```

##### Related

dependencies, discard, forgo, module, modules, require, grok, use

## facility

Creates a private function in a module.

##### Syntax

(facility _name parameters expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| expression | variant | 0+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Facilities are module level functions which are not accessible outside of the module in which they are created. If the name is supplied then the facility is a named facility, otherwise it is automatically named (auto-named). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided. The first variables in the parameter list are required. If a plus sign is provided, then those variables following are optional. If an ampersand is provided, then the symbol following is bound to a list of remaining actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted.

##### Example

```

> (module SuperMath

(facility power {?x + ?y = 1} ; private to the module

(** ?x ?y)

)

(function superpower {& ?numbers} ; public to the module

(if (void-p ?numbers)

(return unknown))

(let ?result (@ ?numbers))

(for ?n in (rest ?numbers)

(--> power ?result ?n))

?result

)

)

.:  SuperMath

> (use User)

.:  User

> (SuperMath.superpower 2 3 4)

.:  4096

> (SuperMath.power 2 3)

.:  \[Failure :Name UndefinedFunction :Text "The function SuperMath.power is not defined"\]

> (facility-p power SuperMath)

.:  true

> (function-p power SuperMath)

.:  false

```

##### Related

call, extend, functions, macro, module, modules

## few

True if a predicate is true for less than half the elements in a sequence.

##### Syntax

(few _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if less than half the elements satisfies the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated.

##### Example

```

> (few ?n in {1 2 3 4} (= (taxon ?n) number))

.:  false

> (few ?m ?n per {{2 1} {3 4} {7 9}} (< ?m ?n))

.:  false

> (few ?m ?n over {4 2 3 7} (divisible-p ?m ?n))

.:  true

```

##### Related

every, nevery, most, none, some

## file

Opens or creates a file.

##### Syntax

(file _url_ _option_ _…_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url to the file. |
| option | expression | 0+  | A key value pair. Any of<br><br>mode _mode_ \- append, create, open (default), truncate.  <br>access _access_ \- read, write, or readwrite (default).  <br>sharing _share_ \- none, read (default), write, or readwrite.  <br>seek _location_ - a number from 1 (default) to # (eof).  <br>content _type_ - binary (default) or text.  <br>from _place_ - memory or network (default).  <br>buffer _size_ - minimum buffer size (default is 1). |

##### Results

| Data Type | Description |
| --- | --- |
| file | A file literal. |

##### Remarks

Opens a file for reading or writing and returns a file resource. If the file does not exist then it is created. If from memory is specified, the contents of the file is first cached locally to memory then accessed. If from network is specified, the contents of the file isaccessed over the network.

##### Example

```

> (let ?url (url "file://localhost/C:/temp/quick.txt"))

.:  true

> (if (there ?url)

(let ?file (file ?url mode append))

(write ?file "The quick brown fox")

(close ?file)

(free ?file))

.:  closed

```

##### Related

close, erase, free, read, seek, there, write

## files

Returns a list of file names.

##### Syntax

(files _folder_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| folder | folder | 1   | A folder. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list file name strings. |

##### Remarks

If the path is invalid, the function fails. Files or symbolic links to files are returned.

##### Example

```

> (files path (path "c" (separator volume)))

.:  {"homework.txt" "temp.txt" "mypath.lnk"}

```

##### Related

folder, folders, links, there, path, separator

## fill

Fills a list with the result of an expression.

##### Syntax

(fill _symbol_ from _start_ to _end_ by _increment_ with _expression_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol iterator |
| from | literal | 0-1 | The literal from. |
| start | number | 0-1 | A number. If from is given this is required. Defaults to 1. |
| to | literal | 1   | The literal to. |
| finish | number | 1   | A number. |
| by | literal | 0-1 | The literal by. |
| increment | number | 0-1 | A number. If by is supplied this is required. |
| with | literal | 1   | the literal with. |
| expression | variant | 1   | a value to populate the list |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of the indicated length containing the value of the expression. |

##### Remarks

The value of the symbol iterator is available to the expression when building the list.

##### Example

```

> (fill ?i to 3 with ($ "foo-" ?i))

.:  {"foo-1" "foo-2" "foo-3"}

> (fill ?j to 5 with (\* ?j 2))

.:  {2 4 6 8 10}

> (fill ?x from -4 to 6 by 2 with {?x})

.:  {{-4}{-2}{0}{2}{4}{6}}

```

##### Related

fill, pad, range

## filter

Returns a sequence of elements that satisfy a predicate.

##### Syntax

(filter _sequence predicate_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| predicate | function | 1   | A truth function. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A new list containing elements satisfying the predicate. |

##### Remarks

For each element in the sequence, if the predicate is true for the element, the element is concatenated into a result list, otherwise the item is excluded from the result list. Finally, the result list is returned.

##### Example

```

> (filter {1 2 3 4} even-p)

.:  {2 4}

> (filter {1 2 3 4 5 6} (given {?n} (divisible-p ?n 3))

.:  {3 6}

```

##### Related

apply, coalesce, collect, gather, reduce, sort, map, quantity

## find

Returns the best matching candidates.

##### Syntax

(find _features candidates option_ _..._ )

_option ::= key value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| features | List | 1   | The features to compare to the candidates |
| candidates | list | 1   | The candidates to be compared |
| option | expression | 0+  | Key value pairs , where a key is one of:<br><br>limit - The number of matches to return.  <br>(default is 1)<br><br>minscore - value above which candidates shall be considered. Default is ninfinity<br><br>maxscore – Value below which candidates are acceptable. Default is 1.<br><br>transform – The literal name of a value transformation function.<br><br>comparer - The literal name of a comparison function |

##### Results

| Data Type | Description |
| --- | --- |
| list | A sorted list of lists containing candidate - score pairs. |

##### Remarks

Find compares a set of features to those of candidates and returns the best matching candidate(s) with match score(s). It uses the similarity function (~) as the default comparer. If provided, transforms are applied before comparison. Finally, a comparer can accept two values and returns a score representing the degree of similarity where higher means more similar.

##### Example

```

> (find {" t" " th" "thi" "his" "is " "s "}

{"there" "that" "though" "thin"}

comparer (given {?x} (ngrams ?x 3)))

.:  {{"thin" 0.142857}}

```

##### Related

~ _similarity_, /~ _dissimilarity_

## finishes-p

True if two intervals finish together.

##### Syntax

(finishes-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if interval1 finishes with interval2. |

##### Remarks

None.

##### Example

```

> (finishes-p \\@i{\\@s1 \\@s2} \\@i{\\@s3 \\@s4})

.:  false

> (finishes-p \\@i{\\@s1 \\@s5} \\@i{\\@s4 \\@s5})

.:  true

> (finishes-p \\@i{\\@s1 \\@s9} \\@i{\\@s4 \\@s6})

.:  false

> (finishes-p \\@i{\\@s4 \\@s9} \\@i{\\@s1 \\@s9})

.:  true

> (finishes-p \\@i{\\@s7 \\@s9} \\@i{\\@s3 \\@s8} \\@s1)

.:  true

```

##### Related

before-p, during-p, meets-p, overlaps-p, starts-p

## finishing

Returns the instant an interval finishes.

##### Syntax

(finishing _interval_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval | interval | 1   | An interval |

##### Results

| Data Type | Description |
| --- | --- |
| instant | The finishing value of the interval. |

##### Remarks

None.

##### Example

```

> (finishing \\@i{\\@s1 \\@s2})

.:  \\@s2

> (finishing \\@i{\\@s1 \\@s5})

.:  \\@s5

> (finishing \\@i{\\@s4 \\@s6})

.:  \\@s6

```

##### Related

beginning

## fix

Adds variables to the current environment.

##### Syntax

(fix _declaration_ _..._ )

_declaration ::= taxon symbol value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| declaration | expression | 1+  | A taxon, symbol and value triple. |

##### Results

| Data Type | Description |
| --- | --- |
| Truth | Returns true. |

##### Remarks

Sequentially creates variables in the current environment. Each symbol shall replace any extant symbol with the same name in the environment. The taxon shall restrict the type of the symbol. If the default does not match the taxon, a failure shall be triggered.

##### Example

```

> (fix literal ?person DrWho)

.:  true

> ?person

.:  DrWho

> (fix integer ?x 1

float ?y 2.0

long ?z 3n)

.:  true

```

##### Related

<-- _before tie_, --> _after tie_, constant, dynamic, fix, global, local, set, tie

## float

Converts a value to a floating number.

##### Syntax

(float _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number or the literal minimum or maximum. |

##### Results

| Data Type | Description |
| --- | --- |
| float | A float number. |

##### Remarks

If the value cannot be converted to a float, the function fails.

##### Example

```

> (float {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a float"\]

> (float "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not a float"\]

> (float 500)

.:  500.0f

> 500.0f

.:  500.0f

> (float "23.4")

.:  23.4f

```

##### Related

complex, imaginary, integer, long, rational, real

## floor

Rounds a number towards negative infinity.

##### Syntax

(floor _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| number | The next lower integer. |

##### Remarks

Returns the next lower positive integer.

##### Example

```

> (floor 100.5)

.:  100

> (floor -100.5)

.:  -101

```

##### Related

ceiling, round, truncate

## fold

Tranforms a sequence into a value.

##### Syntax

(fold _symbol_ _…_ in _sequence_ into _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 2+  | Iteration variables |
| in | literal | 1   | The literal in |
| sequence | sequence | 1   | A sequence (string or list) |
| into | literal | 1   | The literal into |
| expression | variant | 1+  | A expression that transforms the iteration variables |

##### Results

| Data Type | Description |
| --- | --- |
| list | A new list after the transformation is applied |

##### Remarks

The first element of the list is stored in the first variables and the second element is stored in the second symbol (and so forth), then the expressions are evaluated. The result of the last expression is stored in the first symbol while the next element(s) in the sequence is (or are) stored in the second symbol (and so on). This is repeated until all elements are processed

##### Example

```

> (fold ?x ?y in {1 2 3 4 5} into (\* ?x ?y))

.:  120

> (generator OneToFive (yield 1)(yield 2)(yield 3)(yield 4)(yield 5)(done))

.:  OneToFive

> (fold ?i ?j ?k in (OneToFive) into (+ ?i ?j ?k))

.:  15

```

##### Related

reduce

## folder

Creates or locates a folder in the file system.

##### Syntax

(folder _url_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url to the file. |

##### Results

| Data Type | Description |
| --- | --- |
| folder | A folder resource. |

##### Remarks

Returns a folder resource.

##### Example

```

> (let ?path (path "." (separator) "temp"))

.:  true

> (there path ?path)

.:  false

> (folder path ?path)

.:  folder-1

> (there path ?path)

.:  true

```

##### Related

file, file-p, folder-p, path, read, separator, write

## folders

Returns a list of sub folders.

##### Syntax

(folders _option_ _…_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 1+  | A key value pair. One of<br><br>url _url_ \- full url to the file.<br><br>host _host_ \- name of the host computer<br><br>volume _volume_ \- name of the disk volume<br><br>path _path_ - name of the path to the folder<br><br>name _name_ \- name of the folder |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of folders strings in the specified path. |

##### Remarks

If the path is invalid, the function fails. Otherwise, a list of sub folders is returned for the path.

##### Example

```

>(folders path (path "."))

.:  {"build" "META-INF" "WebContent"}

```

##### Related

erase, file, files, folder, there, path, separator

## for

Iterates over the elements in a sequence.

##### Syntax

(for _symbol_ _…_ _binding reversal_ _sequence_ _…_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, over, or across. |
| reversal | literal | 0-1 | The literal reverse. |
| sequence | sequence | 1+  | A list or string |
| expression | variant | 0+  | The expression(s) to evaluate |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value returned on the last iteration. |

##### Remarks

Variables and sequences are required for in, per, and over. If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If the binding across is specified, each symbol is bound to elements of the corresponding sequence (i.e, first symbol to the first sequence, second to the second, etc.). If there are insufficient elements to bind to the variables then the function fails. If the literal reverse is present, the sequence is traversed in reverse. On each iteration, all the expressions are executed. The return value is the result of the last call evaluated on the last iteration.

##### Example

```

> (for ?c in reverse "the quick brown fox" (tell user ?c))

xof nworb xciuq eht.: told

> (for ?key ?value per {{k1 v1}{k2 v2}{k3 v3}}

(tell user ($ ?key ($$ ?value , (\\s)))))

k1 v1, k2 v2, k3 v3, .: told

```

##### Related

count, do, each, loop, repeat, step, until, while

## forever

Repeatedly evaluates expressions until a failure is encountered.

##### Syntax

(forever _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, over, or across. |
| reversal | literal | 0-1 | The literal reverse. |
| sequence | sequence | 1+  | A list or string |
| expression | variant | 0+  | The expression(s) to evaluate |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value returned on the last iteration. |

##### Remarks

On each iteration, all the expressions are executed. The return value is the result of the last call evaluated on the last iteration.

##### Example

```

> (forever

(try (print ">> " (eval (ask user "\* ")))

learn ?error (print ">> " ?error)))

\* hello

>> hello

\*

```

##### Related

count, do, each, loop, repeat, step, until, while

## forgo

Removes a dependent module.

##### Syntax

(forgo _dependency module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| dependency | literal | 1   | A dependent module. |
| module | literal | 0-1 | A module. Default to the module obtained by (use). |

##### Results

| Data Type | Description |
| --- | --- |
| module | Returns the module. |

##### Remarks

Removes a module from the current module’s dependencies list.

##### Example

```

> (dependencies User)

.:  {Premise}

> (extend User (require (module Algebra)))

.:  Algebra

> (dependencies User)

.:  {Premise Algebra}

> (forgo Algebra User)

.:  User

> (dependencies User)

.:  {Premise }

```

##### Related

dependencies, discard, extend, forgo, module, require, grok, use

## format

Formats a string.

##### Syntax

(format _template value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| template | string | 1   | A format template. which uses the following directives:<br><br>~c - formats a number as currency<br><br>~e - formats a number as an exponential<br><br>~f - formats a floating point number<br><br>~g - formats a long number<br><br>~n - formats an integer number<br><br>~s - formats a string.<br><br>~v \- formats a generic variant<br><br>~~ - formats a single tilde character |
| value | variant | 0+  | A value to be formatted. |

##### Results

| Data Type | Description |
| --- | --- |
| string | A formatted string |

##### Remarks

The formatted result is returned.

##### Example

```

> (format "~v ~v" hello world)

.:  "hello world"

```

##### Related

$ _concatenate_, $$ _elide_, ask, capitalize, char, lowercase, tell, trim, uppercase

## fractional

Returns the fractional portion of a number.

##### Syntax

(fractional _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The fractional portion. |

##### Remarks

The fractional portion is the number minus the floor of the number.

##### Example

```

> (fractional 300)

.:  0.0

> (fractional 0.564)

.:  0.564

> (fractional -2302.023900)

.:  -0.0239

> (fractional 0.003500)

.: 0.0035

```

##### Related

digit, digits, exponential, sign, significand

## free

Releases resources.

##### Syntax

(free _resources_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| resources | variant | 1   | A single resource or list of resources. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns the literal freed if successful. |

##### Remarks

None.

##### Example

```

> (free

(tarry (complete

(do (idle \\@s5) something)

(do (idle \\@s5) something-else)

(do (idle \\@s5) one-more-thing))))

.:  freed

> (free

(cancel (complete

(do (idle \\@s5) something)

(do (idle \\@s5) something-else)

(do (idle \\@s5) one-more-thing))

mode immediate))

.:  freed

```

##### Related

concurrent, cancel, complete, reclaim, tarry, task, wait

## full

True if values are equal or either value is nil.

##### Syntax

(full _first_ _second_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| first | variant | 1   | A value to be compared. |
| second | variant | 1   | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are the same or if either is nil |

##### Remarks

Returns true if each value is the same or if either value is nil. Both values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equivalent if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical). Return false otherwise.

##### Example

```

> (full a a)

.:  true

> (full "johnny" "ralph")

.:  false

> (full 3 nil)

.:  true

> (full nil 4)

.:  true

```

##### Related

< _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal_, identical, left, right

## function

Creates a public function in a module.

##### Syntax

(function _scope name parameters returning expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ % _keyword_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ % _keyword_ _…_ & _remaining_ }

_parameters_ ::= {_required_ _…_ % _keyword_ _…_ & _remaining_ }

_parameters_ ::= {_required_ _…_ & _remaining_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ % _keyword_ }

_parameters_ ::= { \+ _optional_ _…_ % _keyword_ _…_ & _remaining_ }

_parameters_ ::= { \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { % _keyword_ _…_ }

_parameters_ ::= { % _keyword_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied, a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| returning | expresrsion | 0-1 | The expression “returns _taxon_”, where taxon is a taxon or meron. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Functions are defined using the function intrinsic function. If the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided. The first variables in the parameter list are required. If a plus sign is provided, then those variables following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If a percent sign is supplied the next variables are keyword variables where the supplied slot shall have the same name as the symbol parameter excepting the first character of the name which shall be a colon for the slot and a question mark for the symbol. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. The entire parameter list may be omitted.

If the literal returns follows the (non)extant parameter list then the next literal is either a taxon or a meron. which restricts the result of the function. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example

```

> (function {?n} (+ 1 ?n))

.:  fn-1

> (function plusN {?n + ?i = 1} (+ ?n ?i))

.:  plusN

> (function (scope) addAll {& ?nums} (apply + ?nums))

.:  addAll

> (fn-1 100)

.:  101

> (plusN 100)

.:  101

> (function tryParseNum {String ?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

> (tryParseNum "foo")

.:  {false nil}

> (tryParseNum "123")

.:  {true 123}

> (function dont {{try ?what} + {at ?where = nil}}

(apply (given {?s}(tell user ?s))

($ don't try ?what (unless (any ?where) "" ($ at ?where))))

.:  dont

> (dont try "skydiving into a volcano")

don't try skydiving into a volcano

.:  told

> (dont try this at home)

don't try this at home

.:  told

```

##### Related

arguments, call, extend, functions, junction, macro, module, modules, parameters, procedure

## functions

Returns a list of functions defined in a module.

##### Syntax

(functions _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module. If not provided defaults to the current module. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of functions defined in the module. |

##### Remarks

The module must be a literal in the list obtained by calling the (modules) function. If the module is not provided this function uses the current module (obtained via the (use) function).

##### Example

```

> (module Mine

(function foo {} bar))

.:  Mine

> (functions Mine)

.:  {foo}

> (use User)

.:  User

> (function hello {} world)

.:  hello

> (functions)

.:  {hello}

```

##### Related

function, module, modules, variables

## gather

Returns a sequence of elements that satisfy a predicate.

##### Syntax

(gather _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A sequence (string or list) |
| expression | variant | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A sequence containing the elements that satisfy the test. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated. If the last value returned is a true truth value, the item is concatenated into a result list, otherwise the item is excluded from the result list. Finally, the result list is returned.

##### Example

```

> (gather ?n in {-3 -2 -1 0 1 2 3 4} (even-p ?n))

.:  {-2 0 2 4}

> (gather ?x ?y per {{4 2}{7 3}{1 2}{15 5}} (divisible-p ?x ?y))

.:  {{4 2}{15 5}}

```

##### Related

coalesce, collect, filter

## generator

Creates a series generator.

##### Syntax

(generator _name parameters expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern gn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| generator | A function that returns a series. |

##### Remarks

If the name is not supplied then the generator is automatically named (auto-named). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided in the call to the generator. The first variables in the parameter list are required. If a plus sign is provided, then those variables following are optional. If an asterisk is provided, then keyword and vaues are expected. Keyword parameters (literal symbol pairts) may be provided as required or optional. If an ampersand is provided, then the symbol following is bound to a list of remaining actual parameter values. The entire parameter list may be omitted.

##### Example

```

> (generator primeNumbers

(so {?primes {}}

(step ?i from 2 to infinity

(if (none ?p in ?primes (divisible-p ?i ?p))

(add ?primes ?i)

(yield ?i)))))

.:  primeNumbers

> (collect ?p in (primeNumbers)

(if (> ?p 20) (break ?p) else ?p))

.:  {2 3 5 7 11 13 17 19 23}

> (let ?series (series (primeNumbers)))

.:  true

> (if (next ?series) (this ?series))

.:  2

> (if (next ?series) (this ?series))

.:  3

> (if (next ?series) (this ?series))

.:  5

> (generator {?interrupt}

(yield 1)

(yield 2)

(if ?interrupt (done))

(yield 3)

(yield 4)

(done))

.:  gen-1

> (collect ?x in (gen-1 true) ?x)

.:  {1 2}

> (collect ?x in (gen-1 false) ?x)

.:  {1 2 3 4}

> (gen-1 true)

.:  {...}

```

##### Related

done, is, next, reset, this, yield

## get

Retrieves a value using one or more keys.

##### Syntax

(get _container key_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | A sequence or assortment. |
| key | variant | 1+  | A key or function. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The value resulting from the retrieval. |

##### Remarks

Consecutively applies the next key to each resultant value. Terminates when all keys are exhausted or when the function fails.

##### Example

```

> (get (new (relation Box :Length 24 :Width 12 :Height 9)) :Width ++ ++)

.:  14

> (relation Person :Name :Friend)

.:  Person

> (so {?person nil}  
(for ?name in {Jane John Sally Chuck Martha Shane Todd}

(tie ?person (new Person :Name ?name :Friend ?person))))

.:  Person_7

> (get Person_7 :Friend :Name)

.:  Shane

> (get Person_7 :Friend :Friend :Name)

.:  Martha

```

##### Related

@ _element_, deq, enq, get, let, the, with

## given

Creates an anonymous function.

##### Syntax

(given { _parameter_ _…_ } _expression_ _…_ )

_parameter_ ::= _required_ _…_

_parameters_ ::= _required_ _…_ + _optional_ _…_

_parameters_ ::= \+ _optional_ _…_

_parameters_ ::= _required_ _…_ \+ _optional_ _…_ & _remaining_

_parameters_ ::= & _remaining_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| parameters | list | 1   | A list containing zero or more parameters and sigils |
| expression | variant | 0+  | Expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| anonym | Returns the anonym the expression represents. |

##### Remarks

An anonym is an anonymous function. An anonym is equivalent to lambda in the Lisp programming language, and can be used in most places a function name is required. Anonyms cannot be recursive, since they are unnamed. Continuations may be taken within an anonym. Neither do anonyms use tags that can be reference by a return. If no parameters are specified, then each expression is executed in succession and the value of the last expression is returned. If parameters are specified, then arguments must be provided in the invocation. Anonyms are ephemeral because function definitions are not maintained for them.

##### Example

```

> ((given {?s} (tell user ($ ?s \\n))) "Hello, world.")

Hello, world.

.:  told

> (map {One Two Three Four Five}

(given {?x} (tell user ($$ ?x "..." \\n)))

One...

Two...

Three...

Four...

Five...

.:  told

> (filter (range 1 to 40) (given {?n} (and (even-p ?n) (divisible-p ?n 7))))

.:  {14 28}

```

##### Related

wait, abort, concurrent, await, complete, done-p, reclaim,task, use

## global

Creates global variables.

##### Syntax

(global _assignment_ _…_ )

_assignment_ ::= _symbol value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assignment | expression | 1+  | A symbol value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates global variables.

##### Example

```

> (global ?START_OF_TASK 1)

.:  true

> (global ?FIRST_NAME "Jane"

?LAST_NAME "Smith"

)

.:  true

```

##### Related

<-- _before tie_, --> _after tie_, constant, dynamic, local, let, modular, put, suppose, swap, undeclare

## go

Transfers control to a function.

##### Syntax

(go _function argument_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function. |
| argument | variant | 0+  | An argument to the function. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the result. |

##### Remarks

Transfers control to the specified function by unwinding the current function from the call graph then jumping to the specified function.

##### Example

```

> (relation Queue :Items {} :Capacity 100

!count (given {?me}(# (:Items ?me)))

!full-p (given {?me}(>= (!count ?me) (:Capacity ?me))))

.:  Queue

> (function produce {?q}

(while (not (!full-p ?q))

(repeat (random 1 to (- (:Capacity ?q) (!count ?q)))

(enq ?q :Queue (new Item))))

(go consume ?q))

.:  produce

> (function consume {?q}

(while (more-p(:Queue ?q))

(repeat (random 1 to (# (:Queue ?q)))

(deliver (pop (:Queue ?q)))))

(go produce ?q))

> (produce (new Queue))

```

##### Related

continuation, continue

## grok

Evaluates expressions in a url or file.

##### Syntax

(grok _what_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| what | variant | 1   | A uniform resource locator or file resource. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last expression evaluated. |

##### Remarks

This function opens the url or file, and evaluates each expression therein.

##### Example

```

> (grok (file name "Module1.th"))

.:  Module1

> (grok (url "file://MyCodeSite.com/Module2.th"))

.:  Module2

```

##### Related

eval, file, posit, url

## group

Combines sublists by position or key.

##### Syntax

(group _list_ by _key_ _…_ into _symbol_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| list | list | 1   | A list containing  sublists or tuples. |
| by | literal | 1   | The literal by. |
| keys | list | 1   | A list containing either slots, integer positions, or transform functions that return a value given an element of the list. |
| into | literal | 1   | The literal into. |
| symbol | symbol | 1   | A symbol storing each grouping. |
| expression | variant | 0+  | An expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of the last expression. |

##### Remarks

Each key is either a numeric position, slot or method name, or a transform function which when applied to a list element shall return a value. If as is not provided, then a list of the intermediate groupings is returned. If keyword as is provided, then the subsequent expressions shall have the grouping symbol available for evaluation and the final expression is collected into a list.

##### Example

```

> (group {{1 a b c}{2 b c a}{3 c a b}{4 a b c}{5 b c a}{6 c a b}} by {2 3} into ?g)

.:  {{{1 a b c}{4 a b c}}{{2 b c a}{5 b c a}}{{3 c a b}{6 c a b}}}

> (group

{\[Fruit :Color red :Name cherry\]\[Fruit :Color red :Name apple\]

\[Fruit :Color red :Name tomato\]\[Fruit :Color yellow :Name banana\]}

by {:Color} into ?g

\[R :Color (:Color (@ ?g)) :Count (# ?g)\])

.:  {\[R :Color red :Count 3\] \[R :Color yellow :Count 1\]}

```

##### Related

coalesce, collect, count, gather, given, separate, sort, with

## halt

Terminates a cell or bion.

##### Syntax

(halt _compute_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| compute | compute | 1   | A cell or bion. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The literal halted. |

##### Remarks

This function starts an asynchronous agent task that processes incomingc messages and performs a default job.

##### Example

```

> (let ?url (url scheme tcp port 5001))

.:  true

> (function reply {?sender ?message} (tell ?sender "OK"))

.:  reply

> (function job {& ?args} (tell user ($ 1)) (wait 0.5))

.:  job

> (agent ?url reply job)

.:  Agent-1

> (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1)

111111.: cancelled freed

```

##### Related

bion, cell, free, task

## has

True if a key is present in an assortment.

##### Syntax

(has _assortment key_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | A sequence or assortment |
| key | variant | 1   | A key. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the key is present. or false if the key is absent. |

##### Remarks

None

##### Example

```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.:  Lexicon-1

> (has Lexicon-1 :C)

.:  true

> (has Lexicon-1 !m)

.:  true

> (has Lexicon-1 !q)

.:  false

```

##### Related

beyond, lacks, within

## hash

Computes a hash code.

##### Syntax

(hash _value option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| option | expression | 0+  | A key value pair<br><br>size number - a hash table size (default 1000)<br><br>seed number - a prime number seed. |

##### Results

| Data Type | Description |
| --- | --- |
| integer | The hash value |

##### Remarks

Returns a hash value between zero and the given size, based on the given prime number seed. The size and seed can be omitted.

##### Example

```

> (hash {a b c})

.:  822826764062

> (hash {a b c} size 100)

.:  62

> (hash {a b c} size 1000 prime 3)

.:  186

```

##### Related

array, collection, lexicon

## help

Describes a function.

##### Syntax

(help _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 0-1 | The name of a function. |

##### Results

| Data Type | Description |
| --- | --- |
| nil | Returns nil. |

##### Remarks

Prints the function documentation and returns nil.

##### Example

```

> (help)

Enter expressions followed by a blank line. Type (help), (copyright) or (license)

for information. Type (grok "file.theory") to read a file. Type (bye) to exit.

.:  nil

> (help help)

(intrinsic Base.help {+ ?function} returns NIL ...)

Returns documentation about a function. If no function is provided, general help is displayed.

.:  nil

```

##### Related

about, bye, copyright, license

## here

Adds variables in parallel to the current environment.

##### Syntax

(here _assignment_ _..._ )

_assignment ::= symbol value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true |

##### Remarks

Concurrently creates variables in the current environment. Each symbol shall replace any extant symbol with the same name in the current environment. Each symobl assignment occurs either in parallel with, or in isolation to, the other symbol assignments.

##### Example

```

> (let ?start 1 ?end 100 ?range (range ?start to ?end))

.:  true

> (undeclare {?start ?end ?range})

.:  undeclared

> (here ?start 1 ?end 100 ?range (range ?start to ?end))

.:  \[Failure :Name UnboundSymbol :Text "The symbol ?start is unbound"\]

> (do (here ?start 1 ?end 100)

(step ?i from ?start to ?end (do nothing)))

.:  nothing

```

##### Related

<-- _before tie_, --> _after tie_, assume, constant, dynamic, given, global, local, put

## hyperlink

Creates a hyperlink.

##### Syntax

(hyperlink _option_ _…_ )

(hyperlink _address_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| address | string | 0-1 | The url address. |
| option | expression | 0+  | A key value pair. One of<br><br>user _credentials_ \-user name and password<br><br>host _host_ \- host computer name (default is localhost)<br><br>port _number_ – a port number. (default is 2001)<br><br>path _path_ – a path<br><br>query _query_ – a query element<br><br>fragment _fragment_ – a fragment element |

##### Results

| Data Type | Description |
| --- | --- |
| service | A file resource |

##### Remarks

Returns a hyperlink.

##### Example

```

> (function reply {?target ?request} (tell ?target "goodbye."))

.:  reply

> (service (var ?service (hyperlink "http://localhost:4500/foxxy")) reply)

.:  Service-1

> (ask ?service "hello")

.:  "goodbye."

> (cancel Service-1) (free ?service) (free Service-1)

.:  cancelled freed freed

```

##### Related

close, erase, path, pipe, read, socket, write

## id

Returns a resource number.

##### Syntax

(id _resource_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| resource | resource | 1   | A resource. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The resource number or nil. |

##### Remarks

None

##### Example

```

> (new (relation Q))

.:  Q_1

> (id Q_1)

.:  1

> (id \[Q ^ Q_2\])

.:  2

> (id file-27)

.:  27

> (id foo)

.:  nil

```

##### Related

^ _thought_, id, uid, unique

## identical-p

True if all values occupies the same memory location.

##### Syntax

(identical-p _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | value | 2+  | Values to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are identical |

##### Remarks

Returns true if each value is identical to its successor from left to right, and false otherwise. All values must be of the same type, and must occupy the same address in memory. This function short circuits if false.

##### Example

```

> (identical-p a a a a)

.:  true

> (identical-p a (clone a) a a)

.:  false

> (identical-p "johnny" "ralph" "sam")

.:  false

> (identical-p 3 3)

.:  true

> (identical-p 3 (clone 3))

.:  false

```

##### Related

< _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal,_ canonify, identity

## identity

Returns the value itself.

##### Syntax

(identity _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | Any value |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the value. |

##### Remarks

None.

##### Example

```

> (identity a)

.:  a

> (identity {a b c})

.:  {a b c}

> (identity (++ 0))

.:  1

```

##### Related

canonify, identical-p

## idle

Pauses for a specified interval.

##### Syntax

(idle _duration_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| duration | instant | 1   | The quantity of time to pause. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns ready |

##### Remarks

None

##### Example

```

> (idle \\@s10)

.:  ready

```

##### Related

moment, seconds, tick

## if

Branched conditional evaluation.

##### Syntax

(if _condition_ _expression_ … _or-clause_ … _else-clause_)

_or-clause_ ::= or _condition expression_ _…_

_else-clause_ ::= else _expression_ _…_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| expression | expression | 1+  | Any expression |
| or-clause | expression | 0+  | The literal or followed by a condition and zero or more expressions. |
| else-clause | expression | 0-1 | The literal else followed by one or more expressions |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The last value of the executed clause or nil if no conditions were true and no else clause was provided. |

##### Remarks

None

##### Example

```

> (global ?N 100)

.:  true

> (if (> ?N 100) over

or (< ?N 100) under

else exactly)

.:  exactly

```

##### Related

and, case,either, not, or, unless

## imaginary

Converts a value to an imaginary number.

##### Syntax

(imaginary _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number or the literal minimum or maximum. |

##### Results

| Data Type | Description |
| --- | --- |
| integer | An integer number. |

##### Remarks

If the number cannot be converted to an imaginary number, the function fails. If the value is complex, then the imaginary portion is selected.

##### Example

```

> (imaginary {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (imaginary "a b c")

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (imaginary 500)

.:  500i

> (imaginary 500.1)

.:  500.1i

> (imaginary "-23.4")

.:  -23.4i

```

##### Related

complex, integer, long, rational, real

## includes

True if a value is in a sequence.

##### Syntax

(includes _sequence element option_ _…_ )

##### Module

Base

##### Parameters

None

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| element | variant | 1   | A value. |
| option | expression | 0-2 | A key value pair. Any of<br><br>depth _number_ \- Number or # (for any depth). Default is 1.<br><br>transform _function_ \- A function to transform the element. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the item is in the container. |

##### Remarks

If value and sequence are strings, then a string search is performed. If sequence is a list and depth is greater than one, then subsequences shall be checked for the value. A depth of # implies search to any depth.

##### Example

```

> (includes {a b c d e f g} d)

.:  true

> (includes "cbazyx" "w")

.:  false

> (includes "cbazyx" 25 transform (given {?c} (++ (- (unicode ?c) (unicode "a")))))

.:  true

```

##### Related

excludes, in, out

## index

Creates an index on slots of a relation.

##### Syntax

(index _relation slot_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| relation | literal | 1   | A meron. |
| slot | literal | 1+  | The name of a slot in the relation |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the index |

##### Remarks

Creates an index for the specified slots to expedite value retrieval.

##### Example

```

> (relation X :A :B :C)

.:  X

> (index X :B)

.:  X_Index_1

> (index X :A :B)

.:  X_Index_2

> (new X :A 1 :B 2)

.:  X_1

> (which X ^ as ?x :B 1 list ?x)

.:  {X_1}

```

##### Related

drop, indices, relation

## indices

Returns a list of indices for a relation.

##### Syntax

(indices _relation_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| relation | relation | 1   | A relation. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of indices associated with the relation. |

##### Remarks

None.

##### Example

```

> (relation X :A :B :C)

.:  X

> (indices X)

.:  {}

> (index X :B)

.:  X_Index_1

> (index X :A :B)

.:  X_Index_2

> (indices X)

.:  {X_index_1 X_index_2}

> (drop (indices X))

.:  1

```

##### Related

drop, index, relation

## infix

Creates a new sequence with interposed delimeters.

##### Syntax

(infix _sequence delimeter_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| delimeter | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list with delimeters between the elements |

##### Remarks

A delimeter is placed between each element. If the sequence is a string, the delimiter shall be converted into a string. If the sequence has less than two elements, no changes are made.

##### Example

```

> (infix {a b c d} \* )

.:  {a \* b \* c \* d}

> (infix "abcd" ", ")

.:  "a, b, c, d"

> (infix {} ",")

.:  {}

> (infix "" ",")

.:  ""

```

##### Related

$ _concatenate_, split

## inside

Creates an expression from a sequence or assortment.

##### Syntax

(inside _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A sequence, assortment, or expression. |

##### Results

| Data Type | Description |
| --- | --- |
| expression | returns the contents of the value as an expression. |

##### Remarks

If value is a sequence or assortment then the contents are returned as an expression, otherwise, an empty expression is returned.

##### Example

```

> (inside {the quick brown fox})

.:  the quick brown fox

> (inside {})

.: 

> (void-p (inside {}))

.:  true

> (inside (lexicon 1 a 2 b 3 c 4 d))

.:  1 a 2 b 3 c 4 d

> (inside (collection 1 2 3 a b c))

.:  1 2 3 a b c

```

##### Related

& _merge_, && _abridge_, expression, is, list

## insert

Creates a new sequence by inserting values.

##### Syntax

(insert _sequence position value_ _…_ )

_entry ::=_ _value position_

_entry ::= alue_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| position | integer | 1   | The position to begin inserting the values. |
| value | variant | 1+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A new sequence. |

##### Remarks

This function creates a new sequence. To modify a sequence use the push function.

##### Example

```

> (insert "abcdef" 1 g)

.:  "gabcdef"

> (insert "abcdef" # g)

.:  "abcdefg"

> (insert {a b c} 1 d e f)

.:  {d e f a b c}

> (insert "abc" 1 d e f)

.:  "defabc"

```

##### Related

\# _size_, add, cut, deq, enq, get, key, keys, push, put, values, zap

## insort

Inserts a value into a sorted sequence.

##### Syntax

(insort _sequence value option_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| value | value | 1   | A value |
| option | expression | 0+  | A key value pair where the key is<br><br>comparer _function_ - a function returning &lt;, =, &gt;<br><br>unique _yes\|no_ - Allows duplicate values. Default yes. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The new sequence after insertion. |

##### Remarks

Inserts the item in sorted order in the sequence. If the sequence is a list and first element is a number then the list is kept numerically sorted, otherwise it is alphabetically sorted.

##### Example

```

> (insort {a b c d e x} q)

.:  {a b c d e q x}

> (insort "abcde" "z")

.:  "abcdez"

> (function desc {?x ?y}

(if (> ?x ?y) &lt; or (= ?x ?y) = else &gt;))

.:  desc

> (insort {108 79 33} 84 comparer desc)

.:  {108 84 79 33}

```

##### Related

insert

## instantiate

Creates an expression with premises in place of thoughts.

##### Syntax

(instantiate _expression_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | A SubThought or a list containing thoughts. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list containing premises |

##### Remarks

Replaces thoughts with corresponding premises within the supplied expression.

##### Example

```

> (relation E :Value)

.:  E

> (new E)

.:  E_1

> (relation B :Slot)

.:  B

> (new B)

.:  B_1

> (instantiate {E_1 {:Foo {B_1 x}}})

.:  {\[E ^ E_1 :Value nil\] {:Foo {\[B ^ B_1 :Slot nil\] x}}}

```

##### Related

^ _thought_, get, id,premise

## integer

Converts a value to an integer.

##### Syntax

(integer _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Data Type | Description |
| --- | --- |
| integer | An integer number. |

##### Remarks

If the value is minimum (or maximum) the minimum (or maximum) integer is returned; otherwise, if the value cannot be converted to an integer, the function fails. The fractional part of the number is truncated. An integer is a signed 64 bits number.

##### Example

```

> (integer {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (integer "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not a number."\]

> (integer 500.3)

.:  500

> (integer "23.4")

.:  23

```

##### Related

ceiling, complex, floor, is, long, radix, rational, real, round, truncate, unsigned

## interleave

Interleaves arguments into a new sequence.

##### Syntax

(intersection _sequence sequence_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | A sequence |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The interleaved sequence. |

##### Remarks

Returns a single sequence interleaving all sequences. if there are insufficient elements, NOTHING is supplied as the element. If the first element is not a sequence, then a list is returned. The sequence type shall be that of the first element.

##### Example

```

> (interleave {1 2 3} {4 5 6} {7 8 9} {10})

.:  {1 4 7 10 2 5 8 3 6 9}

> (interleave \[1 2 3\] \[4 5 6\] \[7 8 9\] \[10\])

.:  \[1 4 7 10 2 5 8 3 6 9\]

> (interleave |1 2 3| |4 5| |6| |7 8 9| |10|)

.:  |1 4 7 10 2 5 8 3 6 9|

> (interleave "abc" "def" "ghi" "j")

.:  "adgjbehcfi"

```

##### Related

&& _abridge_, mid, insert, pop, push, swap, transfer

## intersection

Creates a sequence of common elements.

##### Syntax

(intersection _sequence_ _sequence_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | A list or string |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A list of common items |

##### Remarks

Returns the intersection of the provided sequences, i.e., the elements common to all sequences.

##### Example

```

> (intersection {1 2 3 4} {2 3 4 5)

.:  {2 3 4}

> (intersection {2 3 4 5} {4 5 6 7})

.:  {4 5}

> (intersection {1 2 3 4} {2 3 4 5} {3 4 5 6} {4 5 6 7})

.:  {4}

> (intersection "abc" "bcd" "cde")

.:  "c"

```

##### Related

common, difference, union

## intersects-p

True if any elements intersect.

##### Syntax

(intersects-p _set1 set2_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| set1 | sequence | 1   | A sequence. |
| set2 | sequence | 1   | A sequence |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the sets have any elements in common. |

##### Remarks

None.

##### Example

```

> (intersects-p {a b c d e f g} {a b x})

.:  true

> (intersects-p {a b c d e f g} {a b d})

.:  true

> (intersects-p "the quick brown" "ick bro")

.:  true

> (intersects-p {a b c} {d e f})

.:  false

> (intersects-p {1 2 3} {4 5 6})

.:  false

```

##### Related

disjoint-p, subset-p

## interval

Creates a time interval.

##### Syntax

(interval _start finish_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| start | time | 0-1 | A time value. (Default is neternity) |
| finish | time | 0-1 | A time value. (Default is eternity) |

##### Results

| Data Type | Description |
| --- | --- |
| interval | An interval. |

##### Remarks

If no parameters are provided, start shall default to negative eternity (neternity), and finish wil default to positive eternity. If only start is provided, finish shall default to positive eternity If finish is less than start, the positions shall be swapped so that start is always less than or equal to finish.

##### Example

```

> (interval 2014-01-01 2015-12-31)

.:  \\@i{\\@d2014-01-01T00:00:00.000 \\@d2015-12-319T00:00:00.000}

> (interval \\@m2015000000000000)

.:  \\@i{\\@m2015000000000000 eternity}

> (interval \\@t63573798191026000 neternity)

.: \\@i{neternity \\@t63573798191026000}

> (interval)

.:  \\@i{neternity eternity}

> (interval \\@e600 \\@e300)

.:  \\@i{\\@e300 \\@e600}

```

##### Related

date, epoch, moment, seconds, tick

## into

Creates new thoughts based on existing thoughts.

##### Syntax

(into _relation thoughts_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| relation | relation | 1   | A relation . |
| thoughts | list | 1   | A list of records. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the relation or structure. |

##### Remarks

If the thoughts contain slots that are in the relation, the slot values are copied to new thoughts.

##### Example

```

> (relation X :A :B :C)

.:  X

> (repeat 10

(new X :A (random 1 to 100) :B (random 50 to 500) :C (random 0 to 1)))

.:  X_10

> (into (relation Y uses {X}) (with X))

.:  Y

> (which Y)

.:  {Y_1 Y_2 Y_3 Y_4 Y_5 Y_6 Y_7 Y_8 Y_9 Y_10}

```

##### Related

knew, new

## invoke

Invokes a call.

##### Syntax

(invoke _call environment_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| call | call | 1   | A call. |
| environment | environment | 0-1 | An environment (defaults to (scope)) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | A value returned by the call. |

##### Remarks

Invokes the call using the provided (or the current) environment.

##### Example

```

> (relation A

:Datum 0

!incr (function {?me}

(bind ?me :Datum ?n)

(put ?me :Datum (++ n))))

.:  A

> (new A)

.:  A_1

> (invoke (call !incr A_1) (scope))

.:  1

> (invoke (call !incr A_1) (scope))

.:  2

> (invoke (call @ "hello"))

.:  "h"

```

##### Related

apply, call, closure, eval, function, macro, scope, supply

## is

Applies the predicate to the value returning true or false..

##### Syntax

(is _value_ _predicate_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| predicate | literal | 0-1 | a unary function returning true or fase. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is true, or if the applied unary predicate returns true. |

##### Remarks

None.

##### Example

```

> (is true)

.:  true

> (is false)

.:  false

> (is 41 even-p)

.:  false

> (is 9 (given {?n} (divisible-p ?n 3)))

.:  true

> (is foo null-p)

.:  false

> (is nil null-p)

.:  true

```

##### Related

convert, datatype, known, the, type

## junction

Creates a public function in a module with arguments evaluated in parallel.

##### Syntax

(junction _scope name parameters expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied then a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Junctions are defined using the junction intrinsic function. A junction is merely a function that evaluates all it’s arguments in parallel. A parallel argument evaluation the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided. The first variables in the parameter list are required. If a plus sign is provided, then those variables following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example

```

> (junction add_it {integer ?a integer ?b integer ?c} (+ ?a ?b ?c))

.:  add_it

> (add_it 1 2 3)

.:  6

> (function fib {?n ) (on (<= ?n 1) 1 (add_it (fib (- ?n 1)) (fib (- ?n 2)))))

.:  fib

> (function fib2 {?n} (on (<= ?n 1) 1 (+ (fib (- ?n 1)) (fib (- ?n 2)))))

.:  101

> (macro duration {?x} (so {?now (jiffy) ?value (eval ?x) ?done (jiffy)}

(- ?ticks ?now))

.:  duration

> (duration (fib2 10))

.:  50

> (duration (fib 10))

.:  5

```

##### Related

arguments, call, extend, functions, macro, module, modules, parameters

## key

Finds the key for a value in an assortment.

##### Syntax

(key _assortment value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| value | variant | 1   | A value |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The key for the value. |

##### Remarks

If a key does not exist for the value, the function fails. It is advised to test whether the value exists in the assortment by first using the values function.

##### Example

```

> (var ?s (lexicon a 1 b 2 c 3 d 4))

.:  Lexicon-1

> (values ?s)

.:  {1 2 3 4}

> (keys ?s)

.:  {a b c d}

> (key ?s 4)

.:  d

> (key ?s 5)

.:  \[Failure :Name NotFound "The value 5 was not found in the assortment."\]

```

##### Related

@ _element_, position, values

## keys

Returns a list of keys for an assortment.

##### Syntax

(keys _assortment_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of values |

##### Remarks

All keys from the assortment are returned in a list.

##### Example

```

> (var ?s (lexicon a 1 b 2 c 3 d 4))

.:  Lexicon-1

> (values ?s)

.:  {1 2 3 4}

> (keys ?s)

.:  {a b c d}

> (key ?s 4)

.:  d

> (key ?s 5)

.:  \[Failure :Name NotFound :Text "The value 5 was not in the assortment."\]

```

##### Related

key, values

## keywords

Returns the list of Premise keywords.

##### Syntax

(keywords)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is a keyword. |

##### Remarks

None.

##### Example

```

> (keywords)

.:  {\\%eternity \\%false \\%impossible \\%indefinite \\%infinity \\%neternity \\%ninfinity \\%true \\%undefined \\%unknown}

```

##### Related

is

## knew

Finds or creates a thought.

##### Syntax

(knew _relation_ _criterion_ _…_ )

_criterion_ ::= _slot referent_

_criterion_ ::= _method function_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| relation | relation | 1   | The name of the relation to find |
| criterion | expression | 0+  | A slot referent pair or method function pair. |

##### Results

| Data Type | Description |
| --- | --- |
| thought | A known or new thought. |

##### Remarks

Looks for an existing thought that matches the criteria and returns the first match. If no thought matches the criteria, a new thought is created using the criteria.

##### Example

```

> (relation Pairs :A :B)

.:  Idea

> (knew Pairs :A 1 :B 2)

.:  Pairs_1

> (knew Pairs :A 1)

.:  Pairs_1

> (knew Pairs :B 3)

.:  Pairs_2

```

##### Related

new, relation

## knowledge

Finds or creates a knowledge base.

##### Syntax

(knowledge _option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 0+  | Key value pair. Any of the following<br><br>name _name_ \- A literal to identify the knowlebge base.<br><br>Options for constructing a local knowledge base<br><br>path _string_ \- the local path (required if constructing).<br><br>unit _literal_ \- either TB, GB, MB (default)<br><br>size _real_ \- the initial knowledge base (default is 5).<br><br>max _real_ \- maximum kb size (default is nil)<br><br>log _real_ \- initial log size. (default is 2).<br><br>growth _real_ \- Resize percentage (default is 10).<br><br>Options for connecting to an existing knowledge base<br><br>connect _string_ - use the specified connection string.<br><br>poolsize _integer_ \- maximum # of connections<br><br>provider _literal_ - either mssql, odbc, maria, pgsql<br><br>Options for building the connection string from elements.<br><br>driver _string_ - the driver<br><br>server _string_ \- server address<br><br>version _number_ - server version<br><br>class _class_ - class name of driver<br><br>host _address_ \- host address<br><br>port _port_ \- server port for database service<br><br>instance _instance_ \- server instance name<br><br>integratedSecurity _truth_ \- true or false<br><br>database _name_ - database name<br><br>user _username_ - user name<br><br>password _password_ - user password<br><br>trusted _yesorno_ - trusted connection yes or no.<br><br>source _name_ - data source name<br><br>protocol _protocol_ - database protocol<br><br>subprotocol _subprotocol_ - database sub protocol<br><br>subname _subname_ - sub name |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the new knowledge base. |

##### Remarks

If path is provided, then name is required. If data is provided then a knowledge base must already exist at the specified data url.

##### Example

```

> (knowledge provider mssql connect "Data Source=MYHOST\\SERVER; Initial Catalog=MyKB; Integrated Security=SSPI;")

.:  Knowledge-1

> (knowledge name Mathematics path "c:/premise/kb/" units MB size 2 max 10

log 1 growth 10)

.:  Mathematics

```

##### Related

attach, conceive, detach, each, eradicate, knew, knowing, new, relation, which, with

## known

True if a SubThought pattern matches.

##### Syntax

(known _pattern_ _…_ _option_ _…_ )

_pattern_ ::= \[_relation clause …_\]

_clause_ ::= _slot referent_

_clause_ ::= _slot_ is _unary-predicate_

_clause_ ::= _slot_ not _referent_

_clause_ ::= _slot binary-predicate referent_

_clause_ ::= _slot n-ary-predicate referent-list_

_clause_ ::= _method function_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| pattern | expression | 0+  | A relation clause pattern enclosed in square brackets. |
| option | expression | 0-2 | Key value pairs:<br><br>limit number - maximum number of thoughts to match.<br><br>scan number - maximum number of thoughts to search. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns whether any thoughts matched. |

##### Remarks

Looks for existing thoughts matching the criteria.

##### Example

```

> (relation Pairs :A :B)

.:  Pairs

> (new Pairs :A 1 :B 2)(new Pairs :A 3 :B 4)(new Pairs :A 5 :B 2)

.:  Pairs_1 Pairs_2 Pairs_3

> (known \[Pairs :B 2\] limit 1)

.:  true

```

##### Related

knew, new, relation, the, with

## lacks

True if a key is absent from an assortment.

##### Syntax

(lacks _assortment key_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| key | variant | 1   | A key. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the key is absent or false if the key is present. |

##### Remarks

None

##### Example

```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.:  Lexicon-1

> (lacks Lexicon-1 :C)

.:  false

> (lacks Lexicon-1 !m)

.:  false

> (lacks Lexicon-1 !q)

.:  true

```

##### Related

beyond, has, within

## last

Creates a subsequence of the last elements.

##### Syntax

(last _sequence count_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |
| count | number | 0-1 | The number of elements to return. Default is 1. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The selected sub sequence |

##### Remarks

None

##### Example

```

> (last {a b c})

.:  {c}

> (last {a b c d e f} 3)

.:  {d e f}

> (last "abcde" 2)

.:  "de"

```

##### Related

but, rest, top

## left

True if values are equal or the second value is nil.

##### Syntax

(left _first_ _second_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| first | variant | 1   | A value to be compared. |
| second | variant | 1   | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are the same or if second is nil |

##### Remarks

Returns true if each value is the same or if the second value is nil, and false otherwise. Both values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equal if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical). Returns false if both values are false.

##### Example

```

> (left a a)

.:  true

> (left "johnny" "ralph")

.:  false

> (left 3 nil)

.:  true

> (left nil 4)

.:  false

```

##### Related

< _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal_, full, identical, right

## let

Adds variables to the current environment.

##### Syntax

(let _manner assignment_ _..._ )

_assignment ::= symbol value_

_assignment ::=_ {_symbol_ _..._ } _list_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed<br><br>either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| Truth | Returns true. |

##### Remarks

Sequentially creates variables in the current environment. Each symbol shall replace any extant symbol with the same name in the environment. . If parallel is specified as the manner, the variables are defined in parallel, otherwise the variables are assigned in tandem (by default).

##### Example

```

> (let ?person DrWho)

.:  true

> ?person

.:  DrWho

> (let parallel ?x 1 ?y 2 ?z 3)

.:  true

```

##### Related

<-- _before tie_, --> _after tie_, constant, dynamic, fix, global, local, set, tie

## lexemes

Creates an uppercase string with spaces between words.

##### Syntax

(lexemes _string_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A string to be converted |

##### Results

| Data Type | Description |
| --- | --- |
| string | A converted string. |

##### Remarks

Converts a string to uppercase with a single space between alphanumeric words. Removes punctuation.

##### Example

```

> (lexemes "The quick brown fox!! ")

.:  "THE QUICK BROWN FOX"

```

##### Related

char, format, lexemes, like, lowercase, ngrams, split, trim, unlike, unicode, uppercase

## lexicon

Creates a lexicon.

##### Syntax

(lexicon _association_ _…_ )

_association ::= key value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| association | expression | 0+  | A key and a value. |

##### Results

| Data Type | Description |
| --- | --- |
| lexicon | The newly created lexicon. |

##### Remarks

None.

##### Example

```

> (lexicon {a b c} "foo 123" bar "bar 456" baz (lexicon))

.:  Lexicon-2

> (keys Lexicon-2)

.:  {{a b c} bar baz}

> (values Lexicon-2)

.:  {"foo 123" "bar 456" Lexicon-1}

> (@ Lexicon-2 {a b c})

.:  "foo 123"

> (key Lexicon-2 Lexicon-1)

.:  baz

```

##### Related

lexicon

## lexicons

Creates a list of all lexicons.

##### Syntax

(lexicons)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list of lexicons. |

##### Remarks

None.

##### Example

```

> (lexicons)

.:  {}

> (lexicon k1 v1 k2 v2)

.:  Lexicon-1

> (lexicons)

.:  {Lexicon-1}

```

##### Related

lexicon

## license

Prints the software license.

##### Syntax

(license)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| nil | nil |

##### Remarks

None.

##### Example

```

> (license)

Premise Community Edition

Copyright (c) 2013-2025 SubThought Corporation. All Rights Reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of the Community edition of the software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

.:  nil

```

##### Related

about, bye, copyright

## like

Compares a pattern to a sequence.

##### Syntax

(like _sequence pattern_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A string or list of strings to be compared. |
| pattern | string | 1   | A regex pattern. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | If sequence is a string, then a truth is returned.<br><br>If sequence is a list, then a list of matches is returned |

##### Remarks

If the sequence is a list, then this function Creates a new list containing only those elements matching the pattern. If the sequence is a string, then this function returns true if the pattern matches the candidate, and false otherwise. Standard regular expression matching is used.

##### Example

```

> (like "abc" "bc")

.:  true

> (like "abc" "\[xy\]")

.:  false

> (like {"abc" "def" "xyz" "wxy"} "xy")

.:  {"xyz" "wxy"}

```

##### Related

unlike

## list

Creates a list.

##### Syntax

(list _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | Any value |

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list containing the values. |

##### Remarks

A list can also be created by simply enclosing the elements with curly braces, {}.

##### Example

```

> (list a b c {d})

.:  {a b c {d}}

> (list "a b c")

.:  {"a b c"}

> (list 500)

.:  {500}

> (list foo)

.:  {foo}

> {a b c {d}}

.:  {a b c {d}}

> {"a b c"}

.:  {"a b c"}

```

##### Related

& _merge_, && _abridge_, inside, vector

## literal

Creates a literal.

##### Syntax

(literal _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A string or literal to be converted. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | A literal. |

##### Remarks

Only strings or literals can be converted to a literal. sequences, numbers and variables cannot be converted to literals. This function fails if the value cannot be converted.

##### Example

```

> (literal abc)

.:  abc

> (literal 500)

.:  \[Failure :Name ArgumentValue :Text "Cannot convert '500' to a literal."\]

> (literal "500")

.:  \[Failure :Name ArgumentValue :Text "Cannot convert '500' to a literal."\]

> (literal "foo")

.:  foo

> (literal (symbol bar))

.:  \[Failure :Name ArgumentValue :Text "Cannot convert '?bar' to a literal."\]

```

##### Related

is

## local

Creates a task level scope.

##### Syntax

(local _assignments expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assignments | list | 1   | A list of symbol value pairs |
| expression | variant | 0+  | An expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true. |

##### Remarks

The new variables shall shadow any existing variables with the same name.

##### Example

```

> (function appendToFile {& ?messages}

(local {?file (file name "myfile.out")}

(try

(seek ?file #)

(for ?s in ?messages (write ?file ?s))

(close ?file)

appended

learn ?e

(may (close ?file)) ; surpress further failure

?e)))

.:  appendToFile

```

##### Related

<-- _before tie_, --> _after tie_, constant, dynamic, given, global, only, set

## location

Sets a symbol to the current location.

##### Syntax

(location _symbol_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol to contain the location. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result value. |

##### Remarks

This function saves the present program location in a symbol. A subsequent resume call shall reset the location to the one in the symbol for the program control to resume at the location.

##### Example

```

> (function makeSandwich {?where}

(tell user "Made a sandwich.\\n")

(proceed ?where set ?sandwich made))

.:  makeSandwich

> (function eatSandwich

(tell user "Ate the sandwich.\\n"))

.:  eatSandwich

> (do

(let ?sandwich none)

(location ?kitchen)

(if (= ?sandwich made)

(eatSandwich)

else

(makeSandwich ?kitchen)))

Made a sandwich.

Ate the sandwich.

.:  told

```

##### Related

resume, go

## log

Logarithm.

##### Syntax

(log _number base_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| base | number | 1   | The base. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The logarithm |

##### Remarks

Returns the logarithm of the number for a base.

##### Example

```

> (log 100 10)

.:  2

> (log 27 3)

.:  3

> (log 22026.31763368418 (e))

.:  10

```

##### Related

** _exponentiation_

## long

Converts a value to a long number.

##### Syntax

(long _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Data Type | Description |
| --- | --- |
| long | An long number. |

##### Remarks

A long is a signed 128 bit number. If the value is minimum (or maximum) the minimum (or maximum) monadic is returned; otherwise, if the value cannot be converted to a monadic, the function fails. The fractional part of the number is truncated. The suffix n denotes a long number.

##### Example

```

> (long {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (long "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not a number."\]

> (long 500)

.:  500n

> (long 500.0)

.:  500n

> (long "23.4")

.:  23n

```

##### Related

big, integer

## loop

Repeatedly evaluates expressions.

##### Syntax

(loop _expression_ _…_ _gate_ )

_gate ::=_ repeat _integer_

_gate ::=_ until _truth_

_gate ::=_ while _truth_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 0+  | Expressions to be evaluated. |
| gate | expression | 1   | the literal while or until followed by a truth expression, or the literal repeat followed by an integer. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the value of the last executed expression before the gate. |

##### Remarks

Each expression is executed in succession and the value of the last expression before te gate is returned. This function repeats the expression(s) according to the gate. If until is specified, the iteration fails when the condition becomes true. If while is specified, the iteration fails when the condition becomes false. If repeat and an integer value is specified as the gate, then the iteration repeats for the number of times in the integer value. The gate may be omitted to iterate only once.

##### Example

```

> (loop (--> ++ ?i) while (< ?i 10))

.:  10

> (loop (--> -- ?i) until (< ?i 1))

.:  0

> (loop (--> ++ ?i) repeat 10)

.:  10

```

##### Related

wait, abort,, await, complete, done-p, reclaim, use, for, iterate, loop, step, task, until, while

## lowercase

Converts a string to lower case.

##### Syntax

(lowercase _string_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A string |

##### Results

| Data Type | Description |
| --- | --- |
| string | The lower cased string |

##### Remarks

None

##### Example

```

> (lowercase "The Quick BROWN fox")

.:  "the quick brown fox"

```

##### Related

capitalize, uppercase

## lowercase-p

Returns true if a string's first position is lower case.

##### Syntax

(lowercase-p _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the first position is lowercase. |

##### Remarks

None

##### Example

```

> (lowercase-p "the quick brown fox")

.:  true

> (lowercase-p "This and that")

.:  false

```

##### Related

letter-p, lowercase-p, uppercase-p, whitespace-p

## macro

Creates a macro.

##### Syntax

(macro _name parameters expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | A macro name |
| parameters | list | 1   | A parameter list |
| expression | variant | 1+  | Forms to be evaluated |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value in the list of frames |

##### Remarks

A macro is a function whose parameters are unevaluated. To evaluate any of the parameters, the eval function must explicity be called on that parameter.

##### Example

```

> (macro set2 {?value ?var1 ?var2}

"puts value into two variables in parallel"

(eval (\` (set , ?var1 , ?value , ?var2 , ?value))))

.:  set2

> (let ?x1 nil ?x2 nil) ?x1 ?x2

.:  true nil nil

(set2 (+ 2 2) ?x1 ?x2)

> ?x1 ?x2

.:  4 4

```

##### Related

evaluate, function, ' _quote_, \` _expand_

## macros

Creates a list of macros defined in a module.

##### Syntax

(macros _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A valid module name. Defaults to the current module. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of macros defined in the module. |

##### Remarks

##### None.

##### Example

```

> (macro set2 {?s1 ?s2 ?value}

(eval (\` (set , ?s1 , ?value , ?s2 , ?value))))

.:  set2

> (macros)

.:  {set2}

```

##### Related

\` _expand_, ' _quote_, eval, functions, is, macro

## make

Creates a record by creating a relationship if it does not already exist.

##### Syntax

(make _prototype_ _term_ _…_ )

_term_ ::= _slot_ _referent_

_term_ ::= _method_ _function_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| prototype | prototype | 1   | A relation or structure. |
| term | expression | 0+  | A slot and a referent, or method and function. |

##### Results

| Data Type | Description |
| --- | --- |
| identifier | The identifier of the premise |

##### Remarks

If the prototype is a relation which has has an !onNew method defined, the method shall be invoked once during SubThought creation, before the SubThought identifier is returned to the calling function. If the relationship is new, the referents and functions shall serve as defaults for the relationship.

##### Example

```

> (make Employee :Name "John Smith" :Salary 225000

!onNew (function Employee_new {?me}

(tell user ($ Emp - ($$ (:Name ?me),)

Pay - (:Salary ?me) \\n \\n)))))

Emp - John Smith, Pay – 225000

.:  Employee_1

```

##### Related

nix, old, relation, seal, unseal

## map

Applies a function to elements across sequences.

##### Syntax

(map _sequence_ _..._ _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1+  | A sequence of values |
| function | variant | 1   | The name of the function to invoke |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The sequence resulting from applying the function to all sequences. |

##### Remarks

Applies the argument to a list containing values and returns the results.

##### Example

```

> (map {1 2 3} {4 5 6} {7 8 9} +)

.:  {12 15 18}

> (map {1 2 3} even-p)

.:  {false true false}

> (map {10 20 30} {3 4 5} \*)

.:  {30 80 150}

```

##### Related

apply, collect, count, each, filter, fold, gather, group, merge, reduce , scale , separate, sort

## max

Finds the maximum element.

##### Syntax

(max _value_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A sequence, or an atomic value. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The largest element in the sequence. |

##### Remarks

Returns the maximum element in a list or expression. If the list or expression is empty, it returns nil. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example

```

> (max {1 2 3 4 5})

.:  5

> (max {a b c d e})

.:  e

> (max {})

.:  nil

  
\> (max 1 2 3 4 5)

.:  5

> (max {1 2 3} 4 {6 3 2})

.:  {6 4 4}

```

##### Related

choose, min

## maximum

Finds the maximum element.

##### Syntax

(maximum _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result of applying the max function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the variables then the function fails. The last expression shall be evaluated and the maximum function shall be applied to both that expression and any prior result. The final value is returned.

##### Example

```

> (maximum ?x in (range 1 to 10) ?x)

.:  10

> (maximum ?x in {1 2 3 4} (** ?x 2))

.:  16

> (maximum ?x ?y per {{a 1}{b 2}{c 3}} ?x)

.:  c

```

##### Related

fold, minimum, product, summation

## may

Evaluates an expression while surpressing failures.

##### Syntax

(may _expression_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | An expression to evaluate. |

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list containing a truth success value, the result, and possible failure. |

##### Remarks

If the expression fails, the result shall be nil.

##### Example

```

> (may (string x))

.:  {true "x" nil}

> (may (integer x))

.:  {false nil \[Failure :Name TypeConversion :Text "Cannot convert x to Integer"\]}

> (let {?success ?result ?error} (may ($ hello world)))

.:  true

> ?success ?result ?error

.:  true "hello world" nil

```

##### Related

assert, can, did, ensure, fail, finally, try

## median

Finds the middle value of a sequence.

##### Syntax

(median _value_ _…_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The median value of all elements. |

##### Remarks

Returns the median. If the list or expression is empty, it returns nil. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example

```

> (median {1 2 3 4 5})

.:  3

> (median {})

.:  nil

> (median 1 2 3 4 5)

.:  3

> (median {1 2 3} 4 {6 3 2})

.:  {4 3 3}

```

##### Related

avg, max, median, min, statistics, sigma, sum

## meets-p

True if an interval finishes when a second interval starts.

##### Syntax

(meets-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if interval1 finishes when interval2 starts. |

##### Remarks

None.

##### Example

```

> (meets-p \\@i{\\@s1 \\@s2} \\@i{\\@s3 \\@s4})

.:  false

> (meets-p \\@i{\\@s1 \\@s5} \\@i{\\@s5 \\@s8})

.:  true

> (meets-p \\@i{\\@s1 \\@s9} \\@i{\\@s4 \\@s6})

.:  false

> (meets-p \\@i{\\@s4 \\@s6} \\@i{\\@s6 \\@s9})

.:  true

> (meets-p \\@i{\\@s5 \\@s6} \\@i{\\@s8 \\@s9} \\@s2)

.:  true

```

##### Related

before-p, during-p, finishes-p, overlaps-p, starts-p

## meron

Returns the meronomic (i.e., proto) type of a value.

##### Syntax

(meron _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A structure, relation, or premise |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The meronomic prototype of the relation |

##### Remarks

None

##### Example

```

> (meron (relation A))

.:  A

> (meron (new (structure B :Slot1 :Slot2)))

.:  B

> (meron 100)

.:  nil

> (meron foo)

.:  nil

> (meron (new (relation C uses {A B})))

> C

> (meron \[D :Foo 1 :Bar 2\])

> D

```

##### Related

id, is, meronomy,, taxon, taxonomy

## meron-p

True if the value isa meron or is of a specific meronomic type.

##### Syntax

(meron-p _value_ _meron_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |
| meron | literal | 0-1 | The name of a meronomic type. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is a meron or is of a specific meronomic type.. |

##### Remarks

If the meron parameter is omitted, the functon returns true if the value is a meron. Otherwise, the function returns true if the value is of the specified meronomic type. .

##### Example

```

> (meron-p 500)

.:  false

> (relation A :S1 :S2 0) (relation B uses {A} :S3 100)

.:  A B

> (meron-p (new A))

.:  true

> (meron-p (new B) A)

.:  true

```

##### Related

meron, meronomy, taxon, taxon-p, taxonomy

## meronomy

Returns a list of meronomic (i.e., proto) types for a value.

##### Syntax

(meronomy _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |

##### Results

| Data Type | Description |
| --- | --- |
| list | The meronomic types used |

##### Remarks

The value must be a premise, prototype, or record , otherwise an empty list is returned

##### Example

```

> (meronomy 100)

.:  {}

> (meronomy donut)

.:  {}

> (relation C uses {(relation A) (relation B)})

.:  C

> (meronomy (new C))

.:  {C A B}

> (meronomy A)

.:  {A}

```

##### Related

taxon,taxonomy, id, is, meron, relation, structure

## method

Creates a function within a prototype.

##### Syntax

(method _scope name parameters expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied, a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Methods are defined using the method intrinsic function. If the name is supplied then the method is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided. The first variables in the parameter list are required. If a plus sign is provided, then those variables following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined. A hidden variant parameter ?me is supplied as the first parameter to the method function and is available within the method for reading. It may not be upadted or changed in the scope of the method.

##### Example

```

> (relation Context_Items

:Lexicon

:Item )

.:  Context_Item

> (relation MyLexicon

:Name

:Context {}

!refreshContext

(method {}

(let ?me :Name ?lexicon :Context ?context)

(with Context_Item :Lexicon = ?lexicon :Item as ?Item

(out ?item ?context)

do (zap Context_Item :Lexicon ?lexicon :Item ?item)

(for ?item in ?context

(knew Context_Item :Lexicon ?lexicon :Item ?item))))

.:  MyLexicon

> (structure IMonsterTask

:Name

!setInfo

!setRoomTask

:RoomTask

!kill )

.:  IMonstertask

> (structure MonsterTask

uses {IMonsterTask}

:MonsterInfo (new MonsterInfo)

!onActivate (method {truth ?cancelled}

(put ?me :Id (!getPrimaryKey ?me))

(registerTimer move nil (interval \\@s150 \\@s9000))

)

!setInfo (method {MonsterInfo ?info}

(put ?me :MonsterInfo ?info)

(return done))

!name (method {} (get ?me :MonsterInfo :Name ))

!setRoomTask (method {RoomTask ?room}

(if (exists-p (:RoomTask ?me))

(await (!exit (:RoomTask ?me))))

(put ?me :RoomTask ?room)

(!enter (:RoomTask (:MonsterInfo ?me))))

!move (method {}

(if (exsist-p (:RoomTask ?me))

(let ?directions {north south west east}

?random (random 0 to 4)

?nextRoom (await (!exitTo (:RoomTask ?me)

(@ ?directions ?random))))

(if (null-p ?nextRoom) (return nil))

(await (!exit (:RoomTask ?me) (:MonsterInfo ?me)))

(await (!enter ?nextRoom (:MonsterInfo ?me)))

(put ?me :RoomTask ?nextRoom)))

!kill (method {RoomTask ?room}

(if (exists-p (:RoomTask ?me))

(return (on (/= (get ?me :RoomTask :PrimaryKey)

(get ?room :PrimaryKey))

(tell User ($ (!name (:MonsterInfo ?me)) snuck away.

You were too slow!))

(do (!exit (:RoomTask ?me))

(tell User ($ (!name (:MonsterInfo ?me)) is dead.))))

(return (tell User ($ (!name (:MonsterInfo ?me)) is already dead. \\n

You were too slow and someone else got to

him.)))))

.:  MonsterTask

```

##### Related

arguments, call, extend, functions, junction, macro, module, modules, parameters

## mid

Copies a subsequence of a sequence.

##### Syntax

(mid _sequence start stop skip_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | sequence |
| start | number | 1   | Starting position |
| stop | expression | 1   | One of to _finish_ or go _count_ |
| skip | expression | 0-1 | Key value pairs<br><br>by _count_ – skips a number of elements<br><br>The expression by _count_ default is 1. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The sub-sequence |

##### Remarks

The _end_ value must be greater than the _start_ value.

##### Example

```

> (mid {a b c d} 2 to 3)

.:  {b c}

> (mid "abcdefg" 4 go 4)

.:  "defg"

> (mid "abcdefg" 2 to 4)

.:  "bcd"

> (mid "abcdefg" 2 go 3 by 2)

.:  "bd"

```

##### Related

but, last, rest, top

## min

Finds the minimum element.

##### Syntax

(min _value_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | An atom or list of atoms. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The smallest element in the sequence. |

##### Remarks

Returns the minimum element in a list or expression. If the list or expression is empty, it returns nil. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example

```

> (min {1 2 3 4 5})

.:  1

> (min {a b c d e})

.:  a

> (min {})

.:  nil

  
\> (min 1 2 3 4 5)

.:  1

> (min {1 2 3} 4 {6 3 2})

.:  {1 2 2}

```

##### Related

choose, max

## minimum

Finds the minimum element.

##### Syntax

(minimum _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result of applying the plus function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the variables then the function fails. The last expression shall be evaluated and the minimum function shall be applied to both that expression and any prior result. The final value is returned.

##### Example

```

> (minimum ?x in (range 1 to 10) ?x)

.:  1

> (minimum ?x in {1 2 3 4} (** ?x 2))

.:  1

> (maximum ?x ?y per {{a 1}{b 2}{c 3}} ?x)

.:  a

```

##### Related

fold, maximum, minimum, product

## missing

True if a value is absent from an assortment.

##### Syntax

(missing _assortment key_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| vaue | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the value is absent or false if the value is present. |

##### Remarks

None

##### Example

```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.:  Lexicon-1

> (missing Lexicon-1 3)

.:  false

> (missing Lexicon-1 X_foo)

.:  false

> (missing Lexicon-1 elephant)

.:  true

```

##### Related

beyond, has, within

## mod

Finds the remainder after division.

##### Syntax

(mod _dividend_ _modulus_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number or list of numbers. |
| modulus | variant | 1   | A number or list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | the remainder after dividing dividend by divisor as a number or list of remainders. |

##### Remarks

Returns the remainder of the dividend divided by the modulus. Both values must be numbers or lists. If each argument is a list, they must be the same length.

##### Example

```

> (mod 28 3)

.:  1

> (mod {6 8 9 2} 2)

.:  {0 0 1 0}

> (mod 17 {5 6 3 4})

.:  {2 5 2 1}

> (mod {12 45 8 17} {5 5 3 7})

.:  {2 0 2 3}

```

##### Related

/ division, \* multiplication

## modular

Evaluates expressions within a module's scope.

##### Syntax

(modular _module expression_ _…_ )

_assignment_ ::= _symbol value_ expression

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | Literal | 1   | A module name |
| expression | variant | 1+  | An expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates module level variables.

##### Example

```

> (modular User (let ?START_OF_TASK 1))

.:  true

> (modular Business

(let ?FIRST_NAME Jane

?LAST_NAME Smith))

.:  true

```

##### Related

<-- _before tie_, --> _after tie_, constant, dynamic, local, put, suppose, swap, undefine, use

## module

Creates a module.

##### Syntax

(module _name definition_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | A module name |
| definition | expression | 0+  | A function, macro, or relation definition call |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the module. |

##### Remarks

Shall create a new module or redefine an existing module. To add definitions to an existing module use the extend function. To prohibit new definitions in a module use the wrap function. Each module is global, this means that nested module definitions do not concatenate.

##### Example

```

> (module Algebra

(function sum ?args (apply + ?args)))

.:  Algebra

> (module Outer

(module Inner

(function Which {} One) ; the function shall be Inner.Which

)

)

.:  Outer

> (Inner.Which)

.:  One

```

##### Related

dependencies, discard, extend, forgo, modules, require, grok, unwrap, use, wrap

## modules

Creates a list of known modules.

##### Syntax

(modules)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of all modules |

##### Remarks

Returns the list of known modules.

##### Example

```

> (modules)

.:  {Apex Base IO KB Math Tasks User}

```

##### Related

dependencies, discard, extend, forgo, module, require, grok, unwrap, use, wrap

## moment

Creates a moment or returns the current moment.

##### Syntax

(moment _units secs mins hours days year_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| units | number | 0-1 | Units. Up to three digits for milliseconds. |
| secs | number | 0-1 | Two digits: e.g., (seconds / 60) \* 100 |
| min | number | 0-1 | Two digits: e.g., (minutes / 60) \* 100 |
| hour | number | 0-1 | Two digits: e.g., (hour / 24) \* 100 |
| days | number | 0-1 | Three digits e.g. (day of year / 365.25) x 1000 |
| year | variant | 0-1 | Four digits for year (e.g. 2015, 2017, 2018, 2025) |

##### Results

| Data Type | Description |
| --- | --- |
| moment | The current moment in nano years |

##### Remarks

If no arguments are supplied, moment returns the current time as a moment, otherwise it attempts to construct a moment from the supplied arguments.

##### Example

```

> (moment)

.:  \\@m2018270038501744

> (moment 3000)

.:  \\@m3000

> (moment 0 0 0 0 0 2020)

.:  \\@m2020000000000000

> (moment 0 0 0 (time hour part 18) (time days part 182) 2027)

.:  \\@m2027499030000000

```

##### Related

date, epoch, tick

## more-p

True if a container contains more than zero elements.

##### Syntax

(more-p _sequence_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the container contains more than zero elements. |

##### Remarks

None.

##### Example

```

> (more-p "not empty")

.:  true

> (more-p (call pi))

.:  true

> (more-p "")

.:  false

> (more-p {})

.:  false

> (more-p \[A\])

.:  true

> (more-p (expression foo))

.:  true

```

##### Related

void-p

## morph

Applies functions in succession using the arguments.

##### Syntax

(morph _arguments functions_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| arguments | list | 1   | The intial arguments to the last function in the functions list. |
| functions | list | 1   | An ordered list of functions to be applied. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The result of the application of the last function. |

##### Remarks

If the arguments parameter is an empty list, the leftmost function is assumed to be niladic (requiring no arguments). The leftmost function is applied to the arguments parameter list, then the second from leftmost is applied to the result, and so on, until all functions are applied. The final result is returned. The opposite function is compose. The scatter function applies functions in parallel.

##### Example

```

> (morph {0} {++ ++ ++ (given {?n} (\* ?n 2))})

.:  6

> (morph {{the quick brown fox jumped over the lazy dogs}}

{but rest but rest})

.:  {brown fox jumped over the}

> (morph {2 3 4} {+ ++ ++ (given {?n} (\* ?n 2))})

.:  22

```

##### Related

apply, compose, map, scatter

## most

True if the predicate is true for more than half of the elements in a sequence.

##### Syntax

(most _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if more than half the elements satisfies the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated.

##### Example

```

> (most ?n in {1 2 3 4} (= (taxon ?n) number))

.:  true

> (most ?m ?n per {{2 1} {3 4} {7 9}} (< ?m ?n))

.:  true

> (most ?m ?n over {4 3 2 7} (divisible-p ?m ?n))

.:  false

```

##### Related

every, few, nevery, none, some

## move

Moves or renames one or more files.

##### Syntax

(move _source destination_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| source | url | 1   | The source url |
| destination | url | 1   | The destination url |

##### Results

| Data Type | Description |
| --- | --- |
| list | A possibly empty list of file path strings for each file moved. |

##### Remarks

If the path is invalid, the function fails.

##### Example

```

> (move (url path "foo.txt") (url path "bar.txt"))

.:  {"bar.txt"}

```

##### Related

close, mkdir, file, path, write

## my

Returns the current cell resource.

##### Syntax

(my)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| cell | The cell resource for the performing functions. |

##### Remarks

None.

##### Example

```

> (my)

.:  Cell-0

> (get (my) :Self)

.:  Task-0

```

##### Related

premise, self

## nall

True if not all relevant knwledege satisfies all the premises.

##### Syntax

(nall _premise_ … )

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= as _symbol_

_binding_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _value_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| premise | variant | 1+  | A pattern, call, or truth value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if not all values return true. |

##### Remarks

True if any value is nil. Terminates on the first nil value. If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.

##### Example

```

> (nall grapefruit nil apple)

.:  true

> (nall nil nil)

.:  true

> (nall nil)

.:  true

> (nall foo)

.:  false

```

##### Related

all, any, no

## nand

Negated logical conjunction.

##### Syntax

(nand _truth truth_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | truth | 2+  | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if any argument value is false |

##### Remarks

Equivalent to (not (and truth …)).

##### Example

```

> (nand true true true false)

.:  true

> (nand true true true true)

.:  false

```

##### Related

and, is, nor, not, or, xor

## negative-p

True if a number is negative.

##### Syntax

(negative-p _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the number is less than zero. |

##### Remarks

None.

##### Example

```

> (negative-p 500)

.:  false

> (negative-p 0)

.:  false

> (negative-p -25)

.:  true

```

##### Related

even-p, odd-p, positive-p, zero-p

## nevery

True if the predicate is false for any element in the sequence.

##### Syntax

(nevery _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if any element does not satisfy the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example

```

> (nevery ?n in {1 a 3 4} (= (taxon ?n) number))

.:  true

> (nevery ?m ?n per {{1 2} {3 4}} (> ?m ?n))

.:  true

> (nevery ?m ?n over {4 2 1} (divisible-p ?m ?n))

.:  false

```

##### Related

every, few, most, none, some

## new

Creates a record.

##### Syntax

(new _prototype_ _term_ _…_ )

_term_ ::= _slot_ _referent_

_term_ ::= _method_ _function_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| prototype | prototype | 1   | A relation or structure. |
| term | expression | 0+  | A slot and a referent, or method and function. |

##### Results

| Data Type | Description |
| --- | --- |
| identifier | The identifier of the premise |

##### Remarks

If the prototype is a relation which has has an !onNew method defined, the method shall be invoked once during SubThought creation, before the SubThought identifier is returned to the calling function.

##### Example

```

> (relation Employee :Name :Salary

!onNew (function Employee_new {?me}

(tell user ($ Emp - ($$ (:Name ?me),)

Pay - (:Salary ?me) \\n \\n)))))

.:  Employee

> (new Employee :Name "John Smith" :Salary 225000)

Emp - John Smith, Pay – 225000

.:  Employee_1

```

##### Related

nix, old, relation, seal, unseal

## next

Advances a series to the next element.

##### Syntax

(next _series_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| series | series | 1   | A series. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the next item in the iteration can be accessed. |

##### Remarks

None.

##### Example

```

> (function walk {?iterable}

(let ?series (series ?iterable))

(while (next ?series)

(tell user ($ Found ($$ (this ?series) .) \\n)))

walked)

.:  walk

> (walk {a b c})

Found a.

Found b.

Found c.

.:  walked

> (walk (lexicon a 1 b 2 c 3))

Found {a 1}.

Found {b 2}.

Found {c 3}.

.:  walked

```

##### Related

reset, series, this

## ngrams

Creates a list of substrings.

##### Syntax

(ngrams _string_ _length_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A target string |
| length | integer | 0-1 | The length of substrings to find. (Default is 3.) |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of strings of the specified length |

##### Remarks

Affixes spaces before and after the string, then divides the string into substrings of the specified length.

##### Example

```

> (ngrams "fox" 3)

.:  {" f" " fo" "fox" "ox " "x "}

> (ngrams "fox")

.:  {" f" " fo" "fox" "ox " "x "}

> (ngrams "fox" 5)

.:  {" f" " fo" " fox" " fox " "fox " "ox " "x "}

```

##### Related

lexemes, split, trim

## nil-p

True if a value is nil.

##### Syntax

(nil-p _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the values is nil. |

##### Remarks

None.

##### Example

```

> (nil-p yes)

.:  false

> (nil-p \\%nil)

.:  true

> (nil-p (nothing))

.:  false

> (nil-p \\%void)

.:  false

> (nil-p nil)

.:  true

```

##### Related

exists-p

## nix

Deletes a prototype.

##### Syntax

(nix _prototype_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| prototype | prototype | 1+  | A prototype or list of prototypes. |

##### Results

| Data Type | Description |
| --- | --- |
| expression | Returns the literal nixed and the quantity deleted. |

##### Remarks

Undeclares a prototype. All thoughts of the relation must be reclaimed with the old function first, otherwise the function fails.

##### Example

```

> (new (relation Q))

.:  Q_1

> (nix Q)

.:  \[Failure :Name InvalidOperation :Text "Cannot nix relations having thoughts."\]

> (do (with Q ^ as ?q do (old ?q)) (nix Q))

.:  nixed 1

> (is Q (given {?r} (more-p (meronomy ?r)))

.:  false

> (new (relation P))

.:  P_1

> (do (old (with P)) (nix P))

.:  nixed 1

```

##### Related

structure, structures, old, relation, relations, seal, unseal

## no

True if no relevant knowledge satisfies all of the premises.

##### Syntax

(no _premise_ _…_ )

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= as _symbol_

_binding_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _value_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A pattern, call, or ruth value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all the values are nil. |

##### Remarks

Equivalent to (not (any premise …)). If the value is a pattern or a relationship, then a cursor is created over which the remaining values are tested until truth or falsity is determined. If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.

##### Example

```

> (no one two three)

.:  false

> (no a b nil)

.:  false

> (no nil nil nil)

.:  true

```

##### Related

all, any, default, nall

## none

True if the predicate is false for all sequence elements.

##### Syntax

(none _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | variant | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if every element does not satisfy the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example

```

> (none ?n in {1 2 3 4} (alphabetic-p ?n))

.:  true

> (none ?m ?n per {{1 2} {3 4}} (< ?m ?n))

.:  true

> (none ?m ?n over {4 2 1} (divisible-p ?m ?n))

.:  false

```

##### Related

every, few, most, nevery, some

## nor

Negated logical disjunction.

##### Syntax

(nor _truth truth_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 1+  | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all argument values are false |

##### Remarks

Equivalent to (not (or value value …)).

##### Example

```

> (nor true true true false)

.:  false

> (nor true true true true)

.:  false

> (nor false false false false)

.:  true

```

##### Related

and, nand, not, or, xnor, xor

## not

True if the value is false, or if the applied unary predicate returns false.

##### Syntax

(not _value_ _predicate_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| predicate | literal | 0-1 | A unary predicate |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if value is false, or if the applied unary predicate returns false. |

##### Remarks

None.

##### Example

```

> (not false)

.:  true

> (not true)

.:  false

> (not 3 even-p)

.:  true

> (not 7 (given {?n} (divisible-p ?n 3)))

.:  true

> (not foo null-p)

.:  true

> (not nil null-p)

.:  false

```

##### Related

convert, datatype, is, known, the, type

## nothing

Returns nothing.

##### Syntax

(nothing)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| nothing | A nothing value. |

##### Remarks

None.

##### Example

```

> (nothing)

.: 

> {a (nothing) b (nothing) c}

.:  {a b c}

```

##### Related

ceiling, complex, floor, is, long, radix, rational, real, round, truncate, unsigned

## null-p

True if a value is nothing or nil.

##### Syntax

(null-p _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the values is nothing or nil. |

##### Remarks

None.

##### Example

```

> (null-p yes)

.:  false

> (null-p \\%nil)

.:  true

> (null-p (nothing))

.:  true

> (null-p \\%void)

.:  true

```

##### Related

exists-p

## odd-p

True if a number is odd.

##### Syntax

(odd-p _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the number is odd. |

##### Remarks

Returns true if the number is not evenly divisible by two.

##### Example

```

> (odd-p 500)

.:  false

> (odd-p 1)

.:  true

> (odd-p -33)

.:  true

```

##### Related

even-p, negative-p, positive-p, zero-p

## old

Deletes a thought.

##### Syntax

(old _thought_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| thought | variant | 1   | A premise, thought, relation, or list of thoughs. |

##### Results

| Data Type | Description |
| --- | --- |
| expression | Returns the literal reaped and the number of thoughts deleted. |

##### Remarks

Returns the number of thought identifiers deleted. If the relation has an !onOld method defined, then the method is invoked prior to the thought being deleted.

##### Example

```

> (relation Q)

.:  Q

> (new Q)

.:  Q_1

> (new Q)

.:  Q_2

> (old Q_1)

.:  1

> (old Q)

.:  1

> (nix Q)

.:  nixed

```

##### Related

structure, new, nix, relation

## omit

Creates a new sequence with values omitted.

##### Syntax

(omit _sequence value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| value | variant | 0+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The modified assortment |

##### Remarks

A new sequence is constructed. To modify the sequence use the rip function.

##### Example

```

> (omit {a b c d e f g} a b)

.:  {c d e f g}

> (omit {a 1 nil b 2 c 3 nil nil d nil 4} nil)

.:  {a 1 b 2 c 3 d 4}

```

##### Related

Insert, pop, push

## on

Branched conditional evaluation.

##### Syntax

(on _condition_ _true-case_ _false-case_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| true-case | variant | 1   | An expression to evaluate |
| false-case | variant | 1   | An expression to evaluate |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The last value of the executed expression. |

##### Remarks

Evaluates the condition and either the true case or the false case.

##### Example

```

> (on (> 101 100) (tell user "yes") (tell user "no"))

yes .: told

> (on (< 101 100) (tell user "yes") (tell user "no"))

no .: told

```

##### Related

and, case, if, not, or, unless

## only

Creates a restricted scope.

##### Syntax

(only _variables_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| variables | list | 1   | A list of variables from the enclosing scope |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| value | Returns the last value. |

##### Remarks

Creates a new environment shadowing the designated variables in the encompassing environment and executes each of the expressions, one at a time, returning the result of the last expression. No free variables (i.e., variables not defined inside the scope or not in the symbol list) are permitted within the scope. only is equivalent to an in-line anonymous function. Changes to the variables shall not affect the enclosing scope.

##### Example

```

> (function sample {?b ?c}

(let ?a 5)

(tell user ($ given a+b= (+ ?a ?b) \\n))

(tell user ($ given a+b+c= (+ ?a ?b ?c) \\n))

(only {?a ?b}

(tell user ($ only a+b= (+ ?a ?b) \\n))

(try (tell user ($ only a+b+c= (+ ?a ?b ?c) \\n))

learn ?f (tell user ($ "?c" is not in scope \\n)))))

.:  sample

> (sample 15 30)

given a+b= 20

given a+b+c= 50

only a+b= 20

?c is not in scope

.:  told

```

##### Related

given, dynamic, local

## open

Opens a file or data url.

##### Syntax

(open _url_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A file or data url. |

##### Results

| Data Type | Description |
| --- | --- |
| url | The opened url. |

##### Remarks

Opens an file.

##### Example

```

> (var ?file (file name "kwikfox.txt"))

.:  File-1

> (open ?file)

.:  File-1

> (let ?contents (read ?file #))

.:  true

> ?contents

.:  "The quick brown fox jumped over the lazy dogs."

> (close ?file)

.:  closed

```

##### Related

close, data, file

## or

Logical disjunction.

##### Syntax

(or _truth truth_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 1+  | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if any argument value is true |

##### Remarks

Short circuits evaluation upon reaching the first true argument.

##### Example

```

(or false true false false)

.:  true

(or true true true true)

: true

(or false false false false)

.:  false

```

##### Related

and, is, nand, nor, not, xnor, xor

## out

True if a value is absent from a sequence.

##### Syntax

(out _value sequence option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| sequence | sequence | 1   | A sequence. |
| option | expression | 0-2 | A key value pair. Any of<br><br>depth _number_ \- Number or # (for any depth). Default is 1.<br><br>transform _function_ \- A function to transform the element.. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is not in the sequence. |

##### Remarks

If value and sequence are strings, then a string search is performed.

##### Example

```

> (out x {a b c d e f g})

.:  true

> (out "a" "cbazyx")

.:  false

```

##### Related

includes, excludes, in, occurrences, pick, position

## overlaps-p

True if an interval finishes after a second interval starts.

##### Syntax

(overlaps-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if interval1 finishes after interval2 starts. |

##### Remarks

None.

##### Example

```

> (overlaps-p \\@i{\\@s1 \\@s2} \\@i{\\@s3 \\@s4})

.:  false

> (overlaps-p \\@i{\\@s1 \\@s5} \\@i{\\@ss4 \\@s8})

.:  true

> (overlaps-p \\@i{\\@s1 \\@s9} \\@i{\\@s4 \\@s6})

.:  false

> (overlaps-p \\@i{\\@s4 \\@s6} \\@i{\\@s5 \\@s9})

.:  true

> (overlaps-p \\@i{\\@s3 \\@s4} \\@i{\\@s5 \\@s9 \\@s2})

.:  true

```

##### Related

before-p, during-p, finishes-p, meets-p, starts-p

## pad

Creates a new padded sequence.

##### Syntax

(pad _sequence length value side_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A string or list |
| length | number | 1   | The length of the final sequence |
| value | variant | 1   | A value to insert into the sequence |
| side | literal | 0-1 | the literal left or right (default). |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | Creates a new sequence |

##### Remarks

If the sequence is a string, the value must also be a one position string. If the sequence is a list, the value may be any value. To modify a string destructively, use resize.

##### Example

```

> (pad {1 2 3} 10 0)

.:  {1 2 3 0 0 0 0 0 0 0}

> (pad "123" 10 "0")

.:  "1230000000"

> (pad "123" 10 "0" left)

.:  "0000000123"

> (pad {1 2 3} 10 0 left)

.:  {0 0 0 0 0 0 0 1 2 3}

```

##### Related

fill , resize

## partition

Creates a list of equivalence sets for a pivot element.

##### Syntax

(partition _sequence pivot comparer_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| pivot | variant | 1   | An element in the list. |
| comparer | function | 0-1 | A comparison function.( Defaults to compare.) |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of sublists each containing elements partitioned by a predicate.. |

##### Remarks

If no comparer is provided, the function compare is used. The element argument is compared to each item in the sequence and three lists are returned, elements that are less, elements that are the same, and elements that are greater. If a comparer function is provided, it must return the literals <, \=, > for elements that are less than, equal to, or greater than the pivot element.

##### Example

```

> (partition (3 5 2 0 5 8 9} 5)

.:  {{3 2 0}{5 5}{8 9}}

> (partition "abcdefg" "e")

.:  {{"a" "b" "c" "d"}{"e"}{"f" "g"}}

> ((function qksort {?list}

(if (void-p ?list) {}

else (let {?less ?same ?more} (partition ?list (pick ?list)))

(& (qksort ?less) ?same (qksort ?more))))

(3 5 2 7 5 6 0 8 9})

.:  {0 2 3 5 5 6 7 8 9}

```

##### Related

categorize

## path

Concatenates a folder and file name.

##### Syntax

(path _component_ _…_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| component | string | 1   | A folder, separator, or file name. |

##### Results

| Data Type | Description |
| --- | --- |
| string | Returns the concatenated folder and file as a string. |

##### Remarks

Returns a properly formatted path combining the folder and file name.The folder may or may not contain a terminating directory separator. The file may or may not contain a leading directory separator.

##### Example

```

> (path "C:/projects/project1/" (separator) "plan.pdf")

.:  "C:/projects/project1/plan.pdf"

> (path "C:/projects/project1/" (file name "plan.pdf"))

.:  "C:/projects/project1/plan.pdf"

> (path "C:/projects/project1/" (separator) "plan" (separator file) "pdf")

.:  "C:/projects/project1/plan.pdf"

```

##### Related

file, folder, separator, url

## pattern

Creates a pattern containing the supplied expressions.

##### Syntax

(pattern _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1+  | An expression. |

##### Results

| Data Type | Description |
| --- | --- |
| premise | A premise |

##### Remarks

Returns an unevaluated pattern.

##### Example

```

> (pattern Prediction ^ as ?p :Hypothesis as ?h)

.:  \[Prediction ^ as ?p :Hypothesis as ?h\]

> (pattern Hypothesis as ?h :Before as ?b :After as ?a (< ?b ?a))

.:  \[Hypothesis as ?h :Before as ?b :After as ?a (< ?b ?a)\]

> (pattern {Solution_1 Solution_2} as ?s :Timeframe >= ?t)

.:  \[Solution ^ {Solution_1 Solution_2} for ?s :Timeframe >= ?t\]

```

##### Related

^ _thought_, id, premise

## pause

Pauses an agent.

##### Syntax

(pause _agent_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| agent | agent | 1   | An agent |

##### Results

| Data Type | Description |
| --- | --- |
| agent | The agent task. |

##### Remarks

This function pauses an asynchronous agent task that processes incomingc messages and performs a default job.

##### Example

```

> (let ?url (url scheme tcp port 5001))

.:  true

> (function reply {?sender ?message} (tell ?sender "OK"))

.:  reply

> (function job {& ?args} (tell user ($ 1)) (wait 0.5))

.:  job

> (agent ?url reply job) (start Agent-1)

.:  Agent-1 Agent-1

> (pause Agent-1) (wait 3) (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1)

111111.: cancelled freed

```

##### Related

ask, cancel, listen, pause, perform, start, tell

## perform

Invokes a call.

##### Syntax

(perform _environment method instance expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| environment | environment | 0-1 | An environment (defaults to (scope)) |
| method | method | 1   | The method to be invoked |
| instance | instance | 1   | A prototype instance |
| expression | variant | 0+  | Additional arguements |

##### Results

| Data Type | Description |
| --- | --- |
| variant | A value returned by the call. |

##### Remarks

Invokes the method using the provided (or the current) environment.

##### Example

```

> (relation A

:Datum 0

!incr (method {}

(let ?me :Datum ?n)

(put ?me :Datum (++ ?n))))

.:  A

> (new A)

.:  A_1

> (perform (scope) !incr A_1)

.:  1

> (perform !incr A_1)

.:  2

```

##### Related

apply, call, closure, eval, function, macro, method, scope, supply

## pi

Returns 3.141592653589793.

##### Syntax

(pi)

##### Module

Math

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| real | The value of pi, 3.141592653589793 |

##### Remarks

Returns the constant 3.141592653589793

##### Example

```

> (pi)

.:  3.141592653589793

```

##### Related

e

## pick

Creates a list of randomly selected elements.

##### Syntax

(pick _sequence quantity_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence of elements |
| quantity | integer | 0-1 | The number of items to select. Default is 1. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A sequence containing the selected elements. |

##### Remarks

Returns the specified quantity of randomly-chosen elements from the sequence. The quantity must be a number between 1 and the sequence size.

##### Example

```

> (function chunk (+ 7 (random -2 to +2)))

.:  chunk

> (pick {a b c d e f g h i j k l m n o p q r s t u v w x y z} (chunk))

.:  {k j z h q f}

> (pick "abcdefghijklmnopqrstuvwxyz" (chunk))

.:  "cfilnsw"

```

##### Related

random, shuffle

## pipe

Creates a pipe.

##### Syntax

(pipe _option_ _…_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 1+  | A key value pair. One of<br><br>host _host_ \- name of the host computer<br><br>port _number_ – a port number.<br><br>path _name_ \- name of the pipe<br><br>mode _mode_ \- either read, write, or readwrite (default).<br><br>content _type_ - either binary or text (default).<br><br>address _url_\- url string.. |

##### Results

| Data Type | Description |
| --- | --- |
| io resource | A file resource |

##### Remarks

Creates a pipe for reading or writing.

##### Example

```

> (let ?pipe (pipe address "pipe://localhost:4500/MyPipe"))

.:  true

> (function reply {?target ?message} (tell ?target "goodbye."))

.:  reply

> (service ?pipe reply)

.:  Service-1

> (ask ?pipe "hello")

.:  "goodbye."

> (cancel Service-1) (free ?pipe) (free Service-1)

.:  cancelled freed freed

```

##### Related

close, erase, path, read, service, socket, write

## pop

Returns the element removed from a sequence.

##### Syntax

(pop _sequence position_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | An assortment or sequence. |
| position | integer | 0-1 | A position. (defaults to 1) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The removed element |

##### Remarks

If position is omitted the first element of the sequence shall be deleted. The sequences is modified.

##### Example

```

> (pop {a b c d})

.:  a

> (pop {a b c d} 2)

.:  b

> (pop {a b c d e f g} 7)

.:  g

```

##### Related

@ _element_, add,bind, cut, deq, enq, get, key, keys, put, #, values, zap

## posit

Writes module expressions to a url.

##### Syntax

(posit _module url_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | module | 1   | A module. |
| url | url | 0-1 | A url. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns the literal posited if successful. |

##### Remarks

This function writes all expression in the module to a file named "&lt;module&gt;.th".

##### Example

```

> (posit Geometry (folder path "c:/projects/premise/"))

.:  posited

> (posit MyModule (url path "//MyServer/Misc/"))

.:  posited

```

##### Related

dependencies, discard, file, folder, forgo, module, modules, require, grok, use, url

## position

Finds the position of an element or subsequence within a sequence.

##### Syntax

(position _sequence element option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The sequence to search |
| element | value | 1   | The item to be located |
| option | expression | 0+  | Key value pairs containing any of the following keys:<br><br>from _integer_ – the beginning position, (default is 1).<br><br>to _integer_ – a stop position, or # (default) for end of list<br><br>go _direction_ – forward (default) or backward. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The position of the item, or nil if not found. |

##### Remarks

None

##### Example

```

> (position {a b c d e f g h} f)

.:  6

> (position {a b c d e f g h} {f g h})

.:  6

> (position {a b a} a go backward)

.:  3

> (position {a b a} a go backward from 2)

.:  1

> (position "abcdefg" "cde" from 4)

.:  nil

```

##### Related

@ _element_, gather, in, occurs, pick

## positions

Returns positions of an element in a sequence or position value pairs.

##### Syntax

(positions _sequence element option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The sequence to search |
| element | value | 0   | The item to be located |
| option | expression | 0+  | Key value pairs containing any of the following keys:<br><br>from _integer_ – the beginning position, (default is 1).<br><br>to _integer_ – a stop position, or # (default) for end of list<br><br>go _direction_ – forward (default) or backward. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A possibly empty list containing the positions of the element. |

##### Remarks

If element is omitted, the function returns a list containing position value pairs for the sequence.

##### Example

```

> (positions {a b c d} b)

.:  {2}

> (positions {a b c d} x)

.:  {}

> (positions {a b c b d b} x)

.:  {2 4 6}

> (positions (tuple :X nil :Y nil :Z apple))

.:  {{1 :X}{2 nil}{3 :Y}{4 nil} {5 :Z}{6 apple}}

> (positions "abcd")

.:  {{1 "a"}{2 "b"}{3 "c"}{4 "d"}}

```

##### Related

bindings, definitions, entries, position

## positive-p

True if a number is greater than zero.

##### Syntax

(positive-p _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the number is greater than zero |

##### Remarks

None.

##### Example

```

> (positive-p 500)

.:  true

> (positive-p 0)

.:  false

> (positive-p -25)

.:  false

```

##### Related

even-p, negative-p, odd-p, zero-p

## premise

Creates a premise representation of a value.

##### Syntax

(premise _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A variant. |

##### Results

| Data Type | Description |
| --- | --- |
| premise | A premise |

##### Remarks

None.

##### Example

```

> (premise 1)

.:  \[Integer :Value 1\]

> (premise "The quick brown fox")

.:  \[String :Value "The quick brown fox" :Size 19\]

> (relation Foo :Item)

.:  Foo

> (premise (new Foo :Item bar))

.:  \[Foo ^ Foo_1 :Item bar\]

```

##### Related

id, position, known, new, old, relation, structure, the, with

## probability

Calculates the probability over a series.

##### Syntax

(probability _events A operation B_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| events | list | 1   | A list of elements representing events |
| A   | expression | 1   | A key value pair. One of<br><br>of _event_ - a list element<br><br>that _predicate_ - a unary truth function. |
| operation | literal | 0-1 | An operation. One of {and, or, given} |
| B   | expression | 0-1 | A key value pair. One of<br><br>of _event_ - a list element<br><br>that _predicate_ - a unary truth function. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The probability of the supplied expression. |

##### Remarks

Calculates the probability of A in a list, or a conditional probability if B is also provided. The operator may be one of {and, or, given}.

##### Example

```

> (probability {head tail head tail} of tail)

.:  0.5

> (probability {1 2 3 4 5 6} that even-p and that (given {?n} (< ?n 4)))

.:  0.16666666667

> (probability {1 2 3 4 5 6} that even-p given that (given {?n} (< ?n 4)))

.:  0.08333333333

```

##### Related

statistics

## procedure

Creates a public function that retuns \\%void within a module.

##### Syntax

(procedure _scope name parameters expression_ _…_ )

_parameters_ ::=

_parameters_ ::= { }

_parameters_ ::= {_required_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ }

_parameters_ ::= {_required_ _…_ + _optional_ _…_ % _keyword_ }

_parameters_ ::= {_required_ _…_ \+ _optional_ _…_ % _keyword_ _…_ & _remaining_ }

_parameters_ ::= {_required_ _…_ % _keyword_ _…_ & _remaining_ }

_parameters_ ::= {_required_ _…_ & _remaining_ }

_parameters_ ::= { \+ _optional_ _…_ }

_parameters_ ::= { \+ _optional_ _…_ % _keyword_ }

_parameters_ ::= { \+ _optional_ _…_ % _keyword_ _…_ & _remaining_ }

_parameters_ ::= { \+ _optional_ _…_ & _remaining_ }

_parameters_ ::= { % _keyword_ _…_ }

_parameters_ ::= { % _keyword_ _…_ & _remaining_ }

_parameters_ ::= { & _remaining_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied, a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing variables, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Procedures are functions defined using the procedure intrinsic function. If the name is supplied then the procedure is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter variables to any actual parameter expressions provided. The first variables in the parameter list are required. If a plus sign is provided, then those variables following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If a percent sign is supplied the next variables are keyword variables where the supplied slot shall have the same name as the symbol parameter excepting the first character of the name which shall be a colon for the slot and a question mark for the symbol. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. The entire parameter list may be omitted.

A procedure returns the taxon \\%void.

##### Example

```

> (procedure {reference ??n} (++ ??n))

.:  fn-1

> (so {?x 100} (fn-1 ?x))

.:  \\%void

> (so {?x 100} (fn-1 ?x) ?x)

.:  101

> (procedure plusN {reference ??n + integer ?i = 1} (++ ?n ?i))

.:  plusN

> (so {?y 100} (plusN ?y))

.:  \\%void

> (so {?y 100} (plusN ?y) ?y)

.:  101

```

##### Related

arguments, call, extend, function, functions, junction, macro, module, modules, parameters

## proceed

Transfers control to a location.

##### Syntax

(proceed _location_ set _assignment_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| location | location | 1   | A location resource. |
| set | literal | 0-1 | The literal set. |
| assignment | expression | 0+  | Symbol value pairs for extant variables at the location. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true. |

##### Remarks

Transfers control to the specified location; then sets the indicated variables to new values. If the variables are not defined at the location, an unbound symbol failure occurs.

##### Example

```

> (function factorial_hps {?n ?k}

(let ?a 1)

(location ?m)

(if (<= ?n 0) (proceed ?k set ?r ?a)

else (proceed ?m set ?n (\* (<-- -- ?n) ?a))))

.:  factorial_hps

> (function factorial {?n}

(let ?r nil)

(location ?k)

(if (any ?r) ?r

else (factorial_hps ?n ?k))))

.:  factorial

> (factorial 5)

.:  120

```

##### Related

location, go

## product

Multiplies an expression over a range of values.

##### Syntax

(product _symbol_ _…_ _binding_ _sequence_ _expression_ _…_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | variant | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result of applying multiplication to the last expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the variables then the function fails. The last expression shall be evaluated and the plus function shall be applied to both that expression and any prior result. The final value is returned.

##### Example

```

> (product ?x in (range 1 to 10) ?x)

.:  55

> (generator OneToTen {}

(step ?i from 1 to 10 (yield ?i))

(done))

.:  OneToTen

> (product ?x in (OneToTen) ?x)

.:  55

```

##### Related

fold, summation

## punctuation-p

True if the first position of a string is punctuation.

##### Syntax

(punctuation-p _string_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A value.. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the first position is punctuation. |

##### Remarks

None

##### Example

```

> (punctuation-p " the quick brown fox ")

.:  false

> (punctuation-p "This and that")

.:  false

> (punctuation-p "400 years")

.:  false

> (punctuation-p "...")

.:  true

```

##### Related

alphabetic-p, lowercase-p, uppercase-p, whitespace-p

## push

Modifies a sequence by inserting a value.

##### Syntax

(push _sequence value position_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| value | variant | 1   | The value to be inserted. |
| position | integer | 0-1 | The position to insert the value. (Default is 1.) |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The modified sequence. |

##### Remarks

If position is omitted the value is prepended to the sequence. If # is used for the position, the value is appended to the sequence. Otherwise, the value is inserted at the indicated position. The sequence itself is modified.

##### Example

```

> (push {a b c} d)

.:  {d a b c}

> (push {a b c} d 2)

.:  {a d b c}

> (push "abcdef" g #)

.:  "abcdefg"

```

##### Related

\# _size_, add, cut, deq, enq, get, insert, key, keys, put, values, zap

## put

Modifies an assortment or sequence by updating values.

##### Syntax

(put _container entry_ _…_ )

_entry_ ::= _key value_

_entry_ ::= _position value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |
| entry | expression | 1+  | A key and value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| thing | Returns the modified assortment or sequence. |

##### Remarks

For assortments, the key(s) to be updated must be present, for sequences, the positions to update must be within the sequence, otherwise the function fails. Keys and positions are added via the add function. Positions may be also added using append. Use copy or clone to return a new container. A coordinate is a position list. A list of keys may be provided for an entry as well, in which case the keys are traversed and the value is placed at the last key. To create a new container use replace.

##### Example

```

> (let ?a (lexicon x 1 y 2 z 3) ?s {a b c d e})

.:  true

> (entries (put ?a y 12 z 13))

.:  {{x 1}{y 12}{z 13}}

> (put ?s 2 hello 3 goodbye)

.:  {a hello goodbye d e}

```

##### Related

add, cut, get, has, key, keys, lacks, let, values

## qualified

Prepends a module to a function name.

##### Syntax

(qualified _module function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module literal. |
| function | literal | 1   | A function or macro literal. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The fully qualified literal with the module prepended to the function. |

##### Remarks

Returns a fully qualified function literal. If omitted, the first function matching the literal is returned.

##### Example

```

> (module Math

(function sum {& ?args} (apply + ?args)))

.:  Math

> (qualified sum)

.:  User.sum

> (qualified Math sum)

.:  Math.sum

> (require Math)

.:  Math

> (qualified sum)

.:  Math.sum

```

##### Related

functions, modules, qualifier, unqualified

## qualifiers

Creates a list of modules associated with an identifier.

##### Syntax

(qualifiers _identifier_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| identifier | identifier | 1   | An identifier |

##### Results

| Data Type | Description |
| --- | --- |
| list | The modules associated with the literal. |

##### Remarks

Checks the function against known modules and returns the modules in which the function is defined.

##### Example

```

> (qualifiers sum)

.:  {}

> (module Math

(function sum ?args (apply + ?args)))

.:  Math

> (use User)

.:  User

> (require Math)

.:  Math

> (qualifiers sum)

.:  {Math}

```

##### Related

functions, modules, qualified, unqualified

## quantify

Returns a quantifier for elements satisfying a test.

##### Syntax

(quantify _sequence predicate option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| predicate | function | 1   | A truth expression |
| option | expression | 0+  | A key value pair. One of<br><br>as _format_ - either the literal word (default) or percent. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns a percentage or the words none, few, half, most, all. |

##### Remarks

None.

##### Example

```

> (quantify {1 2 3 -4 5 6 7 8 9 10} (given {?n} (< ?n 0)))

.:  few

> (quantify {1 2 3 4 5 6 7 8 9 10} number-p as percent)

.:  1.0

> (quantify {1 2 3 4 5 6 7 8 9 10} odd-p)

.:  half

> (quantify {1 2 3 4 5 6 7 8 9 10} negative-p)

.:  none

> (quantify {1 2 3 5 6 7 8 9} odd-p)

.:  most

```

##### Related

coalesce, collect, exactly, filter, gather, quantity

## quantity

Returns the number of elements satisfying a test.

##### Syntax

(quantity _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per. |
| sequence | sequence | 1   | A sequence (string or list) |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| number | Returns the number of elements satisfying the test. |

##### Remarks

None.

##### Example

```

> (quantity ?n in {1 2 3 4 5 6 7 8 9 10}

(is ?n (given {?x} (= (taxon ?x) number))))

.:  10

> (summation ?n in {1 2 3 4 5 6 7 8 9 10} (bracket (odd-p ?n)))

.:  5

> (quantity ?n in {1 2 3 4 5 6 7 8 9 10} (odd-p ?n))

.:  5

> (quantity ?n in {1 2 3 4 5 6 7 8 9 10} (negative-p ?n))

.:  0

```

##### Related

coalesce, collect, exactly, filter, gather, quantify

## radians

Converts degrees to radians.

##### Syntax

(radians _degrees_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| degrees | number | 1   | a number in degrees. |

##### Results

| Data Type | Description |
| --- | --- |
| number | Number of radians. |

##### Remarks

For the conversion the degrees are multiplied by π / 180, or roughly 0.0174532922222222.

##### Example

```

> (radians 200)

.:  3.490658444444444

> (radians 120)

.:  2.094395066666667

> (radians 45)

.:  0.7864815

```

##### Related

cosine, degrees, sine, tangent

## radix

Converts a number to a base.

##### Syntax

(radix _number base_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | An integer or unsigned number to convert |
| base | integer | 0-1 | A number between 2 and 36. (default is 10) |

##### Results

| Data Type | Description |
| --- | --- |
| number | The number converted to the base as as an integer or long. |

##### Remarks

None.

##### Example

```

> (radix 15 8)

.:  \\#n08r17

> (radix (unsigned 89975) 16)

.:  \\#u16r15F77

> (radix \\#nx15F77)

.:  \\#n10r89975

> (radix #gd10 10)

.:  \\#g10r10

> (radix (integer 2.003) 2)

.:  \\#n02r10

```

##### Related

big, complex, float, imaginary, integer, long, real, unsigned

## random

Creates a random number.

##### Syntax

(random _lower_ to _upper precision_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| lower | number | 1   | A lower bound |
| to | literal | 1   | The literal to |
| upper | number | 1   | An upper bound |
| precision | literal | 0-1 | Either integer (default), real or float |

##### Results

| Data Type | Description |
| --- | --- |
| number | A random number. |

##### Remarks

If the precision is omitted the default precision is integer. If precision is omitted and the bounds are zero and one, then the default precision is real. If the precision is supplied, then it is used.

##### Example

```

> (random 0 to 1)

.:  0.325377881526947

> (random 0 to 1 float)

.:  0.8128264546394348216582

> (random 0 to 100)

.:  63

> (random 1000 to 2000 real)

.:  1194.230922829

```

##### Related

pick, shuffle

## range

Creates a list of numbers.

##### Syntax

(range _first_ to _last_ by _increment_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| first | number | 1   | The initial value of the symbol |
| limit | literal | 1   | The literal to, above, below or go. (default is to). |
| last | number | 1   | The final value of the symbol |
| by | literal | 0-1 | by  |
| increment | number | 0-1 | The positive or negative increment for the symbol |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list containing the numbers in the range. |

##### Remarks

If to is specified, the last number is included in the iteration. If below is specified the _last_ value is excluded from the iteration. If above is specified the next number above the _last_ value is included in the iteration. If go is specified, then the _last_ value specifies the number of iterations.

##### Example

```

> (range 1 to 5)

.:  {1 2 3 4 5}

> (range 1 to 10 by 2)

.:  {1 3 5 7 9}

> > (range 100 go 5)

.:  {100 101 102 103 104 105}

```

##### Related

for, step

## rational

Converts values to a rational number.

##### Syntax

(rational _numerator denominator_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| numerator | variant | 1   | An integer or the literal minimum or maximum. |
| denominator | variant | 0-1 | A non-zero integer.( Default is 1.) |

##### Results

| Data Type | Description |
| --- | --- |
| number | A rational number. |

##### Remarks

All integers are rational numbers with a denominator of 1. If a non-zero denominator is supplied, it must be an integer. If a denominator is not supplied, then an attempt is made to convert the value to a rational number.

##### Example

```

> (rational {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not number"\]

> (rational "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not number"\]

> (rational 500)

.:  500/1

> (rational 500.0)

.:  500/1

> (rational "23.4")

.:  234/10

```

##### Related

complex, float, imaginary, integer, is, real

## read

Creates a string or stream.

##### Syntax

(read _file count bits_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| file | resource | 1   | An file, or pipe. |
| count | variant | 0-1 | The number of bytes to read, the literal all,<br><br>or the literal line. (Default is all.) |
| bits | integer | 0-1 | If count is provided, then this represents the size of the character in bits. Either 7, 8, 16,o,r 32. (Default is 8.) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | A string, stream, or the value nothing (if at end of file). |

##### Remarks

If the literal all is provided for count, the entire file (or stream) is read. If line is provided, one line is read (up to the newline character). If count is omitted, then the entire file read.

##### Example

```

> (global ?File (file name "test.txt" seek 1 erase yes)) ; open at BOF

.:  true

> (seek ?File 1)

.:  File-1

> (read ?File all)

.:  "Hello, world.'

> (close ?File)

.:  closed

```

##### Related

bytes, close, take, peek, peep, file, seek, write

## ready-p

True if a task has completed.

##### Syntax

(ready-p _task_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the task has completed |

##### Remarks

Returns true if the task has completed, false otherwise.

##### Example

```

> (let ?task (concurrent (@ (concurrent (idle \\@s100)))))

.:  true

> (do (idle \\@s20)

(if (ready-p ?task)

(free ?task)

else

running))

.:  running

```

##### Related

wait, abort, await, busy-p, cancel, cancelled-p, complete, reclaim, tarry, task

## real

Converts a value to a real number.

##### Syntax

(real _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number or the literal minimum or maximum. |

##### Results

| Data Type | Description |
| --- | --- |
| number | A real number. |

##### Remarks

If the value cannot be converted to a real number, the function fails.

##### Example

```

> (real {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not number"\]

> (real "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not number"\]

> (real 500)

.:  500.0

> (real 500.0)

.:  500.0

> (real "23.4")

.:  23.4

```

##### Related

complex, float, imaginary, integer, long, rational

## reasoning

Resumes or pauses asynchronous rule execution.

##### Syntax

(reasoning _toggle_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| toggle | literal | 0-1 | The value on or off. Default is on if not supplied. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if rule execution is on. |

##### Remarks

If toggle is provided, rule execution is resumed (for on) or paused (for off).

##### Example

```

> (relation Car :Age :Condition)

.:  Car

> (rule

when \[Car :Age /= old :Condition = good\]

do (tell user ($ ($$ \\n that) is possible. \\n)))

.:  Rule-1

> (new Car :Age new :Condition good)

.:  Car_1

> (reasoning)

.:  true

that is possible.

> (reasoning off)

.:  false

```

##### Related

is, rule, rules

## reclaim

Performs garbage collection.

##### Syntax

(reclaim)

##### Module

Base

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns the literal reclaimed when completed. |

##### Remarks

None.

##### Example

```

> (reclaim)

.:  reclaimed

```

##### Related

free

## reduce

Converts a sequence into a value.

##### Syntax

(reduce _sequence function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| function | function | 1   | A function. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The return value of the function applied to all the items in succession. |

##### Remarks

Applies the binary function to each item of a list and returns the final value.

##### Example

```

(reduce {1 2 3 4 5} \*)

.:  120

(reduce {1 2 3 4 5} +)

.:  15

(reduce {3 2 1} **)

.:  9

```

##### Related

fold

## reference

Returns a reference to a symbol.

##### Syntax

(reference _symbol_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol |

##### Results

| Data Type | Description |
| --- | --- |
| reference | Returns a symbol reference. |

##### Remarks

The convention for denoting reference variables is to use two question marks: ??name.

##### Example

```

> (structure ListNode :Val :Next)

.:  ListNode

> (function IsPalindrome2 {ListNode ?tail reference ??head}

(ensure ListNode (actual ??head))

(if (null-p ?tail)

(return true)

or (and (IsPalindrome2 (:Next ?tail)) (= (:Val ?tail) (:Val ??head)))

(set ??head (:Next ??head))

(return true)

else (return false)))

.:  IsPalindrome2

> (function IsPalindrome {?head}

(ensure ListNode ?head)

(return (IsPalindrome2 ?head (reference ?head))))

.:  IsPalindrome

> (IsPalindrome  
(new ListNode :Val a :Next (new ListNode :Val b :Next (new ListNode :Val a))))

.:  true

```

##### Related

actual, assume, dynamic, given, global, let, scope, set, tie

## relation

Creates a relation.

##### Syntax

(relation _name_ _inclusion_ _…_ _definition_ _…_ )

_inclusion_ ::= uses { _prototype_ _…_ }

_definition_ ::= _slot_

_definition_ ::= _slot default-value_

_definition_ ::= _method function_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of the relation |
| inclusion | expression | 0+  | A inclusion expression |
| definition | expression | 0+  | A slot definition expression |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the defined relation |

##### Remarks

Relations are assortment prototypes that represent persistent relationships among one or more values. A relation is comprised of a name, attributes (collectively called slots) with optional default values, and methods. Relations are defined using the relation function. A SubThought is a relation record created using the new function. A relation must be defined before a SubThought can be formed. Any number of slots or methods can be specified, and default values may also be defined. A sealed relation cannot create new thoughts.

##### Example

```

> (relation Employee

:Salary

:Name

:Supervisor

:Reclaim false

!SalaryYTD Employee_salaryYTD

)

.:  Employee

> (new Employee :Name "Jane Dough" :Salary 2000000.00)

.:  Employee_1

> (premise Employee_1)

.:  \[Employee ^ Employee_1 :Salary 2000000.0 :Name "Jane Dough" :Supervisor nil

:Recalim false !SalaryYTD Employee_salaryYTD\]

```

##### Related

new, nix, old, relation-p, relations, seal, structure, structures, unseal

## relations

Returns a list of defined relations.

##### Syntax

(relations)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list of all defined relations. |

##### Remarks

None

##### Example

```

> (relation Animal

:Phylum :Class :Order :Family :Genus :Species :Color :Weight :Height

)

.:  Animal

  
\> (relations)

.:  {Animal}

> (nix Animal)

.:  nixed

> (relations)

.:  {}

```

##### Related

structures, structure, new, nix, old, relation,

## release

Releases locks on critical sections.

##### Syntax

(release _locks_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| locks | list | 1   | A list of literals denoting critical section locks. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns the literal released if successful. |

##### Remarks

Forces the release of critical section locks.

##### Example

```

> (function pp {+ ?a ?b ?c ?d}

(critical {A B} (tell user ($ ?a ?b)))

(critical {C D} (tell user ($ \\s ?c ?d \\n))))

.:  pp

> (free (complete (critical {A B C D} (idle \\@s30)))

(do (idle 5)

(release {A B C D})

(tarry (complete

(pp the quick brown fox)

(pp jumped over lazy dogs)

(pp four score and seven)))))

the quick jumped over brown fox

four score lazy dogs

and seven

.:  freed

```

##### Related

critical

## remove

Creates a new assortment by removing values.

##### Syntax

(remove _assortment value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| value | variant | 1+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The new assortment. |

##### Remarks

To remove elements destructively use the rip function.

##### Example

```

> (entries (collection a b c d))

.:  {{a a} {b b} {c c} {d d}}

> (entries (remove (lexicon a 1 b 2 c 3 d 4) 2 4))

.:  {{a 1}{c 3}}

```

##### Related

add, combine, cut, rip

## repeat

Loops a specified number of times.

##### Syntax

(repeat _count_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| count | variant | 1   | The number of iterations. |
| expression | expression | 0+  | A call to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | returns the last expression on the last iteration. |

##### Remarks

Repeats the expression(s) the specified number of times. An implicit counter from 0 to the designated count. Count may be an integer or long value.

##### Example

```

> (global ?i 0)

.:  true

> (repeat 10 (--> ++ ?i))

.:  10

> (repeat 10 (--> -- ?i))

.:  0

> (repeat 1000 (--> ++ ?i))

.:  1000

> ?i

.:  1000

```

##### Related

do, for, loop, step, until, while

## replace

Creates a new assortment or sequence by updating values.

##### Syntax

(replace _container entries option_ )

_entry_ ::= _key value_

_entry_ ::= _position value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |
| entries | variant | 1+  | A list of key value pairs or index value pairs, or a lexicon. |
| options | expression | 0-1 |     |

##### Results

| Data Type | Description |
| --- | --- |
| thing | Returns the modified assortment or sequence. |

##### Remarks

For assortments, the key(s) to be updated must be present, for sequences, the indicies to update must be within the sequence, otherwise the function fails. Keys and positions are added via the add function. Positions may be also added using append. Use copy or clone to return a new container. A coordinate is a position list. A list of keys may be provided for an entry as well, in which case the keys are traversed and the value is placed at the last key.

##### Example

```

> (let ?a (lexicon x 1 y 2 z 3) ?s {a b c d e})

.:  true

> (entries (replace ?a {{y 12}{z 13}}))

.:  {{x 1}{y 12}{z 13}}

> (replace ?s {{2 hello}{3 goodbye}} by index)

.:  {a hello goodbye d e}

```

##### Related

add, cut, get, has, key, keys, lacks, let, values

## require

Retrieves an absent module.

##### Syntax

(require _module_ as _moniker_ from _url_ _…_ _options_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | The name of the required module |
| as | literal | 0-1 | The literal as. |
| moniker | literal | 0-1 | A literal. |
| from | literal | 0-1 | The literal from. |
| url | url | 0+  | URLs from which to retrieve the module. |
| options | expression | 0+  | Any of the following  <br>update _choice_ where choice Is yes or no. |

#####
Results

| Data Type | Description |
| --- | --- |
| literal | The module |

##### Remarks

Allows the current module to access functions in the specified module using a moniker. The from URLs shall be evaluated if the module is either not present or if the update option is yes. Grok is applied to the urls in succession until one url is available to be read.

##### Example

```

> (mySum 1 2 3)

.:  \[Failure :Name NotFound :Text "The function mySum isn't found"\]

> (require MyMath as m from (file "lib/mymath.th"))

.:  MyMath

> (mySum 1 2 3) (m.mySum 1 2 3)

.:  6 6

```

##### Related

dependencies, discard, extend, forgo, module, modules, run, use

## in

True if a value is in a sequence.

##### Syntax

(in _value sequence option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |
| sequence | sequence | 1   | A sequence. |
| option | expression | 0-2 | A key value pair. Any of<br><br>depth _number_ \- Number or # (for any depth). Default is 1.<br><br>transform _function_ \- A function to transform the element.. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the value is in the sequence, false otherwise. |

##### Remarks

None.

##### Example

```

> (in d {a b c d e f g})

.:  true

> (in "a" "cbazyx")

.:  true

```

##### Related

beyond, includes, excludes, has, out, within

## reset

Resets a series for reuse.

##### Syntax

(reset _series_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| series | series | 1   | A series. |

##### Results

| Data Type | Description |
| --- | --- |
| series | Returns the series. |

##### Remarks

After the series is reset, the next function must be used to move the series to the first element.

##### Example

```

> (global ?Series (series {a b c}))

.:  true

> (while (next ?Series) (tell user ($$ (this ?Series) ,) ($)))

a, b, c, .: told

> (reset ?Series)

.:  Series-1

> (this ?Series)

.:  \[Failure :Name OutOfRange :Text "Must advance series to the first element."\]

> (next ?Series)

.:  true

> (this ?Series)

.:  a

```

##### Related

next, series, this

## resize

Modifies the length of a sequence.

##### Syntax

(resize _sequence length default_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| length | integer | 1   | The length of the final sequence |
| default | variant | 0-1 | A value to fill the sequence (default is nil or space). |

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a the modified list. |

##### Remarks

If the sequence is a string, the default value must be a single position string (space if unspecified). If the sequence is a list, the default value may be any value (nil if unspecified).

##### Example

```

> (let ?s (array 3 of 0))

.:  true

> (fix ?s 1 1 2 2 3 3)

.:  {1 2 3}

> (resize ?s 10 0)

.:  {1 2 3 0 0 0 0 0 0 0}

> (resize ?s 2 0)

.:  {1 2}

```

##### Related

array, fill , pad

## rest

Creates a subsequence of all except the first elements.

##### Syntax

(rest _sequence skip_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |
| skip | number | 0-1 | The number of elements to skip. Default is 1 |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The sequence without the skipped elements. |

##### Remarks

None

##### Example

```

> (rest {a b c d e})

.:  {b c d e}

> (rest "abcdefg")

.:  "bcdefg"

> (rest "abcdefg" 2)

.:  "cdefg"

> (rest {a b c d e} 3)

.:  {d e}

> (rest {a b c d e} 5)

.:  {}

```

##### Related

but, last, top

## retract

Eliminates rules.

##### Syntax

(retract _rules_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| rules | variant | 1   | A single rule resource or a list of rule resources. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The literal retracted |

##### Remarks

None.

##### Example

```

> (relation Fact :Number)

.:  Fact

> (rule

when \[Fact :Number as ?n\]

(no \[Fact ^ as ?f (= (:Number ?f) (++ ?n)\])

do (knew Fact :Number (++ ?n)))

.:  Rule-1

> (rule CleanUp when \[Fact ^ as ?fact\] do (old ?fact))

.:  CleanUp

> (rules)

.:  {CleanUp Rule-1}

> (retract (rules))

.: retracted

> (rules)

.:  {}

```

##### Related

wait, abort, await, task, complete, busy-p, ready,-p, reclaim

## return

Terminates a function call.

##### Syntax

(return _value option_ _…_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | Any value to be returned. (Default is nil.) |
| option | expression | 0-1 | A key value pair. One of:<br><br>from _function_ \- returrns from a function on the call graph.<br><br>unwind _count_ \- unwinds the call graph a number of times.. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The returned value. |

##### Remarks

Return exits from an encompassing function. If the value is not specified, nil is returned. When return is evaluated, the encompassing function immediately returns the value. If from is specified along with the name of a function, the first encompassing function having the same name is exited. If unwind is specified, then the call graph is unwound the indicated number of times.

##### Example

```

> (function foo

(step ?item from 1 to 20

(if (= ?item 10) (return found-it))

not-found))

.:  foo

> (foo)

.:  found-it

> (function f1 {}

(do (tell user ($ inside do. \\n))

(return 0))

(tell user ($ within f1. \\n)))

.:  f1

> (function main

(fn1)

(tell user ($ within main. \\n)))

.:  main

> (main)

inside do.

within f1.

within main.

.:  nil

> (function f1 {}

(do (tell user ($ inside do. \\n))

(break 0))

(tell user ($ within f1. \\n)))

.:  f1

> (main)

inside do.

within f1.

within main.

.:  told

> (function f1 {}

(do (tell user ($ inside do. \\n))

(break 0))

(tell user ($ within f1. \\n)))

.:  f1

> (main)

inside do.

within f1.

within main.

.:  told

> (function f1 {}

(do (tell user ($ inside do. \\n))

(return 0 from f1))

(tell user ($ within f1. \\n)))

.:  f1

> (main)

inside do.

within main.

.:  told

> (function f1 {}

(do (tell user ($ inside do. \\n))

(return 0 from f1))

(tell user ($ within f1. \\n)))

.:  f1

> (main)

inside do.

within main.

.:  told

> (function f1 {}

(do (tell user ($ inside do. \\n))

(return 0 from f1))

(tell user ($ within f1. \\n)))

.:  f1

> (main)

inside do.

within main.

.:  told

> (function f1 {}

(do (tell user ($ inside do. \\n))

(return 0 from main))

(tell user ($ within f1. \\n)))

.:  f1

> (main)

inside do.

.:  0

> (let ?a (so {?y "hello"}

(if (< (@ ?name) "M") (return ($ Goodbye ?name) unwind 2)

else (tell user ($ Hello ?name)))

(ask user ($ What is your favorite color?))

($ You’re nice))

.:  true

> ?a

.:  "You’re nice"

```

##### Related

continue, do, break, fail, function, go, location, resume, try

## reverse

Creates a reversed sequence.

##### Syntax

(reverse _sequence_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The reversed sequence |

##### Remarks

None.

##### Example

```

> (reverse "abcde")

.:  "edcba'

> (reverse {a b c d e})

.:  {e d c b a}

> (reverse \[A :B C :D E\])

.:  \[E :D C :B A\]

> (reverse (' (a b c d e)))

.:  (e d c b a)

```

##### Related

but, first, last, pick, rest, mid, top

## right

True if values are equal or the first value is nil.

##### Syntax

(right _first_ _second_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| first | variant | 1   | A value to be compared. |
| second | variant | 1   | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are the same or if second is nil |

##### Remarks

Returns true if each value is the same or if the first value is nil, and false otherwise. Both values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equal if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical). Returns false if both values are false.

##### Example

```

> (right a a)

.:  true

> (right "johnny" "ralph")

.:  false

> (right nil 3)

.:  true

> (right nil nil)

.:  false

```

##### Related

< _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal_, full, identical, left

## rip

Removes elements from assortments by value.

##### Syntax

(rip _assortment value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| value | variant | 1+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The modified assortment. |

##### Remarks

Assortments are modified destructively. To delete nondestructively use the omit function.

##### Example

```

> (entries (collection a b c d))

.:  {{a a} {b b} {c c} {d d}}

> (entries (rip (lexicon a 1 b 2 c 3 d 4) 2 4))

.:  {{a 1}{c 3}}

```

##### Related

cut, omit

## round

Rounds a number to the nearest integer.

##### Syntax

(round _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A real number. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The rounded integer |

##### Remarks

If the number is zero, zero is returned. If the number is negative then if the tenths digit is five or less, it shall be rounded down towards negative infinity, otherwise it shall be rounded towards positive infinity. If the number is positive, then if the tenths digit is five or greater, it shall be rounded towards positive infinity, otherwise it shall be rounded towards negative infinity.

##### Example

```

> (round 0.5)

.:  1

> (round 0.4)

.:  0

> (round 0.49)

.:  0

> (round -0.5)

.:  -1

> (round -0.4)

.:  0

```

##### Related

% _modulus_, ceiling, floor,truncate,

## rule

Creates a rule.

##### Syntax

(rule _name_ _properties_ when _premises_ _option_ _…_ _action_ _…_ )

_properties_ ::= { _property_ _…_ }

_property_ ::= :Stage _literal_

_property_ ::= :Salience _integer_

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= as _symbol_

_binding_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _value_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

_option_ ::= scan _number_

_option_ ::= limit _number_

_option_ ::= group _slot_ _…_ by _slot_ _…_ into _symbol_

_option_ ::= merge _value_ _…_

_option_ ::= sort _ordering_ _…_

_action_ ::= deem _value1_ else _value2_

_action_ ::= do _expression_ _…_

_action_ ::= give _expression_

_action_ ::= list _value_ _…_

_action_ ::= tally

_action_ ::= yield _expression_

_ordering_ ::= _term comparator_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 0-1 | The name of the rule. If omitted, the rule is auto-named. |
| properties | list | 0-1 | A list containing any of the following properties:<br><br>:Salience _integer_ – indicates the rule priority<br><br>:Stage _literal_ – indicase the rule stage |
| with | literal | 1   | The literal with. |
| clauses / premises | expression | 1+  | Either one or more clauses, or, one or more premises |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |
| action | literal | 0-1 | Either deem, do, give, list, tally, yield. |
| expression | expression | 0+  | An expression |

##### Results

| Data Type | Description |
| --- | --- |
| rule | Returns a rule. |

##### Remarks

The rule macro creates a rule to monitor premises. The rule is run spontaneously when premises match the preconditions. There is no guarantee as to when or whether or not the rule shall execute. The rule may be cancelled and deleted using the reclaim command.

Note that a predicate is a truth function, scan tells the number of matches to attempt (default is infinity), and limit tells how many results to return (default is infinity). If the action is deem, then the subsequent value is returned if the final descriptor is matched, otherwise the else value is returned. If the action is do, then for each match the expressions are run, and for the last match, the last value of the last expression is returned, or nil is returned if all descriptors were false or had no matches. If the action is give, then the expression is immediately returned from the with call on the first match, akin to return from with. If the action is yield, then the expression is immediately returned from the with call, but may be resumed with a next function call. When all matches are completed, the done function is implicitly called to terminate the generator. If the action is group, followed by a list of slots and values from which the group is picked, then the literal by and a set of slots and values that determines the grouping inclusion , and finally the literal into followed by a symbol to which the group shall be bound on each iteration. If the action is either list (or merge), then a (merged) list is returned or an empty list if nothing matched. If the action is sort then the list of slots and comparators should follow. (Note that list is required if the sort action is selected.) If the action is tally, then the number of matched premises is returned, or zero if no matches.

##### Example

```

> (reasoning off)

.:  false

> (relation Fact :All :Are)

.:  Fact

> (rule ExcludedMiddle

when \[Fact :All as ?S :Are as ?M\]

\[Fact :All = ?M :Are as ?P\]

do

(knew Fact :All ?S :Are ?P))

.:  ExcludedMiddle

> (new Fact :All people :Are mortal)

.:  Fact_1

> (with Fact)

.:  {Fact_1}

> (new Fact :All philosophers :Are people)

.:  Fact_2

> (with Fact list @^)

.:  {Fact_1 Fact_2}

> (reasoning on)

.:  true

> (with Fact list @^)

.:  {Fact_1 Fact_2 Fact_3}

> (get Fact_3)

.:  \[Fact ^ Fact_3 :All philosphers :Are mortal\]

> (rules)

.:  {ExcludedMiddle}

> (retract ExcludedMiddle)

.:  retracted

> (rule {:Salience 100 :Stage 0}

when \[Fact :All as ?S :Are as ?M\]

\[Fact :All = ?M :Are as ?P\]

do

(knew Fact :All ?S :Are ?P))

.:  Rule-1

> (rules)

.:  {Rule-1}

> (retract (rules))

.:  retracted

> (which Fact ^ as ?a :Are mortal list ?a)

.:  {Fact_1 Fact_3}

> (which Fact :Are mortal)

.:  {\[Fact ^ Fact_1 :All people :Are mortal\]

\[Fact ^ Fact_3 :All philosophers :Are mortal\]}

```

##### Related

reasoning, reclaim, rules, using, with

## rules

Returns a list of rules defined in a module.

##### Syntax

(rules _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module. If not provided defaults to the current module. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of rules defined in the module. |

##### Remarks

The module must be a literal in the list obtained by calling the (modules) function. If the module is not provided this function uses the current module (obtained via the (use) function).

##### Example

```

> (module Mine

(rule foo {:Stage One :Salience 0} when \[A ^ as ?a\] list ?a))

.:  Mine

> (rules Mine)

.:  {foo}

> (use User)

.:  User

> (rule hello when \[A ^ as ?a\] list ?a)

.:  hello

> (rules)

.:  {hello}

```

##### Related

function, module, modules, variables

## same

True if all values are equal or contain equal elements.

##### Syntax

(same _value_ _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all values are identical |

##### Remarks

Returns true if each value is the equal to the next value from left to right, sequences are the same if the are equal length and contain the same elements regardless of order.

##### Example

```

> (same a a a)

.:  true

> (same "johnny" "ralph" "sam")

.:  false

> (same 3 3 3)

.:  true

> (same {a b c} {c b a} {c a b})

.:  true

> (same "abc" "cba" "cab")

.:  true

> (same {"abc"}{"cba"}{"cab"})

.:  false

```

##### Related

\= _equal_, < _less_ , <= _less or equal_, > _greater_, >= _greater or equal_, /= _unequal_, identical

## scale

Applies a function to a list of numbers and scalar values.

##### Syntax

(scale _list scalar_ _…_ _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| list | list | 1   | A list of numbers. |
| scalar | number | 1+  | A number. |
| function | function | 1   | The name of the function to invoke |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The resulting sequence. |

##### Remarks

None.

##### Example

```

> (scale {1 2 3} 5 +)

.:  {6 7 8}

> (scale {1 2 3} 5 10 \*)

.:  {50 100 150}

```

##### Related

apply, collect, count, filter, gather, group, map, merge, reduce , separate, sort

## scatter

Applies functions in parallel returning a list of results.

##### Syntax

(scatter _arguments functions_)

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| arguments | list | 0-1 | The intial arguments to each function. |
| functions | list | 1   | An unordered list of functions to be applied. |

##### Results

| Data Type | Description |
| --- | --- |
| list | Non nil results |

##### Remarks

This function supplies the arguments to each function and returns a list of results from all the functions evaluated in parallel. Sequential forms of this function are compose and morph.

##### Example

```

> (scatter {5} {++ -- (given {?x} (\* ?x 2))})

.:  {6 4 10}

> (scatter {{the quick brown fox jumped over the lazy dogs}}

{but rest top last})

.:  {{the quick brown fox jumped over the lazy }

{quick brown fox jumped over the lazy dogs}

{the} {dogs}}

> (scatter {2 3 4} {+ \* -})

.:  {9 24 -5}

```

##### Related

apply, concurrent, complete, compose,map, morph

## scope

Finds an environment or gets the current environment.

##### Syntax

(scope _keyval_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| keyval | expression | 0-2 | A key value pair where key is either:<br><br>at _name_ where name of an environment or module,<br><br>of _what_ where what is a symbol or function,  <br>to _offset_ search until negative integer ancestors back,  <br>go _offset_ jumps to negative integer ancestors back. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The environment or nil if not found. |

##### Remarks

If no argument are provided, scope returns the current environment. If offset is provided, it indicates the number of ancestors to search backward. Kewords of and to are used together to locate a function or symbol, while go is used to pick a specific environment relative to a starting environment.

##### Example

```

> (function foo {}

(let ?func (scope) ?symbol (symbol func))

(so {?inner (scope)}

(tell user ($ function scope ?func \\n))

(tell user ($ inner scope ?inner \\n)))

(tell user ($ parent of inner scope (scope at ?inner go -1) \\n)))

(tell user ($ location of ?symbol (scope of ?symbol to -10) \\n))))

.:  foo

> (foo)

function scope Environment-2

inner scope Environment-3

parent of inner scope Environment-2

location of ?func scope Environment-1

.:  told

```

##### Related

do, function, given, global, invoke, local, modular

## seal

Prohibits new records.

##### Syntax

(seal _prototype_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| prototype | literal | 1   | The name of a relation. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns sealed |

##### Remarks

Calling the new function on a sealed relation shall fail. Sealed relations must be unsealed before the new function shall work again.

##### Example

```

> (relation Q)

.:  Q

> (new Q)

.:  Q_1

> (seal Q)

.:  sealed

> (new Q)

.:  \[Failure :Name Permission :Text "Attempt to modify sealed relation Q"\]

> (unseal Q)

.:  unsealed

> (new Q)

.:  Q_2

```

##### Related

relation,structure, unseal

## secant

Calculates the secant of the number.

##### Syntax

(secant number geometry metrum)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The secant of the number. |

##### Remarks

None.

##### Example

```

> (secant 0.785398)

.:  1.41421333

> (secant cir 0.785398 radians)

.:  1.41421333

> (secant cir 75 degrees)

.:  3.863703305

> (secant hyp 10 degrees)

.:  0.98496007966

> (secant hyp 0.0872665 radians)

.:  0.9962043239686199

```

##### Related

acosecant, asecant, cosecant

## seconds

Creates a seconds value or returns seconds since year zero.

##### Syntax

(seconds _seconds_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| seconds | variant | 0-1 | The number of seconds as an integer or time. |

##### Results

| Data Type | Description |
| --- | --- |
| second | The argument converted to seconds, or seconds since the year zero. |

##### Remarks

If no argument is supplied, this function returns the current date and time since the year zero in seconds, otherwise it attempts to construct a second atom from the supplied argument.

##### Example

```

> (seconds)

.:  \\@s63698773193

> (seconds 546)

.:  \\@s546

> (if (< (seconds) eternity)

(tell user ($ Now is less than the infinite future. \\n)))

Now is less than the infinite future.

.:  told

> (if (> (seconds) neternity)

(tell user ($ Now is greater than the infinite past. \\n))

Now is greater than the infinite past.

.:  told

```

##### Related

date, moment, paused, tick

## securelink

Creates a secure link.

##### Syntax

(securelink _option_ _…_ )

(securelink _address_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| address | string | 0-1 | The url address. |
| option | expression | 0+  | A key value pair. One of<br><br>user _credentials_ \-user name and password<br><br>host _host_ \- host computer name (default is localhost)<br><br>port _number_ – a port number. (default is 2001)<br><br>path _path_ – a path<br><br>query _query_ – a query element<br><br>fragment _fragment_ – a fragment element |

##### Results

| Data Type | Description |
| --- | --- |
| service | A file resource |

##### Remarks

Returns a secure link.

##### Example

```

> (function reply {?target ?request} (tell ?target "goodbye."))

.:  reply

> (service (var ?service (securelink "https://localhost:4500/foxxy")) reply)

.:  Service-1

> (ask ?service "hello")

.:  "goodbye."

> (cancel Service-1) (free ?service) (free Service-1)

.:  cancelled freed freed

```

##### Related

close, erase, path, pipe, read, socket, write

## seek

Repositions a file resource to a new read/write location.

##### Syntax

(seek _file position_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| file | file | 1   | An file resource. |
| position | variant | 1   | A byte position in the file, or 1 (beginning), or \# (end). |

##### Results

| Data Type | Description |
| --- | --- |
| file | Returns the file resource. |

##### Remarks

None.

##### Example

```

> (set ?file (file name "test.txt"))

.:  File-1

> (read ?file #)

.:  "Hello"

> (seek ?file 1)

.:  File-1

> (write ?file "Goodbye")

.:  File-1

> (close ?file)

.:  closed

```

##### Related

bytes, close, file, read, write

## self

Returns the currently executing task resource.

##### Syntax

(self)

##### Module

Tasks

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| task | The task resource for the executing task. |

##### Remarks

None.

##### Example

```

> (self)

.:  task-0

> (concurrent (tell user ($ My task is (self) \\n)))

My task is task-4

.:  {task-4}

```

##### Related

wait, abort, concurrent, await, complete, reclaim, task, tasks

## separator

Creates a separator string.

##### Syntax

(separator _kind_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| kind | literal | 0-1 | One of scheme, volume, folder (default), file, path, port, unchost, uncpath. |

##### Results

| Data Type | Description |
| --- | --- |
| string | A folder or volume separator character. |

##### Remarks

None.

##### Example

```

> (separator)

.:  "/"

> (separator path)

.:  "/"

> (separator scheme)

.:  "//"

> (separator volume)

.:  ":/"

> (separator port)

.:  ":"

> (separator file)

.:  "."

```

##### Related

file, folder, path, url

## series

Creates a serial iterator.

##### Syntax

(series _iterable_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| iterable | variant | 1   | A sequence, assortment, or stream,. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | returns the last expression. |

##### Remarks

The iterable must be either a sequence, assortment, or stream..

##### Example

```

> (function walk {?iterable}

(ensure {sequence assortment stream} ?iterable)

(let ?series (series ?iterable))

(map (infix (so {?e nil ?result {}}

(reset ?series)

(while (next ?series)

(set ?e (this ?series))

(add ?result (do ($ ?e))))

?result)

",")

(given {?x} (tell user ?x)))

walked)

.:  walk

> (walk {a b c})

a, b, c.: walked

> (walk (lexicon a 1 b 2 c 3))

{a 1}, {b 2}, {c 3}, .: walked

```

##### Related

next, reset, this

## service

Creates a service.

##### Syntax

(service _url_ _handler_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A Universal Resource Locator.. |
| handler | function | 1   | An message handler function. |

##### Results

| Data Type | Description |
| --- | --- |
| Service | The Service task. |

##### Remarks

This function creates an asynchronous service task that processes messages. The handler function shall receive the sender’s url, and an optional message string so that it may return a response.

##### Example

```

> (let ?url (url scheme tcp port 5001))

.:  true

> (function reply {?sender ?message}  
(tell ?sender "OK"))

.:  reply

> (start (service ?url reply))

.:  Service-3

> (ask ?url "How are you?")

.:  "OK"

> (free (cancel Service-3))

.:  freed

```

##### Related

agent, ask, cancel, free, tell, start

## set

Assigns variables to values. .

##### Syntax

(set _manner assignment_ _..._ )

_assignment ::= symbol value_

_assignment ::=_ {_symbol_ _..._ } _list_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed<br><br>either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| Truth | Returns true. |

##### Remarks

If a list of variables is provided for an assignment, then the value must be a list with the corresponding number of elements. The symbol must have previously been defined otherwise a symbol not found failure shall occur. If parallel is specified as the manner, the variables are defined in parallel, otherwise the variables are assigned in tandem (by default).

##### Example

```

> (set ?person DrWho)

.:  true

> ?person

.:  DrWho

> (set parallel ?x 1 ?y 2 ?z 3)

.:  true

```

##### Related

<-- _before tie_ , --> _after tie_, dynamic, global, let, local, modular, only, scope, tie

## sever

Creates a new assortments by removing keys.

##### Syntax

(sever _assortment key_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| key | variant | 1+  | A key. |

##### Results

| Data Type | Description |
| --- | --- |
| assortment | The new assortment. |

##### Remarks

Assortments are modified destructively. To delete nondestructively use the remove function.

##### Example

```

> (entries (collection a b c d))

.:  {{a a} {b b} {c c} {d d}}

> (entries (sever (lexicon a 1 b 2 c 3 d 4) b d))

.:  {{a 1}{c 3}}

```

##### Related

cut, rip, remove

## shuffle

Creates a reordered sequence.

##### Syntax

(shuffle _sequence seed_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string. |
| seed | number | 0-1 | A randomization seed. |

##### Results

| Data Type | Description |
| --- | --- |
| list | The list reordered. |

##### Remarks

None..

##### Example

```

> (global ?Alphabet {a b c d e f g h i j k l m n o p q r s t u v w x y z})

.:  true

> (shuffle ?Alphabet)

.:  {v z e g s y c b t h x o p I q a d r k l n u m j f w}

> (shuffle ?Alphabet 123)

.:  {y g l r x b k u t a j q f c d i s h e m v p n z o w}

> (shuffle ?Alphabet 123)

.:  {y g l r x b k u t a j q f c d i s h e m v p n z o w}

> (shuffle "abcdefghijklmnopqrstuvwxyz" (tick))

.:  "pnitdvjbqyuxkfazorecmwgslh"

```

##### Related

pick, random

## sigma

Calculates the sigma of a sequence.

##### Syntax

(sigma _list_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| list | list | 1   | A list. |
| of | literal | 0-1 | The literal of. |
| kind | literal | 0-1 | Either population or sample. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The standard deviation |

##### Remarks

Returns the amount of variation or dispersion of the list. Low deviation indicates the values are close to the mean while high deviation indicates values are more spread out.

##### Example

```

> (sigma {1 2 3 4} of population)

.:  1.118033988749895

> (sigma (map {{apple 1}{pear 2}{banana 3}{coconut 4}} (given {?e} (@ ?e 2)))

of population)

.:  1.118033988749895

> (sigma (range 1000 to 3000000 by 10000) of sample)

.:  866020.5925188307

> (sigma (range 100 to 3000 by 100) of sample)

.:  865.544144839919

```

##### Related

probability, range, statistics

## signal

Signals a condition.

##### Syntax

(signal _condition_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | premise | 1   | The condition to be signalled. |

##### Results

| Data Type | Description |
| --- | --- |
| premise | A premise indicating the signalled information. |

##### Remarks

A premise is required. If no arguments are supplied, a generic failure premise is constructed. The premise is thrown to an encompassing try form and the learn symbol is set to the premise. If no encompassing try form exists, the interpreter is halted with the sign as the error.

##### Example

```

> (try

(try

(signal \[Failure :Name User :Text "A big problem"\])

learn ?e

(tell user ($ Learned ?e \\n))

(tell user ($ Signaling... \\n))

(signal ?e))

learn ?f

(tell user ($ Learned ?f again. \\n))

finally

done)

Learned \[Failure :Name User :Text "A big problem"\]

Signaling...

Learned \[Failure :Name User :Text "A big problem"\] again

.:  done

```

##### Related

confirm, confute, ensure, escape, signal, try

## significand

Calculates the modified significand as zero, or a number from 1 to 10.

##### Syntax

(significand _number kind_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |
| kind | literal | 0-1 | One of normed, scientific (default), or integer. |

##### Results

| Data Type | Description |
| --- | --- |
| number | A number between 1 and 10, or 0.0. |

##### Remarks

The normed significand represents the number as a fraction (0.nnnn). The scientific significand represents the number as a decimal between 1.0 and 10.0 (n.nnnn). The integer significand represents the number as an integer (nnnn).

##### Example

```

> (significand 500.645 integer)

.:  500645

> (significand 0)

.:  0.0

> (significand -12345 normed)

.:  0.12345

> (significand -2302.023900 scientific)

.:  2.3020239

```

##### Related

digit, digits, exponential, fractional

## signum

Returns the sign of a number as a number, sigil, or word.

##### Syntax

(signum _number option_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A real number. |
| option | expression | 0+  | One of<br><br>part _which_ - where which is real (default)or imaginary<br><br>format _output_ - either number (default) , glyph or word. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the literal + if the number is positive or zero, or the literal - otherwise. |

##### Remarks

By default , this function returns the number 1 if positive, the number 0 if zero, or -1 if negative. If the format is glyph, then If the number is positive this function returns the plus character "+", if zero it returns space character " ", otherwise it returns the minus character "\-". When the format is word then it returns positive or zero, or negative,.

##### Example

```

> (signum 500)

.:  1

> (signum 0 format number)

.:  0

> (signum -1000+32i part real format word)

.:  negative

> (signum 500 format glyph)

.:  "+"

```

##### Related

digit, digits, exponential, fractional, significand

## sine

Calculates the sine of a number.

##### Syntax

(sine number geometry metrum)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The sine of the number. |

##### Remarks

None.

##### Example

```

> (sine 0.785398)

.:  0.7071066656

> (sine cir 0.785398 radians)

.:  0.7071066656

> (sine cir 45 degrees)

.:  0.7071067811

> (sine hyp 1.5708 radians)

.:  2.30130811905

> (sine hyp 90 degrees)

.:  2.30129890230

```

##### Related

asine, cosine

## so

Creates a lexical scope.

##### Syntax

(so _bindings expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| bindings | list | 0+  | A list of symbol value pairs or taxon symbol value triples. |
| expression | variant | 0+  | An expression. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last expression. |

##### Remarks

Any new variables declared shall shadow any prior variables with the same name. The so special form is a shortcut for (do (let ?s1 v1 …} …).

##### Example

```

> (so {?file (file name "myfile.out") }

(seek ?file #)

(for ?s in ?message (write ?file ($ ?s)))

(close ?file))

.:  closed

> (so {long ?n 1'000'000'000

big ?b 1}

(+ ?n ?b))

.:  \\#bd1000000001

```

##### Related

do, let, scope

## socket

Creates a TCP socket.

##### Syntax

(socket _option_ _…_ )

##### odule

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 0+  | A key value pair. One of<br><br>scheme _scheme_ \- either tcp (default) or udp<br><br>user _username_ \-user name<br><br>password _password_ \- password<br><br>host _host_ \- host computer name (default is localhost)<br><br>port _number_ – a port number. (default is 2001)  <br>address _url_ \- the uniform resource locatior as string |

##### Results

| Data Type | Description |
| --- | --- |
| io resource | A file resource |

##### Remarks

Opens a port for reading or writing and returns a socket.

##### Example

```

> (function reply {?target ?request} (tell ?target "goodbye."))

.:  reply

> (service (var ?socket (socket "http://localhost:4500/foxxy")) reply)

.:  Service-1

> (ask ?socket "hello")

.:  "goodbye."

> (cancel Service-1) (free ?socket) (free Service-1)

.:  cancelled freed freed

```

##### Related

close, erase, path, pipe, read, service, write

## some

True if the test is true for any element in the sequence.

##### Syntax

(some _symbol_ _…_ _binding_ _sequence expression_ … _test_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration symbol |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if any element satisfies the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the variables then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example

```

> (some ?x in {a b c d} (= ?x c))

.:  true

> (some ?m ?n per {{2 1} {3 4}} (< ?m ?n))

.:  true

> (some ?m ?n over {4 3 2 7} (divisible-p ?m ?n))

.:  false

```

##### Related

every, few, nevery, none, most

## sort

Creates a sorted sequence.

##### Syntax

(sort _sequence ordering option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The string or list to sort |
| ordering | variant | 1   | an ordering is either:<br><br>a direction, i.e. < (ascending) or > (descending)<br><br>for a sequence of atoms, or<br><br>an ordered list of slot direction pairs<br><br>(e.g. , { slot dir slot dir ...} )<br><br>if the elements are premises or tuples, or<br><br>an ordered list of position direction pars<br><br>(e.g., {position dir position dir ...} )<br><br>if the elements are sequences.<br><br>an ordered list of key direction pairs<br><br>(e.g., {key dir key dir ...} )<br><br>if the elements are assortments. |
| option | expression | 0+  | A key value pair containing any of the following keys:<br><br>comparer - a comparison function (uses the compare function if this key value pair is not supplied).<br><br>transform - function to retrieve a value given an item<br><br>key – a alist key (if sequence is a alist)<br><br>index – a list index (if sequence is a list of lists)<br><br>minval – a minimum value to consider in card sort<br><br>maxval – a maximum value to consider in card sort<br><br>limit - a number of items to return after sorting<br><br>algorithm - value one of { tree, card } default is tree |

##### Results

| Data Type | Description |
| --- | --- |
| list | The sorted list |

##### Remarks

The typical ordering is < for ascending and > for descending.

##### Example

```

> (sort {1 2 8 9 3 6 2} <)

.:  {1 2 2 3 6 8 9}

> (sort {1 2 8 9 3 6 2} >)

.:  {9 8 6 3 2 2 1}

> (Relation N :Value 0)

.:  N

> (for ?value in (range 1 to 10) (new N :Value (random 1 to 100))

.:  55

> (sort (with N :Value as ?v list ?v) <)

.:  {4 27 38 41 55 68 83 94 97}

> (sort {{A 1}{C 3}{F 6}{B 2}{D 4}{E 5}} {2 >})

.:  {{F 6}{E 5}{D 4}{C 3}{B 2}{A 1}}

> (sort {{Letter A Number 1}{Letter C Number 3}{Letter B Number 2}}

{Letter >})

.:  {{Letter C Number 3}{Letter B Number 2}{Letter A Number 1}}

```

##### Related

align, apply, best, count, gather, map

## split

Creates a list of subsequences divided at a delimiter.

##### Syntax

(split _sequence delimiter_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or a string. |
| delimiters | sequence | 0-1 | A sequence of delimiters.(Default is space character) |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of subsequences. |

##### Remarks

Returns a list of sequences split at a delimiter. The delimiter is not included in the result.

##### Example

```

(split "the quick brown fox")

.:  {"the" "quick" "brown" "fox"}

(split {the quick brown fox jumped over the lazy dogs} {the})

.:  {{quick brown fox jumped over} {lazy dogs}}

```

##### Related

$ _concatenate_ , capitalize, char, infix, lexemes, lowercase, ngrams, take, trim, unicode, uppercase

## start

Starts an agent, cell, or task.

##### Syntax

(start _compute arugment_ _…_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| compute | compute | 1   | An agent, cell, or task. |
| argument | variant | 0+  | An argument to the compute |

##### Results

| Data Type | Description |
| --- | --- |
| compute | Returns the argument. |

##### Remarks

This function starts an asynchronous agent task that processes incomingc messages and performs a default job.

##### Example

```

> (let ?url (url scheme tcp port 5001))

.:  true

> (function reply {?sender ?message} (tell ?sender "OK"))

.:  reply

> (function job {& ?args} (tell user ($ 1)) (wait 0.5))

.:  job

> (agent ?url reply job)

.:  Agent-1

> (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1)

111111.: cancelled freed

```

##### Related

ask, cancel, listen, pause, perform, start, tell

## starts-p

True if two intervals start together.

##### Syntax

(starts-p _interval<sub>1</sub> interval<sub>2</sub> tolerance_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if interval1 starts with interval2. |

##### Remarks

None.

##### Example

```

> (starts-p \\@i{\\@s1 \\@s2} \\@i{\\@s3 \\@s4})

.:  false

> (starts-p \\@i{\\@s1 \\@s5} \\@i{\\@s1 \\@s8})

.:  true

> (starts-p \\@i{\\@s1 \\@s9} \\@i{\\@s4 \\@s6})

.:  false

> (starts-p \\@i{\\@s4 \\@s6} \\@i{\\@s4 \\@s9})

.:  true

> (starts-p \\@i{\\@s5 \\@s9} \\@i{\\@s3 \\@s9} \\@s2)

.:  true

```

##### Related

before-p, during-p, finishes-p, meets-p, overlaps-p

## statistics

Finds the mean, median, sigma, and count of a list of numbers.

##### Syntax

(statistics _numbers_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| numbers | list | 1   | A list of numbers. |

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns an association list containing the mean, median, sigma, min, max. and count. |

##### Remarks

None.

##### Example

```

> (statistics (array (random 0 to 1000) each (random 0 to 10000)))

.:  {mean 5601.26666 median 5701 sigma 3692.856193 min 43 max 9444 count 368}

> (statistics {6 3 1 1 5 1 0 5 5 0 2})

.:  {mean 2.636363 median 2 sigma 2.1436047 min 0 max 6 count 11}

```

##### Related

probability, survey

## step

Loops a symbol over a numeric range to evaluate expressions.

##### Syntax

(step _symbol_ from _i_ _limit_ _j_ by _k expression_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | An index symbol to be incremented |
| from | literal | 1   | from |
| i   | number | 1   | The initial value of the symbol |
| limit | literal | 1   | The literal to, above, below or go. (default is to). |
| j   | number | 1   | The final value of the symbol |
| by | literal | 0-1 | by  |
| k   | number | 0-1 | The positive or negative increment for the symbol |
| expression | expression | 0+  | The expression(s) to be evaluated |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last expression on the last iteration of the loop |

##### Remarks

If to is specified, the _j_ value is included in the iteration. If below is specified the _j_ value is excluded from the iteration. If above is specified the next number above the _j_ value is included in the iteration. If go is specified, then the _j_ value specifies the number of iterations.

##### Example

```

> (step ?n from 1 below 5 (tell user ($$ ?n , (\\s))))

1, 2, 3, 4, .: nil

> (step ?i from 1 to 9 by 2 (tell user ($$(( ?i \\s)))

1 3 5 7 9 .: told

> (step ?i from 100 go 5 (tell user ($$ ?i \\s)))

100 101 102 103 104 .: told

```

##### Related

do, for, loop, repeat, until, while

## stream

Creates a stream.

##### Syntax

(stream _streamable_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| streamable | variant | 0+  | A file, pipe, string, or url.. |

##### Results

| Data Type | Description |
| --- | --- |
| stream | A stream resource. |

##### Remarks

A stream is a potentially infinite byte array containing serialized expressions. Serializations can be prepended to, appended to, or taken from the stream.

##### Example

```

> (function unstream {?s}

(decode (trim (string ?s) cut "|") base16))

.:  unstream

> (var ?s (stream "The quick brown fox jumped over the lazy dogs."))

.:  |540068006500200071007500690063006b002000620072006f0077006e00200066006f00780020006a0075006d0070006500640020006f00760065007200200074006800650020006c0061007a007900200064006f00670073002e00|

> (unstream ?s)

.:  "The quick brown fox jumped over the lazy dogs."

```

##### Related

append, takeable, take, peek, peep, prepend, stream-p

## string

Converts a value to a string.

##### Syntax

(string _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| string | The converted value. |

##### Remarks

None.

##### Example

```

> (string {a b c})

.:  "{a b c}"

> (string "a b c" (\\s) "d e f")

.:  "\\"a b c\\" \\"d e f\\""

> (string 500 50 5)

.:  "500 50 5"

> (string \[A :B :C\])

.:  "\[A :B :C\]"

> (string the quick "brown" fox)

.:  "the quick \\"brown\\" fox"

> (string)

.:  ""

```

##### Related

$ _concatenate_, $$ _elide_, is

## structure

Creates a structure.

##### Syntax

(structure _name_ _inclusion_ _…_ _definition_ _…_ )

_inclusion_ ::= uses { _structure_ _…_ }

_definition_ ::= _slot_

_definition_ ::= _slot default_

_definition_ ::= _method function_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of the structure. |
| inclusion | expression | 0+  | The literal uses followed by a list of structure names. |
| definition | expression | 0+  | A slot definition or method definition expression |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The name of the structure. |

##### Remarks

Structures are assortment prototypes which represent ephemeral relationships among one or more values. A structure record is called an ephemeron and is comprised of a name, slots with optional default values, and methods. Like the name implies, ephemerons are immediate unpersisted objects. This stands in contrast to thoughts which are persisted in the object store. Both structure and relation definitions are persisted in the object store. Structure ephemerons are created using the new function. The Failure prototype is an example of a structure. A prototype is a relation or structure.

##### Example

```

> (structure Fault

:What

:When

:Where

)

.:  Fault

> (new Fault :What "An error" :When (moment) :Where "Over Here")

.:  \[Fault :What "An error" :When \\@m20180561212150036 :Where "Over Here"\]

> (structure Error

uses {Fault}

:Who )

.:  Error

> (new Error :Who MyFunction :What "Punted." :When (moment) :Where "Here")

.:  \[Error :Who MyFunction :What "Punted." :When \\@m20180561212489526 :Where "Here"\]

```

##### Related

is, new, nix, relation, seal, structures, unseal

## structures

Creates a list of all structures.

##### Syntax

(structures)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of all structures. |

##### Remarks

None

##### Example

```

> (structure Foo :Bar :Baz)

.:  Foo

> (structures)

.:  {Failure Foo}

```

##### Related

new, nix, old, relation, relations,seal, structure, unseal

## sub

Replaces a subsequence within a sequence.

##### Syntax

(sub _sequence entry_ _…_ )

_entry_ ::= _start_ to _end replacement_

_entry_ ::= _start_ go _length replacement_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | An assortment or sequence. |
| entry | expression | 1+  | A 4-tuple of the start position, either to position or  go length, and the replacement sequence |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | Returns the modified sequence. |

##### Remarks

Each replacement is inserted into the sequence at the indicated positions. .

##### Example

```

> (sub {the quick red fox jumped} 2 to 4 {cute pink rabbit} )

.:  {the cute pink rabbit jumped}

> (sub "abcdefghij" 4 go 3 "456")

.:  "abc456ghij"

> (sub "the quick brown fox jumped" 11 go 5 "green" 17 to 19 "dog")

> "the quick green dog jumped"

.:  (sub {the quick brown fox jumped} 2 to 4 {cute rabbit})

.:  {the cute rabbit jumped}

```

##### Related

fix, put, replace, sub

## subset

True if all elements in each subset are in the superset.

##### Syntax

(subset-p _subset superset_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| subset | sequence | 1   | A sequence |
| superset | sequence | 1+  | A sequence |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if all elements of the subset are in the superset. |

##### Remarks

If superset and subset are strings and ordered is true, then a string search is performed.

##### Example

```

> (subset-p {a b x} {a b c d e f g})

.:  false

> (subset-p {a b d} {a b c d e f g})

.:  true  


> (subset-p "ick bro" "the quick brown")

.:  true

> (subset-p {g h i} {a b c d e f g})

.:  false

> (subset-p {e f d} {a b c d e f g})

.:  true

```

##### Related

disjoint-p, intersects-p, position, in, pick

## substitute

Modifies a sequence replacing subsequences.

##### Syntax

(substitute _sequence entries_ )

_entry_ ::= {{_start end replacement_ } _…_ }

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | An assortment or sequence. |
| entry | expression | 1   | A list containing lists of triples: the start position, end position and replacement subsequence |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | Returns the modified sequence. |

##### Remarks

Each replacement is inserted into the sequence at the indicated positions. .

##### Example

```

> (substitute {the quick red fox jumped} {{2 4 {cute pink rabbit}}} )

.:  {the cute pink rabbit jumped}

> (substitute "abcdefghij" {{4 7 "456"}})

.:  "abc456ghij"

> (substitute "the quick brown fox jumped" {{11 16 "green"}{17 19 "dog"}})

.:  "the quick green dog jumped"

> (substitute {the quick brown fox jumped} {{2 4 {cute rabbit}}})

.:  {the cute rabbit jumped}

```

##### Related

fix, put, replace, sub

## subsumes-p

True if all elements in each subset are in the superset.

##### Syntax

(subsumes-p _superset subset_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| superset | sequence | 1   | A list or string |
| subset | sequence | 1+  | A list or string |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if superset contains all elements of each subset. |

##### Remarks

None

##### Example

```

> (subsumes-p {a b c d e f g} {a b x})

.:  false

> (subsumes-p {a b c d e f g} {a b x} {a b d})

.:  true  


> (subsumes-p "the quick brown" "ick bro")

.:  true

> (subsumes-p {a b c d e f g} {d e f} {g h i})

.:  false

> (subsumes-p {a b c d e f g} {e f d})

.:  false

```

##### Related

disjoint-p, intersects-p, position, in, pick, subset-p

## sum

Calculates the arithmetic sum.

##### Syntax

(sum _value_ _…_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | An atom or list of atoms. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The arithmetic sum of all elements. |

##### Remarks

Returns the arithmetic sum. If the list or expression is empty, it returns zero. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example

```

> (sum {1 2 3 4 5})

.:  15

> (sum {})

.:  0

> (sum 1 2 3 4 5)

.:  15

> (sum {1 2 3} 4 {6 3 2})

.:  {11 9 9}

```

##### Related

avg, max, median, min, statistics, sigma

## summation

Adds an expression over a range of values.

##### Syntax

(summation _symbol_ _…_ _binding_ _sequence_ _expression_ _…_ )

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result of applying the plus function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the variables then the function fails. The last expression shall be evaluated and the plus function shall be applied to both that expression and any prior result. The final value is returned.

##### Example

```

> (summation ?x in (range 1 to 10) ?x)

.:  55

> (summation ?x in {1 2 3 4} (** ?x 2))

.:  25

> (summation ?n in {1 2 3} (+ ?n 5))

.:  21

```

##### Related

fold, maximum, minimum, product

## supply

Applies a function to an argument list.

##### Syntax

(supply _arguments function environment_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| arguments | list | 1   | A list containing actual parameters. |
| function | function | 1   | The name of a function to invoke |
| environment | environment | 0-1 | An environment. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The result from applying the function. |

##### Remarks

Applies the function to the list using the supplied environment, or the current scope if no environment is provided. The function is applied to the entire list and the result is returned.

##### Example

```

> (supply {1 2 3} +)

.:  6

> (consdier {?x 9} (let ?env (scope))(so {?x 3}(supply {1 2 ?x} + ?env)))

.:  12

```

##### Related

apply, call, count, gather, map, reduce

## suppose

Performs hypothetico-deductive reasoning.

##### Syntax

(suppose _facts_ action _goals_ by _strategies_ via _operators_ limit _quantity_

gate _condition_ within _timeframe_ before _timepoint_ options _options_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| _facts_ | variant | 1   | a list of expressions, or the literal “known” |
| action | literal | 1   | one of prove, refute, solve, infer, speculate, explain |
| _goals_ | list | 1   | a list of goal expression |
| by  | literal | 1   | the literal “by” |
| _strategies_ | list | 1   | a list of user defined search functions. |
| via | literal | 0-1 | the literal “via” |
| _operators_ | list | 0-1 | a list of operators |
| limit | literal | 0-1 | the literal “limit” |
| _quantity_ | number | 0-1 | the number of solutions/proofs to generate (default is 1) |
| gate | literal | 0-1 | one of while or until |
| _condition_ | truth | 0-1 | an expression which follows while or until (default is true) |
| within | literal | 0-1 | the literal “within” |
| _timeframe_ | number | 0-1 | a time duration (default is eternity) |
| before | literal | 0-1 | the literal “within” |
| _timepoint_ | number | 0-1 | an exact time (default is now + 60 seconds) |
| options | literal | 0-1 | the literal “options” |
| _options_ | lexicon | 0-1 | a lexicon or list. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns a solution or nil.<br><br>If the action is solve, each solution is a list of operators.<br><br>If the action is prove, each solution is a list of conclusion-operator pairs.<br><br>If the action is refute, each solution is a list of conclusion-operator pairs.<br><br>If the action is infer, a truth result tells if the goals are inferable from the facts<br><br>If the action is speculate, each solution is a conclusion-operator-probability triple.<br><br>If the action is appraise, each solution is a list of solution-cost pairs.<br><br>if the action is explain, each solution is a list of reasons. |

##### Remarks

Returns solutions (i.e. lists of operators) which transform the facts into the goals, or proofs (lists of operators as inference steps) showing the goals follow from the facts, or a truth indicating the goals are provable from the facts, by creating a monitor task and worker tasks which search for operator chains from facts to goals. The using funciton invokes all the supplied strategies (i.e. search functions) concurrently, canceling them if a condition dictates or a timeframe is passed. One or more result lists (up to the limit) is returned.

1.  If the action is solve, each solution is a list of operators.
2.  If the action is prove, each proof is a list of conclusion-operator pairs.
3.  If the action is refute, each proof is a list of conclusion-operator pairs.
4.  If the action is infer, a truth result determines if the goals are inferable from the facts.
5.  If the action is speculate, each proof is a list of conclusion-operator-probability triples.
6.  If the action is explain, each explanation lists the inferences linking goals to facts.

Each strategy (search function) needs to define keyword parameters which accept arguments from the using call. All the following keyword parameters are optional: solve, prove, infer, via, within, options. The strategy shall need to periodically check its own task identifier (by calling (cancelled-p (self)) to determine if the search task has been interrupted by the monitor task.

##### Example

```

> (structure Pegs

:Left

:Temp

:Right

)

.:  Pegs

> (function LeftToTemp {?state} ; a state is a list containing one Pegs structure.

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?left)(or (void-p ?temp) (< (@ ?left) (@ ?temp))))

{(new Pegs :Left (rest ?left) :Temp (& (@ ?left) ?temp) :Right ?right)}))

.:  LeftToTemp

> (function LeftToRight {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?left) (or (void-p ?right) (< (@ ?left) (@ ?right))))

{(new Pegs :Left (rest ?left) :Temp ?temp :Right (& (@ ?left) ?right))}))

.:  LeftToRight

> (function TempToRight {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?temp) (or (void-p ?right) (< (@ ?temp) (@ ?right))))

{(new Pegs :Left ?left :Temp (rest ?temp) :Right (& (@ ?left) ?right))}))

.:  TempToRight

> (function TempToLeft {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?temp) (or (void-p ?left) (< (@ ?temp) (@ ?left))))

{(new Pegs :Left(& (@ ?temp) ?left) :Temp (rest ?temp) :Right ?right)}))

.:  TempToLeft

> (function RightToTemp {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?right) (or (void-p ?temp) (< (@ ?right) (@ ?temp))))

{(new Pegs :Left ?left :Temp (& (@ ?right) ?temp) :Right (rest ?right))}))

.:  RightToTemp

> (function RightToLeft {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?right) (or (void-p ?left) (< (@ ?right) (@ ?left))))

{(new Pegs :Left (& (@ ?right) ?left) :Temp ?temp :Right (rest ?right))}))

.:  RightToLeft

> (relation Node

:Parent

:Operator

:State

:Children {}  
:Tried {}

:Task)

.:  Node

> (function depthFirstSearch {{facts ?facts}{solve ?goals}{using ?operators}

& ?rest}

(let ?root (new Node :State ?facts)

?visited {}

?useless {}

?current ?root

?stack {}

?solution nil)

(repeat

(let ?current :State ?state :Children ?children :Tried ?tried)

(if (and (void-p ?tried)

(void-p ?children))

;;; Expand current node.

(for ?operator in ?operators

(push ?children (new Node :Parent ?current :Operator ?operator

:Task (self))))

(put ?current :Children ?children)

or (more-p ?children)

;;; Expand a child

(set ?child (pick ?children))

(enq ?current :Tried ?child)

(deq ?current :Children ?child)

(so {?state ((:Operator ?child) (:State ?current))}

(put ?child :State ?state)

(if (null-p ?state)

(push ?useless ?child)

or (= ?goals ?state)

(set ?solution (map (rest ?stack) :Operator))

or (in ?visited ?state transform :State)

(push ?useless ?child)

else

(push ?stack ?current)

(push ?visited ?child)

(set ?current ?child)))

else

;;; Backtrack

(if (more-p ?stack)

(set ?current (pop ?stack))))

until (or ?solution

(void-p ?stack)

(cancelled-p (self))))

(with \[Node ^ ?n\] (= (:Task ?n) (self)) do (old ?p)))

?solution

)

.:  depthFirstSearch

> (function breadthFirstSearch{{facts ?facts}{solve ?goals}{using ?operators}

& ?rest}

(let ?root (new Node :State ?facts)

?visited {}

?useless {}

?current ?root

?solution nil)

(repeat

(let ?current :State ?state :Children ?children :Tried ?tried)

(if (and (void-p ?tried)

(void-p ?children))

;;; Expand current node.

(for ?operator in ?operators

(push ?children (new Node :Parent ?current :Operator ?operator)

:Task (self))))

(put ?current :Children ?children)

or (more-p ?children)

;;; Expand a child

(set ?child (pick ?children))

(enq ?current :Tried ?child)

(deq ?current :Children ?child)

(so {?state ((:Operator ?child) (:State ?current))}

(put ?child :State ?state)

(if (null-p ?state)

(push ?useless ?child)

or (= ?goal ?state)

(set ?solution (only {?child}

(so {?result {}}

(repeat (--> & ?result (:Operator ?child))

(set ?child (:Parent ?child))

until (null-p ?child))

(reverse (but ?result)))))

or (in ?visited ?state transform :State)

(push ?useless ?child)

else

(push ?frontier ?child)))

else

;;; Backtrack

(if (more-p ?frontier)

(set ?current (pop ?frontier))))

until (or ?solution

(void-p ?frontier)

(cancelled-p (self))))

(with Node ^ ?n (= (:Task ?n) (self))do (old ?p)))

?solution

)

.:  breadthFirstSearch

> (function TowersOfHanoi {% ?facts ?goals}

(suppose {(new Pegs :Left (@ ?facts) :Temp (@ ?facts 2) :Right (@ ?facts 3))}

solve {(new Pegs :Left (@ ?goals) :Temp (@ ?goals 2) :Right (@ ?goals 3))}

by {depthFirstSearch breathFirstSearch}

via {LeftToTemp LeftToRight TempToLeft TempToRight RightToTemp

RightToLeft})

)

.:  TowersOfHanoi

> (TowersOfHanoi facts {{1 2 3} {} {}} goals {{}{}{1 2 3}})

.:  {{LeftToRight LeftToTemp RightToTemp LeftToRight TempToLeft TempToRight LeftToRight}}

> (TowersOfHanoi facts {{3}{1 2}{}} goals {{}{}{1 2 3}})

.:  {{LeftToRight TempToLeft TempToRight LeftToRight}}

> (TowersOfHanoi facts {{1 2} {} {}} goals {{}{}{1 2}})

.:  {{LeftToTemp LeftToRight TempToRight}}

```

##### Related

wait, abort, concurrent, await, cancelled-p, complete, rule, self, tarry, with

## survey

Creates a list of referents or referent-count pairs.

##### Syntax

(survey _format_ _relation slot_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| format | literal | 1   | One of values, counts. |
| relation | relation | 1   | A relation |
| slot | slot | 1   | The slot of interest |

##### Results

| Data Type | Description |
| --- | --- |
| list | An association list or list of all values contained in the slot. |

##### Remarks

Returns a list values or an association list of counts (i.e., observations) for a relation slot

##### Example

```

> (relation Fruit :Color :Type)

.:  Fruit

> (new Fruit :Color red :Type apple) (new Fruit :Color red :Type cherry)

.:  Fruit_1 Fruit_2

> (new Fruit :Color red :Type strawberry)

.:  Fruit_3

> (survey values Fruit :Color)

.:  {red red red}

> (survey counts Fruit :Type)

.:  {{apple 1}{cherry 1}{strawberry 1}}

```

##### Related

probability, statistics

## symbol

Creates a symbol.

##### Syntax

(symbol _name environment_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| name | variant | 0-1 | A string, literal or integer. |
| environment | environment | 0-1 | An environment (defaults to the current scope). |

##### Results

| Data Type | Description |
| --- | --- |
| symbol | A symbol |

##### Remarks

The current environment is available via scope. If no arguments are suppled, then a new symbol is returned for the current context based on the value "v".

##### Example

```

> (symbol)

.:  ?v-1

> (use User)

.:  User

> (modular (symbol 500) nil (symbol) 350)

.:  true

> (entries (scope (use)))

.:  {{?500 nil} {?s-2 350}}

```

##### Related

<-- _before tie_, --> _after tie_, add, assign, assume, is, scope, set, tie, var, variables

## symbols

Lists the variables in an environment.

##### Syntax

(symbols _scope option_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | variant | 0-1 | A environment. or module. |
| opetion | expression | 0-1 | A key value pair, one of:  <br>ancestors _truth_ - Search ancestors. (Default is false.) |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of symbols defined in the environment, and parent environments. |

##### Remarks

If ancestors is true, then the symbols from parent environments are gathered recursively.

##### Example

```

> (let ?x 1 ?y 2 ?z 3) (scope)

.:  true {?x ?y ?z}

> (module Mine

(modular ?foo bar))

.:  Mine

> (variables (scope at Mine))

.:  {?foo}

> (so {?g 7 ?h 8 ?i 9}

(so {?d 4 ?e 5 ?f 6}

(so {?a 1 ?b 2 ?c 3}

(variables (scope) ancestors true))))

.:  {?a ?b ?c ?d ?e ?f ?g ?h ?i}

```

##### Related

environment, functions, module, modules, scope, var, symbol

## swap

Modifies a sequence by interchanging values.

##### Syntax

(swap _sequence substitution_ _…_)

_substitution_ ::= _prior-position later-position_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or a string. |
| substitution | expression | 1+  | A prior and later position pair.  <br>A position may be a number o a list of numbers.. |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The modified sequence |

##### Remarks

Destructively modifies the sequence. No changes occur if prior and later are the same. To create a new sequence use the exchange function.

##### Example

```

> (swap {A B C} 1 3)

.: {C B A}

> (swap "ABCD" 1 3)

.: 'CBAD'

> (swap {{1 2 3}{4 5 6}} {2 1} {1 3})

.:  {{1 2 4}{3 5 7}}

```

##### Related

@ _element_, append, exchange, fix, push, pop

## take

Creates an expression from a readable sequence.

##### Syntax

(take _readable options_ _…_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| readable | variant | 1   | An file, stream, or string. |
| options | expression | 0-2 | A key value pair, one of:  <br>start _position_ - Place to setart parrsing. (Default is 1).<br><br>limit _quantity_ - Number of parses to make (Default is 1.) |

##### Results

| Data Type | Description |
| --- | --- |
| expression | The parsed expression and the next position to parse in the readable. |

##### Remarks

Returns an expression containing a list of the extracted expression(s) according to SubThought Premise syntax, and the last parsed position in the readable. If limit is not supplied, the limit becomes one, the next expression is returned. If limit is greater than one then as many expressions are returned as can be extracted up to the limit. If # is provided as the limit, then all remaining expressions are returned. This function returns an empty expression if no expression could be extracted. It's recommended to test the argument prior to parsing using the takeable function.

##### Example

```

> (take (stream ""))

.:  0

> (take "hello world")

.:  hello 7

> (take (stream "hello world" #) start 7)

.:  world 12

> (take "{the quick brown fox} jumped over the lazy dogs" start 23 limit 3)

.:  jumped over the 39

```

##### Related

append, peek, prepend, skip, stream, stream-p, takeable, whitespace-p

## takeable

Calculates the number of expressions that can be read.

##### Syntax

(takeable _readable options_ _…_)

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| readable | variant | 1   | A stream, or file resource or a string containing zero or more expressions. |
| options | expression | 0-2 | A key value pair, one of:  <br>start _position_ - Place to setart parrsing. (Default is 1).<br><br>want _quantity_ - Number of parses to make (Default is #.) |

##### Results

| Data Type | Description |
| --- | --- |
| number | Calculates the number of actual expression that can be taken. . |

##### Remarks

If want is greater than one then as many expressions are tested for completeness as can be extracted up to the count. If # is provided, then all remaining expressions are tested for completeness. After testing, the resource shall be unchanged. Returns a number up to the number of desired expressions that can be successfully taken (because they are complete).

##### Example

```

> (global ?Stream (stream "The quick brown fox {jumped} "))

.:  true

> (takeable ?Stream)

.:  4

> (takeable ?Stream #)

.:  4

> (takeable ?Stream 2)

.:  2

```

##### Related

skip, append, take, peek, prepend, stream, stream-p

## tally

Returns the number of matches in the knowledge base.

##### Syntax

(tally _pattern option_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| pattern | pattern | 1   | A grounded premise |
| option | expression | 0+  | An option for retrieving the bindings.<br><br>limit n - the number of results to return. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of all symbol value pairs |

##### Remarks

Returns an anonymous list generator containing lists of symbol value lists.

##### Example

```

> (relation Poll :Response)

.:  Poll

> (step ?i from 1 to 1000

(new Poll :Response (on (> (radom 0 to 1) 0) Yes No)))

.:  Poll_1000

> (tally \[Poll :Respones Yes\])

.:  672

```

##### Related

tally, using, with

## tangent

Calculates the tangent.

##### Syntax

(tangent number geometry metrum)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Data Type | Description |
| --- | --- |
| number | The tangent of the number. |

##### Remarks

None.

##### Example

```

> (tangent 5)

.:  -3.38051500625

> (tangent 5 cir radians)

.:  -3.38051500625

> (tangent 120 degrees)

.:  1.7320508075

> (tangent 45 hyp degrees)

.:  0.655794202632

> (tangent (pi) hyp radians)

.:  0

```

##### Related

acotangent, atangent, cotangent

## tarry

Allows tasks to complete on their own.

##### Syntax

(tarry _tasks expression_ _…_) )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| tasks | variant | 1   | A task or list of task resources. |
| expression | variant | 0+  | An expression to evaluate after the tasks are completed. |

##### Results

| Data Type | Description |
| --- | --- |
| list | The task resources. |

##### Remarks

This function allows tasks to complete in a non-blocking manner. It is equivalent to

(given {?tasks}

(& ?tasks

(concurrent (do (until (every ?t in ?tasks (ready-p ?t))(idle \\@m1)) ready))))

##### Example

```

> (var ?tasks (tarry (concurrent (repeat 1000000 foo)

(repeat 2000000 bar)

(repeat 3000000 baz))))

.:  {task-1 task-2 task-3 task-4}

> (map ?tasks ({?t}(await ?t \\@s0)))

.:  {­foo bar baz done}

> (free (tarry (complete

(repeat 1000 foo)

(repeat 2000 bar)

(repeat 3000 baz))))

.:  freed

```

##### Related

wait, abort, concurrent, await, complete, do, done-p, free, task

## task

Creates a list of tasks for deferred evaluation.

##### Syntax

(task _cell scope_ _expression_ _…_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| cell | cell | 0-1 | A cell. |
| scope | environment | 0-1 | An environment. A child scope is created if not provided. |
| expression | expression | 1+  | Any expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of task resources, one resource for each expression. |

##### Remarks

The tasks need to be initiated with the concurrent or complete function.

##### Example

```

> (task (/ 1000 57) (** 4 20) (** 4 20))

.:  {Task-1 Task-2 Task-3}

> (concurrent task-1)

.:  {Task-1}

> (await task-1)

.:  17.54385964912281

> (concurrent task-2 task-3)

> (await task-2)

.:  1099511627776

> (await task-3)

.:  1099511627776

> (free {task-1 task-2 task-3})

.:  nil

> (function main {}

(let ?bion (bion) ?cell (cell ?bion))

(start ?cell)

(let ?task (task ?cell (scope) (given {string ?name} ($ Hello, ?name))))

(tell user (await (start ?task "World")))

(halt ?cell)

(halt ?bion)

(free ?cell)

(free ?bion)

)

.:  main

> (main)

Hello World

.:  freed

```

##### Related

wait, abort, concurrent, await, busy-p, cancel, cancelled-p, complete, critical, do, is, ready-p, reclaim , task

## tasks

Creates a list of all tasks.

##### Syntax

(tasks)

##### Module

Tasks

##### Parameters

None.

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list of task handles |

##### Remarks

This list does not include the interpreter task. To obtain the interpreter task, use the self function.

##### Example

```

> (task (apply + {1 2 3}))

.:  {Task-1}

> (complete (apply \* {1 2 3}))

.:  {Task-2}

> (tasks)

.:  {Task-2 Task-1}

> (free (tasks))

.:  freed

```

##### Related

wait, abort, concurrent, await, task, await, complete, reclaim, self, task

## taxon

Returns the taxonomic (i.e., data) type of a value.

##### Syntax

(taxon _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | A taxonomic type name |

##### Remarks

None

##### Example

```

> (taxon true)

.:  truth

> (taxon nil)

.:  nothing

> (taxon 12345)

.:  number

> (taxon #)

.:  literal

```

##### Related

convert, convertible, taxonomy, identity, is, meron, meronomy, relation, structure

## taxon-p

True if the value is of the specific taxonomic type.

##### Syntax

(taxon-p _value_ _taxon_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |
| taxon | literal | 1   | The name of a taxon. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is the taxon. |

##### Remarks

None.

##### Example

```

> (taxon-p 500 literal)

.:  false

> (taxon-p \\@t300 time)

.:  true

> (taxon-p "the quick brown fox" string)

.:  true

```

##### Related

meron, meron-p, meronomy, taxon, taxonomy

## taxonomy

Returns a list of taxonomic types for a value.

##### Syntax

(taxonomy _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |

##### Results

| Data Type | Description |
| --- | --- |
| list | The taxonomic types used |

##### Remarks

None

##### Example

```

> (taxonomy A)

.:  {literal atom thing}

> (taxonomy 100)

.:  {number atom thing}

> (taxonomy {a b c})

.:  {list sequence thing}

> (taxonomy \[A :B 1 :C 2\])

.:  {premise tuple sequence thing}

> (taxonomy \\@t522)

.:  {tick time atom thing}

```

##### Related

taxon, is, id, meron, meronomy, relation, structure

## tell

Sends a message to a recipient.

##### Syntax

(tell _who message option_ _…_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| who | literal | 1   | A URL web resource or the literal user. |
| message | string | 1   | A message or command.. |
| option | expression | 0+  | Key value pairs<br><br>timeout _instant_ – delay before terminating request,  <br>default _value_ – value to return upon timeout, |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns told if successful. If a default is provided then the default is returned in case of a timeout. |

##### Remarks

If user is specified for who, then the output is displayed to the console.

##### Example

```

> (tell user "Hello World!\\n")

Hello World

.:  told

> (function reply {?url ?message}

(tell ?url ($ received ?message)))

.:  reply

> (service (url scheme tcp port 5950) reply)

.:  Service-1

> (ask (url scheme tcp port 5950) "secret")

.:  "received secret"

> (free Service-1)

.:  freed

> (global ?Data (data source (get Settings-1 "/db/dsn")))

.:  true

> ?Data

.:  Data-1

> (open ?Data)

.:  Data-1

> (tell ?Data "update product set price = price \* 1.1025;")

.:  told

> (close ?Data)

.:  closed

```

##### Related

ask, listen,free

## there

True if a file, folder, or url actually exists.

##### Syntax

(there _url_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the url exists.. |

##### Remarks

This function checks whether or not the url exists.

##### Example

```

> (let ?url (ul path "quick.txt"))

.:  true

> (if (there ?url)

(let ?file (file url ?url seek 1 mode write erase yes))

(write ?file "The quick brown fox")

(close ?file))

.:  closed

```

##### Related

absent, file, folder, url

## this

The current element of a series.

##### Syntax

(this _series_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| series | series | 1   | A series. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the current value of the series. |

##### Remarks

The next function is used to advance a series to the first through last elements of an iterable thing. If this is called immediately after the creation of the iterable, or immediately after a reset of the iterable, or before the first next is called, then an out of range failure shall occur since the series is pointing to an unknown item before the first element. If this is called after next returns false, an out of range failure shall also occur because the series is pointing after the last element.

##### Example

```

> (function walk {?iterable}

(confirm (iterable-p ?iterable) since

"Argument to walk must be iterable")

(let ?series (series ?iterable))

(while (next ?series)

(tell user ($$ (this ?series) ,)))

walked)

.:  walk

> (walk {a b c})

a, b, c.: walked

> (walk (lexicon a 1 b 2 c 3))

{a 1}, {b 2}, {c 3}, .: walked

```

##### Related

next, reset, series

## thought

Finds an extant thought.

##### Syntax

(thought _relation id_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| relation | literal | 1   | A relation |
| id  | number | 1   | An instance number |

##### Results

| Data Type | Description |
| --- | --- |
| thought | A thought. |

##### Remarks

Returns an existing thought, otherwise signals a failure If the SubThought does not exist.

##### Example

```

> (relation E :Value)

.:  E

> (new E :Value 100)

.:  E_1

> (new E :Value 200)

.:  E_2

> (thought E 1)

.:  E_1

> (thought E 2)

.:  E_2

> (thought E 3)

.:  \[Failure :Name NotFound :Text "Thought E_3 was referenced but not found."\]

```

##### Related

^ SubThought _id_, id, is, premise

## thunk

Creates a thunk in a module.

##### Syntax

(thunk _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 0+  | Expressions to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| thunk | Returns the thunk containing the expressions. |

##### Remarks

A thunk is a parameterless anonymous function. A thunk is equivalent to lambda expression without parameters in the Lisp programming language, and can be used in most places a function name is required. Anonyms cannot be recursive, since they are unnamed. Continuations may be taken within an anonym. Neither do anonyms use tags that can be reference by a return. Since no parameters are specified, each expression is executed in succession and the value of the last expression is returned. The thunk is ephemeral because function definitions are not maintained for them.

##### Example

```

> (thunk (tell user "Hello, world."))

.:  (thunk (tell user "Hello, world."))

> (invoke (thunk (tell user "Hello, world.")))

Hello, world.

.:  told

```

##### Related

wait, abort, concurrent, await, complete, done-p, reclaim,task, use

## thunks

Returns a list of thunks defined in a module.

##### Syntax

(thunks _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module. If not provided defaults to the current module. |

##### Results

| Data Type | Description |
| --- | --- |
| list or nil | A list of functions defined in the module. |

##### Remarks

The module must be a literal in the list obtained by calling the (modules) function. If the module is not provided this function uses the current module (obtained via the (use) function).

##### Example

```

> (module Mine (thunk bar))

.:  Mine

> (thunks Mine)

.:  {thunk-1}

> (use User)

.:  User

> (thunk “hello world”)

.:  thunk-2

> (thunks)

.:  {thunk-2}

```

##### Related

function, module, modules, rule, rules, variables

## tick

Creates a tick or returns nanoseconds since year zero.

##### Syntax

(tick _nanoseconds_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| nanoseconds | number | 0-1 | A number of nanoseconds. |

##### Results

| Data Type | Description |
| --- | --- |
| tick | nanoseconds since the year zero. |

##### Remarks

If no argument is supplied, this function returns the current date and time in nanoseconds, otherwise it attempts to construct a tick from the supplied argument.

##### Example

```

> (tick)

.:  \\@t63552721198807000

> (tick 5465464)

.:  \\@t5465464

```

##### Related

date, moment, idle

## tie

Assigns variables to values. .

##### Syntax

(tie _manner assignment_ _..._ )

_assignment ::= symbol value_

_assignment ::=_ {_symbol_ _..._ } _list_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed<br><br>either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last assigned value. |

##### Remarks

If a list of variables is provided for an assignment, then the value must be a list with the corresponding number of elements. The symbol must have previously been defined otherwise a symbol not found failure shall occur. Returns the value of the last assignment. If parallel is specified as the manner, the variables are defined in parallel, otherwise the variables are assigned in tandem (by default).

##### Example

```

> (tie ?person DrWho)

.:  DrWho

> ?person

.:  DrWho

> (tie parallel {?x ?y ?z} {1 2 3})

.:  3

```

##### Related

<-- _before tie_, --> _after tie_, assume, constant, dynamic, given, global, local, set

## time

Performs time operations.

##### Syntax

(time _unit operation value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| unit | literal | 1   | one of { year, month, week, weekday, days, day, hour, minute, second, millisec, jiffy, moment, microsec, nanosec, tick, zone. zmin }. |
| operation | literal | 1   | One of {\+ (addition), - (difference), of, in, part, ytd} |
| value | time | 1+  | A time value |

##### Results

| Data Type | Description |
| --- | --- |
| number | The operation performed on the time value(s). |

##### Remarks

Returns the value of the operation in the specified units. If + is specified as the operation, the times are added together and the total is returned in the unit. If \- is specified as the operation, the difference of the times are returned in the specified unit. If of is specified for the operation, then the specified unit is extracted for the specified time value. If in is specified for the operation, then the total time value is converted to the units. If part is specified for the operation, and if the time is converted to a moment segment (day part takes a number between 1 and 366, returning a number between 1 and 999; hour part takes takes a number between 0 and 23, returning a number between 0 and 99; minute part takes a number between 0 and 59, returning a number between 0 and 99; seconds part takes a number between 0 and 59, returning a number between 0 and 99). If ytd is specified then the units are computed for the year to date for the date specified as the time. Otherwise the part of the time value is returned.

##### (imExample

```

> (time seconds - \\@s5 \\@s10)

.:  -5

> (time hour part 18)

.:  75

> (time seconds in \\@s26226)

.:  26226

> (time day ytd 2014-04-09T14:24:19.488Z)

.:  9

> (time month of (tick))

.:  12

> (time month of (moment))

.:  12

> (time month of (date))

.:  12

> (@ {mon tue wed thu fri sat sun} (time weekday part (date 2019 8 31)))

.:  sat

```

##### Related

date, epoch, interval, is, moment, second, tick

## top

Creates a subsequence of the first elements.

##### Syntax

(top _sequence count_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The sequence to search |
| count | number | 0-1 | The number of elements.( Default is 1.) |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A sub sequence containing the desired quantity of elements |

##### Remarks

None.

##### Example

```

> (top {a b c d e f g} 3)

.:  {a b c}

> (top {a b c d e f g})

.:  {a}

```

##### Related

@ _element_, but, last, rest

## transfer

Transfers a value from one sequence to another.

##### Syntax

(transfer _source destination option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| source | symbol | 1   | A symbol bound to a sequence |
| destination | symbol | 1   | A symbol bound to a sequence |
| option | expression | 0+  | A key value pair where the key is<br><br>from position - The position in the source (defaults to 1)<br><br>to position - The position in the destination (defaults to 1)  <br>unique prohibited (Boolean) - indicates if duplicate values are allowed. (Default is false.) |

##### Results

| Data Type | Description |
| --- | --- |
| value | Returns the value that was transferred. |

##### Remarks

Modifies two sequences by removing a value from the source and adding a value to the destination.

##### Example

```

> (let ?x {a b c d e f} ?y {})

.:  true

> (transfer ?x ?y)

.:  a

> (transfer ?x ?y unique true from 2 to 2)

.:  c

> ?x ?y

.:  {b d e f} {a c}

```

##### Related

but, exchange,last, pop, push, rest, reverse, swap, top

## traverse

Loops through the coordinates of a sequence.

##### Syntax

(traverse _symbol binding sequence_ limit _dimensions expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol holding the index or coordinates of the current element of the sequence. |
| binding | literal | 1   | One of the following:<br><br>into - varies the inner (rightmost) coordinates first<br><br>across - varies the outer (leftmost) coordinates first. |
| sequence | sequence | 1   | A possibly nested sequence. |
| limit | literal | 1   | the keyword literal limit |
| dimensions | list | 1   | if the keyword limit is supplied, then this is a list of indicies indicating the maximum dimensions that shall be traversed. |
| expression | expression | 0+  | An expression to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | This form returns the last expression. |

##### Remarks

This function returns last expression of the last iteration. The function assumes that the entire sequence has a uniform number of elements in each dimension. On each iteration the symbol is updated with the coordinates of the current element of the sequence. The into binding provides depth first traversal, while the across binding provides breadth first traversal.

##### Example

```

> (traverse ?i across {{a b}{c d}{e f}{g h}{i j}} limit {5 2} (tell user ($$ ?i \\s)))

{1 1} {2 1} {3 1} {4 1} {5 1} {1 2} {2 2} {3 2} {4 2} {5 2} .: told

> (traverse ?i into {{a b}{c d}{e f}{g h}{i j}} limit {5 2} (tell user ($$ ?i \\s)))

{1 1} {1 2} {2 1} {2 2} {3 1} {3 2} {4 1} {4 2} {5 1} {5 2} .: told

```

##### Related

add, includes, cut, for, item, items, keys, reclaim, values

## trim

Creates a sequence without leading and trailing delimiters.

##### Syntax

(trim _sequence_ _option_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The target sequence |
| option | expression | 0+  | A key value pair:<br><br>cut delimiters - a string or list containing the delimiters.<br><br>on location - the literal left, right, or both (default). |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | The modified sequence |

##### Remarks

Removes delimiter characters from the front or rear of a sequence. If the location is left, then only the left portion is trimmed. If the location is right, then only the right portion of the string is trimmed. If the location is both or if the location is omitted, then both the left and right portion of the sequence is trimmed.

##### Example

```

> (trim " the quick brown fox ")

.:  "the quick brown fox"

> (trim " the_quick_brown_fox \__" cut "\_")

.:  " the_quick_brown_fox "

> (trim " the quick brown fox " on left)

.:  "the quick brown fox "

> (trim {the quick brown fox} cut {the fox} on both)

.:  {quick brown}

```

##### Related

split

## truncate

Rounds a number towards zero.

##### Syntax

(truncate _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |

##### Results

| Data Type | Description |
| --- | --- |
| number | An integer |

##### Remarks

None.

##### Example

```

> (truncate 10.5)

.:  10

> (truncate 10.4)

.:  10

> (truncate 10.49)

.:  10

> (truncate -10.5)

.:  -10

> (truncate -10.4)

.:  -10

> (truncate -10.49)

.:  -10

```

##### Related

%, ceiling, floor, round,

## try

Evaluates expressions and handles signs.

##### Syntax

(try _expression_ _…_ learn _symbol_ _recovery_ _…_ finally _cleanup_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1+  | Expressions to do some processing |
| learn | literal | 1   | The literal learn |
| symbol | symbol | 0-1 | A symbol |
| recovery | expression | 0+  | Expressions for failure recovery and learning |
| finally | literal | 0-1 | The literal finally |
| cleanup | expression | 0+  | Expressions to do some clean up |

##### Results

| Data Type | Description |
| --- | --- |
| value | Returns last call in normal operation, or last failure call if a failure was thrown |

##### Remarks

The try special form performs signal handling. The signal function shall return to the learn tag and bind the thrown premise to the symbol.

##### Example

```

> (function main {& ?args}

(tell user ($ \\n Attempting dangerous operation... \\n))

(try

(dangerousOperation)

(tell user ($ \\n Goodbye \\n))

learn ?condition

(case (:Name ?condition )

of ResourceFailure

(tell user ($ Resource failure occurred \\n))

else

(tell user ($ \\n (:Text ?condition ) \\n)))

(tell user ($ \\n Goodbye \\n))

(signal ?condition ) ; rethrow failure

)

)

.:  main

)

> (main)

Attempting dangerous operation...

The function dangerousOperation was not found.

Goodbye

.:  \[Failure :Name User :Text "The function dangerousOperation was not found."\]

> (so {?file nil}

(try

(set ?file (file name "quick.txt" seek 1 mode read type text))

(tell user ($ (read ?file) \\n))

learn ?e

(signal ?e)

finally

(close ?file)))

The quick brown fox jumped over the lazy dogs.

.:  told

> ; implement a REPL.  


    (forever

(tell user ($ "\\n=>" (try (eval (ask user "\\n\* ")) learn ?failure))))

\* HELLO WORLD

\=> HELLO WORLD

\*

```

##### Related

can, confirm, confute, did, do, ensure, escape, fail, may, signal

## tuple

Creates a tuple.

##### Syntax

(tuple _value_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | Any value |

##### Results

| Data Type | Description |
| --- | --- |
| tuple | Returns a tuple containing the values. |

##### Remarks

A tuple can also be created by simply enclosing the elements with square brackets, \[ \].

##### Example

```

> (tuple a b c {d})

.:  \[a b c {d}\]

> (tuple "a b c")

.:  \["a b c"\]

> (tuple 500)

.:  \[500\]

> (tuple)

.:  \[\]

> \[a b c {d}\]

.:  \[a b c {d}\]

> \["a b c"\]

.:  \["a b c"\]

```

##### Related

&, inside, list-p, sequence-p  

## uuid

Creates a unique universal identifier.

##### Syntax

(uuid)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| uid | A new unique identifier. |

##### Remarks

None.

##### Example

```

> (uid)

.:  90A836B0-63E8-4049-B411-908A6B30F69F

> (uid)

.:  CE79CB00-F400-429A-BFC3-8F9801B7B017

```

##### Related

id, unique

## unbound

Creates a list of free variables in a function.

##### Syntax

(unbound _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of variables not declared in the parameter list (aka free variables). |

##### Remarks

None.

##### Example

```

> (function foo {?x ?y + ?z}

(bar ?x ?y)

(baz ?z ?a))

.:  foo

> (bound foo)

.:  {?x ?y ?z}

> (unbound foo)

.:  {?a}

> (bound (' (given {?s} (@ ?s ?p))))

.:  {?s}

> (unbound (' (given {?s} (@ ?s ?p))))

.:  {?p}

```

##### Related

bound

## unbound-p

True if a symbol is unbound.

##### Syntax

(unbound-p _symbol_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol. |

##### Results

| Data Type | Description |
| --- | --- |
| bool | True if the symbol is unbound. |

##### Remarks

None.

##### Example

```

> (let ?a 1 ?b 2)

.:  true

> (unbound-p ?a)

.:  false

> (unbound-p ?b)

.:  false

> (unbound-p ?c)

.:  true

```

##### Related

unbound-p

## unicode

The Unicode of a string’s first position.

##### Syntax

(unicode _string_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | input string |

##### Results

| Data Type | Description |
| --- | --- |
| number | The Unicode of the first position |

##### Remarks

None

##### Example

```

(unicode "A")

.:  65

(Unicode "apple")

.:  97

```

##### Related

char, format, lexemes, lowercase, ngrams, split, trim, uppercase

## union

Concatenates sequences removing duplicates.

##### Syntax

(union _sequence_ _sequence_ … )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | input sequences |

##### Results

| Data Type | Description |
| --- | --- |
| sequence | A single de-duped sequence. |

##### Remarks

None

##### Example

```

> (union {a b c} {b c d} {d e f})

.:  {a b c d e f}

> (union "abc" "bcd" "def")

.:  "abcdef"

```

##### Related

difference, disjoint, distinct, intersection

## unique

Creates a unique literal based on a prefix.

##### Syntax

(unique _prefix_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| prefix | variant | 0-1 | A literal or string prefix for the id. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | A new literal |

##### Remarks

If prefix is not provided the default prefix "G" is used. Hyphens and underscores are removed from the prefix. This function increments a counter to generate a new literal.

##### Example

```

(unique)

.:  G1

(unique)

.:  G2

(unique "hello")

.:  hello1

(unique My-Object)

.:  MyObject1

(unique "my_Object_")

.:  MyObject2

(unique "my-object-")

.:  MyObject3

```

##### Related

Id, uid

## unless

Branched conditional evaluation.

##### Syntax

(unless _condition_ _false-case_ _true-case_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| false-case | variant | 1   | An expression to evaluate |
| true-case | variant | 1   | An expression to evaluate |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The last value of the executed expression. |

##### Remarks

Evaluates the condition and either the true case or the false case.

##### Example

```

> (unless (> 101 100) (tell user "no") (tell user "yes"))

yes .: told

> (unless (< 101 100) (tell user "no") (tell user "yes"))

no .: told

```

##### Related

and, case, if, not, on, or

## unlike

True if a pattern does not matche a sequence.

##### Syntax

(unlike _sequence pattern_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A string or list of strings to be compared. |
| pattern | string | 1   | A regex pattern. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | If sequence is a string, then a truth is returned.<br><br>If sequence is a list, then a list of non-matches is returned |

##### Remarks

If the candidate argument is a list, then this function Creates a new list containing only those elements not matching the pattern. If the candidate is a string, then this function returns true if the pattern does not match the candidate, and false otherwise. Standard RegEx matching is used.

##### Example

```

> (unlike "abc" "bc")

.:  false

> (unlike "abc" "xy")

.:  true

> (unlike {"abc" "bcd" "def" "ghi"} "bc")

.:  {"def" "ghi"}

```

##### Related

like

## unqualified

The function literal without the module prefix.

##### Syntax

(unqualified _function_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function literal |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The function literal without a module |

##### Remarks

None

##### Example

```

> (unqualified Math.sum)

.:  sum

```

##### Related

qualified, qualifiers

## unseal

Permits new records for a protoytpe.

##### Syntax

(unseal _prototype_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| prototype | literal | 1   | The name of a prototype. |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns unsealed |

##### Remarks

Calling the new function on a sealed relation shall fail. Sealed relations must be unsealed before the new function shall work again.

##### Example

```

> (relation Q)

.:  Q

> (new Q)

.:  Q_1

> (seal Q)

.:  sealed

> (new Q)

.:  \[Failure :Name Permission :Text "Attempt to modify sealed relation Q"\]

> (unseal Q)

.:  unsealed

> (new Q)

.:  Q_2

```

##### Related

new, relation, seal, structure

## unsigned

Converts a value to an unsigned number.

##### Syntax

(unsigned _value_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Data Type | Description |
| --- | --- |
| integer | An integer number. |

##### Remarks

If the value is minimum (or maximum) the minimum (or maximum) unsigned number is returned; otherwise, if the value cannot be converted to an unsigned number, the function fails. The fractional part of the number shall be truncated.

##### Example

```

> (unsigned {a b c})

.:  \[Failure :Name ArgumentValue :Text "{a b c} is not a number."\]

> (unsigned "a b c")

.:  \[Failure :Name ArgumentValue :Text "'a b c' is not a number."\]

> (unsigned 500.3)

.:  500u

> (unsigned "23.4")

.:  23u

> (unsigned (\* 2 2))

.:  4u

```

##### Related

ceiling, complex, floor, is, long, rational, real, round, truncate  

## until

Loops expressions until a condition is true.

##### Syntax

(until _condition_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| expression | expression | 0+  | An expression to be evaluated |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value of the last iteration |

##### Remarks

None

##### Example

```

> (modular ?i 0)

.:  true

> (until (>= ?i 10) (idle \\@s1) (--> ++ ?i))

.:  10

```

##### Related

for, iterate, loop, repeat, step, while

## unwrap

Permits modifications to a module.

##### Syntax

(unwrap _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | A module |

##### Results

| Data Type | Description |
| --- | --- |
| literal | Returns unwrapped |

##### Remarks

This function has no effect on already unwrapped modules.

##### Example

```

> (module Math

(function sum ?args (apply + ?args)))

.:  Math

> (wrap Math)

.:  wrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.:  \[Failure :Name Permission :Text "Can't modify a wrapped module"\]

> (unwrap Math)

.:  unwrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.:  Math

```

##### Related

extend, module, wrap

## uppercase

Converts a string touppercase.

##### Syntax

(uppercase _string_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A value to convert |

##### Results

| Data Type | Description |
| --- | --- |
| string | The converted string |

##### Remarks

None

##### Example

```

> (uppercase "the quick brown fox")

.:  "THE QUICK BROWN FOX"

```

##### Related

capitalize, lexemes, lowercase

## uppercase-p

True if a string's first position is upper case.

##### Syntax

(uppercase-p _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the value is a string and its first position is upper case. |

##### Remarks

None

##### Example

```

> (uppercase-p "the quick brown fox")

.:  false

> (uppercase-p "This and that")

.:  true

```

##### Related

letter-p, lowercase-p

## url

Creates a URL resource.

##### Syntax

(url _option_ _…_ )

(url _address_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| address | string | 0-1 | The url address. |
| option | expression | 0+  | A key value pair. One of<br><br>scheme _scheme_ \- the url scheme (e.g., file, http, https)<br><br>user _user_ \- the name of the user<br><br>password _password_ \- the password of the user<br><br>host _host_ - hostname or the literal ip for this ip address<br><br>port _port_ \- port number or the literal new<br><br>path _path_ \- file path<br><br>query _query_ \- query key value pairs.<br><br>fragment _fragment_ - section specification..<br><br>address _url_ - A full url address. |

##### Results

| Data Type | Description |
| --- | --- |
| url | A url resource. |

##### Remarks

If no arguments are provided, then this function returns the universal resource locator for the SubThought Premise interpreter running on the current machine. If new is specfied as the port, an unused port number is utilized.

##### Example

```

> (url scheme https host "www.youtube.com" path "watch" query "v=kqicbyONxO8")

.:  Url-1

> (address Url-1)

.:  "https://www.youtube.com/watch?v=kqicbyONxO8"

```

##### Related

address, ask, is, listen, tell

## use

Creates a scope for knowledge based operations.

##### Syntax

(use _knowledge expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| knowledge | variant | 1   | A knowledge base or url to a knowledge base. |
| expression | variant | 0+  | An expression. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last expression. |

##### Remarks

The use function creates a scope by attaching to the knowledge base, evaluating the expressions, then detaching from the knowledge base. The last expression is returned.

##### Example

```

> (use (knowledge url "file:///c:/premise/kb/defultKb.mdb")

(relation Fact :All :Are)

(new Fact :All people :Are mortal)

(new Fact :All philosophers :Are people)

(with \[Fact :All as ?x :Are as ?y\]

\[Fact :All = ?y :Are as ?z\]

list (knew \[Fact :All ?x :Are ?z\]))

)

.:  Fact_3

> (use

(knowledge name Mathematics path "c:/premise/kb/" units MB size 2 max 10

log 1 growth 10)

(relation Circle :Radius)

)

.:  Circle

```

##### Related

attach, detach, each, get, knowledge, put, using, which, with

## using

Accesses a scope.

##### Syntax

(using _scope expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| scope | variant | 1   | An environment or module name. |
| expression | variant | 0+  | An expression. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last expression. |

##### Remarks

The using function accesses a scope by attaching to scope and then evaluating the expressions, then detaching from the scope. The last expression is returned.

##### Example

```

> (using User

(definitions (scope)))

.:  {}

> (extend User

(function foo {} hello)

(function bar {} world))

.:  User

> (using User

(definitions (scope)))

.:  {{foo "(function foo {} hello)"}

{bar "(function bar {} world)"}}

```

##### Related

attach, detach, each, get, knowledge, put, using, which, with

## values

Creates a list of values for an assortment.

##### Syntax

(values _assortment_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | A environment, enumeration, or lexicon. |

##### Results

| Data Type | Description |
| --- | --- |
| list | A list of values |

##### Remarks

For collections this function returns the same result as the keys function.

##### Example

```

> (global ?M nil)

.:  true

> (set ?M (lexicon :X 1 !m noop :T nil A 2))

.:  true

> (values ?M)

.:  {1 noop nil 2}

> (filter (keys ?M) (given {?v} (term-p ?v)))

.:  {:X !m :T}

> (filter (values ?M) (given {?v} (not (term-p ?v))))

.:  {1 noop nil 2}

> (values (collection the quick brown fox))

.:  {the quick brown fox}

```

##### Related

@ _element_, add, bindings, cut, free, get, in, key, keys, size

## var

Adds variables to the current environment returning the last assigned value.

##### Syntax

(var _manner_ _assignment_ _..._ )

_assignment ::= symbol value_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed<br><br>either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | Returns the last assigned value. |

##### Remarks

Sequentially creates variables in the current environment. Each symbol shall replace any extant symbol with the same name in the environment. Returns the value of the last assignment.

##### Example

```

> (var ?person DrWho)

.:  DrWho

> ?person

.:  DrWho

```

##### Related

<-- _before tie_, --> _after tie_, assume, constant, dynamic, given, global, let, local, set, symbol, variables

## vector

Creates a vector of atoms.

##### Syntax

(vector _atom_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| atom | atom | 0+  | An atomic value such as a number, time, or literal. |

##### Results

| Data Type | Description |
| --- | --- |
| vector | Returns a vector containing the atoms. |

##### Remarks

A vector is an immutable sequence of atoms. Vectors can also be created by simply enclosing the elements with vertical bars called pipes ( | ). Whenever vectors are manipulated, a new vector is created. Vectors cannot be embedded, and cannot contain sequences.

##### Example

```

> (vector a b c d)

.:  |a b c d|

> (vector 500)

.:  |500|

> (vector foo)

.:  |foo|

> |a b c d|

.:  |a b c d|

```

##### Related

& _merge_, && _abridge_, inside, list

## version

Provides version information.

##### Syntax

(version)

##### Module

Base

##### Parameters

None

##### Results

| Data Type | Description |
| --- | --- |
| nil | Returns nil |

##### Remarks

Prints system and version information.

##### Example

```

> (version)

\[Premise :Version 0.2.0 20180201.001 :OS Windows 10 :Edition Community\]

.:  nil

```

##### Related

bye, help, copyright

## void-p

True if a container has zero elements.

##### Syntax

(void-p _sequence_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the sequence has zero items. |

##### Remarks

True if the container has zero items.

##### Example

```

> (void-p "not empty")

.:  false

> (void-p (expression))

.:  true

> (void-p "")

.:  true

> (void-p {})

.:  true

> (void-p (call))

.:  true

> (void-p \[\])

.:  true

```

##### Related

more-p

## wait

Waits for tasks to end.

##### Syntax

(wait _tasks timeout_ )

##### Module

Tasks

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| tasks | list | 1   | A list of task resources |
| timeout | instant | 0-1 | The amount of time to wait for the task. The default is eternity which implies to wait indefinitely |

##### Results

| Data Type | Description |
| --- | --- |
| list | The task resources. |

##### Remarks

The wait function waits for either the timeout duration or for the task to complete. This function allows tasks to complete in a blocking manner.

##### Example

```

> (var ?tasks (wait (concurrent (repeat 1000000 foo)

(repeat 2000000 bar)

(repeat 3000000 baz))

\\@s10))

.:  {task-1 task-2 task-3}

> (map ?tasks (given {?t}(await ?t \\@s0)))

.:  {foo bar baz}

> (free (wait (complete

(repeat 1000 foo)

(repeat 2000 bar)

(repeat 3000 baz))))

.:  freed

```

##### Related

wait, abort, concurrent, await, complete, do, done-p, free, task, tarry

## which

Creates a list of thoughts for a pattern..

##### Syntax

(which _category_ _criterion_ _…_ _option_ _…_)

_category_ ::= _relation_

_category_ ::= _list_

_criterion := slot binding_

_criterion_ ::= _slot condition_

_criterion_ ::= _slot condition_

_binding_ ::= as _symbol_

_iteration_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition ::= slot /__\=_ _value_

_condition_ ::= is _unary-predicate_

_condition_ ::= not _unary-predicate_

_condition_ ::= _binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

_option_ ::= scan _number_

_option_ ::= limit _number_

_option_ ::= group _slot_ _…_ by _slot_ _…_ into _symbol_

_option_ ::= merge _value_ _…_

_option_ ::= sort _ordering_ _…_

_ordering_ ::= _term comparator_

_action_ ::= give _expression_

_action_ ::= list _value_ _…_

_action_ ::= tally

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| relation | variant | 1   | A relation name or list of thoughts. |
| criterion | expression | 0+  | A slot referent pair or method function pair. |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |

##### Results

| Data Type | Description |
| --- | --- |
| list | Returns a list of premises matching the pattern. |

##### Remarks

Looks for existing thoughts matching the criteria. If no variables are specified, the relation name is used, e.g. the Employee shall use an ?Employee symbol for each instance found. If the action is give, then the expression is immediately returned from the which call on the first match. If the action is either list, then a list containing each expression is returned or an empty list is returned if nothing matched. If the action is tally, then the number of matched premises is returned, or zero if no matches.

##### Example

```

(relation Car :Make :Model :Year)

(which Car :Make Toyota)

(which (which Car :Make Toyota) each ?thought

\[Dealer :Has (:Make ?tuple)\]

deem true)

> (relation Pairs :A :B)(new Pairs :A 1 :B 2)(new Pairs :A 3 :B 4)

.:  Pairs Pairs_1 Pairs_2

> (which Pairs :B 2)

.:  Iterator-1

> (relation Fact :All :Are)

.:  Fact

> (new Fact :All people :Are mortal) (new Fact :All philosophers :Are people)

.:  Fact_1 Fact_2

> (function ExcludedMiddle {}

(with \[Fact :All as ?s :Are as ?m\]

\[Fact :All ?m :Are as ?p\]

(no \[Fact :All ?s :Are ?p\])

list (premise (knew A :All ?s :Are ?p))))

.:  ExcludedMiddle

> (ExcludedMiddle)

.:  {\[Fact ^ Fact_3 :All philosophers :Are mortal\]}

> (which Fact ^ as ?a :Are mortal)

.:  Iterator-2

> (with Fact :Are mortal)

.:  {\[Fact ^ Fact_1 :All people :Are mortal\]

\[Fact ^ Fact_3 :All philosophers :Are mortal\]}

> (relation Fruit :Name :Size :Shape :Color)

.:  Fruit

> (step ?i from 1 to (random 1 to 1000)

(new Fruit :Size (pick {small medium large})

:Shape (pick {ellipsoid spheroid bananoid})

:Color (pick {red orange yellow green})))

.:  Fruit_387

> (with \[Fruit ^ as ?f :Name as ?name :Size as ?size :Shape spheroid :Color orange\]

(null-p ?name)

(in {small medium} ?size)

deem Orange else Other)

.:  Orange

> (with

\[Fruit as ?f\]

(let ?f :Size ?size :Shape ?shape :Color ?color)

(in {small medium} ?size)

(= ?shape bananoid)

(= ?color yellow)

deem true else false)

.:  true

> (relation Customer :CustomerId :FirstName :LastName)

.:  Employee

> (relation Order :OrderId :CustomerId :Quantity :Product)

.:  Order

> (step ?i from 1 to (random 1 to 10)

(let ?c (new Customer))

(step ?j from 1 to (random 0 to 10)

(new Order :CustomerId ?c)))

.:  Order_347

> (with \[Customer as ?c\]

\[(with Order as ?o (= (:CustomerId ?o) (:CustomerId ?c))) each ?orders\]

tally)

.:  2

> (with

\[Customer as ?c :CustomerId ?x\]

\[(with Order as :CustomerId ?y (= ?x ?y)) as ?orders\]

scan 30

limit 5

list

\[R :Customer ?c :Orders (# ?orders)\])

.:  {\[R :Customer Customer_1 :Orders 3\]

\[R :Customer Customer_2 :Orders 7\]

\[R :Customer Customer_4 :Orders 4\]

\[R :Customer Customer_3 :Orders 9\]}

> (relation Student

:First

:Last

:StudentNo

:Year

:Tests {})

> (do

(new Student :First John :Last Jones :No 20 :Year 2 :Tests {100 56 87 86})

(new Student :First Lexie :Last Bates :No 16 :Year 3 :Tests {67 68 98 87})

(new Student :First Yong :Last Lee :No 17 :Year 1 :Tests {78 79 90 95})

(new Student :First Paul :Last Gates :No 14 :Year 4 :Tests {86 89 88 89})

(new Student :First Jenny :Last Luria :No 15 :Year 3 :Tests {99 98 97 99})

(new Student :First Phillipa :Last Sanchez :No 18 :Year 2 :Tests {85 87 89 97})

(new Student :First Patrice :Last Jones :No 13 :Year 1 :Tests {99 95 94 72})

(new Student :First Jesus :Last Castaneda :No 12 :Year 4 :Tests {98 89 95 94})

(new Student :First Charlie :Last Rose :No 11 :Year 2 :Tests {97 98 98 97})

(new Student :First Boris :Last Pushkin :No 19 :Year 3 :Tests {100 85 100 100})

(new Student :First Alex :Last Sartre :No 22 :Year 1 :Tests {85 97 86 95})

(new Student :First Elizabeth :Last Wilson :No 21 :Year 4 :Tests {100 100 85 95}))

.:  Student_12

> (which Student ^ ?student

(let ?exam 3 ?score 90)

(> (@ (:Tests ?student) ?exam) ?score)

list {:Name (:Last ?student) :Score (@ (:Tests ?student) ?exam)})

.:  {{:Name Bates :Score 98}{:Name Luria :Score 97}{:Name Parker :Score 94}

{:Name Castaneda :Score 95}{:Name Rose :Score 98}{:Name Pushkin :Score 100}}

> (which Student as ?s

group ?s

by :Year into ?g

list ?g

sort 1 <)

.:  {{1 \[Student :First Yong :Last Lee :No 17 :Year 1 :Tests {78 79 90 95}\]

\[Student :First Patrice :Last Jones :No 13 :Year 1 :Tests {99 95 94 72}\]

\[Student :First Alex :Last Sartre :No 22 :Year 1 :Tests {85 97 86 95}\]}

{2 \[Student :First John :Last Jones :No 20 :Year 2 :Tests {100 56 87 86}\]

\[Student :First Phillipa :Last Sanchez :No 18 :Year 2 :Tests {85 87 89 97}\]

\[Student :First Charlie :Last Rose :No 11 :Year 2 :Tests {97 98 98 97}\]}

{3 \[Student :First Lexie :Last Bates :No 16 :Year 3 :Tests {67 68 98 87}\]

\[Student :First Jenny :Last Luria :No 15\] :Year 3 :Tests {99 98 97 99}\]

\[Student :First Boris :Last Pushkin :No 19 :Year 3 :Tests {100 85 100 100}\]}

{4 \[Student :First Paul :Last Gates :No 14 :Year 4 :Tests {86 89 88 89})

\[Student :First Jesus :Last Castaneda :No 12 :Year 4 :Tests {98 89 95 94}\]

\[Student :First Elizabeth :Last Wilson :No 021 :Year 4 :Tests {100 100 85 95})}\]}}}

> (which Student as ?s :Id ?id

group ?id

by (given {?s} (@ ($ (:Last ?s)) 1)) into ?g

list ?g)

.:  {{"B" 16}{"C" 12}{"G" 14}{"P" 19}{"R" 11}{"L" 17 15}{"W" 21}{"S" 18 22}{"J" 20 13}}

> (which Student as ?s :Tests ?t

(let ?percentile (/ (avg ?t) 10))

group ($ (:First ?s) (:Last ?s))

by ?percentile into ?g

list ?g

sort 1 < )

.:  {{8 "John Jones" "Lexie Bates" "Yong Lee" "Paul Gates" "Phillipa Sanchez"}

{9 "Jenny Luria" "Patrice Jones" "Jesus Castaneda" "Charlie Rose" "Boris Pushkin" "Alex Sartre" "Elizabeth Wilson"}}

> (with Student as ?s

group \[R :FirstLetter (@ ($ (:Last ?s)) 1)

:Score (:Score ?s)\]

by (given {?s} (> (@ (:Tests ?s) 1) 85)\])

into ?g

list ?g

sort (given {?x} (:FirstLetter ?x)) <)

.:  {{"C" \[R :FirstLetter "C" :Score 98\]}{"J" \[R :FirstLetter "J" :Score 100\]

\[R :FirstLetter "J" :Score 99\]}{"L" \[R :FirstLetter "L" :Score 99\]}

{"G" \[R :FirstLetter "G" :Score 86\]}{"P" \[R :FirstLetter "P" :Score 100\]}

{"R" \[R :FirstLetter "R" :Score 97\]}{"W" \[R :FirstLetter "W" :Score 100\]}}

```

##### Related

each, knew, known, new, relation, such, suppose, unless, using, with

## while

Loops expressions while a condition is true.

##### Syntax

(while _condition_ _expression_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| expression | expression | 0+  | A call to be evaluated. |

##### Results

| Data Type | Description |
| --- | --- |
| value | The last value of the last iteration |

##### Remarks

None

##### Example

```

> (modular ?i 0)

.:  true

> (while (< ?i 1000)

(--> ++ ?i)) ; assign ?i to the increment of ?i.

.:  1000

```

##### Related

for, iterate, loop, repeat, step, until

## whitespace-p

True if the first position of a string is whitespace.

##### Syntax

(whitespace-p _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the value is a string and the first position is whitespace. |

##### Remarks

Whitespace is a space, newline, or tab.

##### Example

```

> (whitespace-p {a b c})

.:  false

> (whitespace-p "a b c")  


.:  false

> (whitespace-p " a b c")

.:  true

> (whitespace-p 450)

.:  false

> (whitespace-p " foo")

.:  true

> (whitespace-p "hello world")

.:  false

```

##### Related

capitalized-p, letter-p, lowercase-p, uppercase-p

## with

Matches patterns against the knowledge base.

##### Syntax

(with _premises_ _option_ _…_ _action_ )

_premises_ ::= _premise_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _premises_

_premises_::= _premise_ _restriction … premises_

_restriction_ ::= (_predicate value_ _…_)

_premise_ ::= \[_category descriptor_ _…_ \]

_category_ ::= _type_

_category_ ::= _list_

_descriptor_ ::= _slot binding_

_descriptor_ ::= _slot condition_

_binding_ ::= as _symbol_

_binding_ ::= each _symbol_

_condition ::= slot_ _\=_ _value_

_condition ::= slot_ _/=_ _value_

_condition_ ::= _slot_ is _unary-predicate_

_condition_ ::= _slot_ not _unary-predicate_

_condition_ ::= _slot binary-predicate value_

_condition_ ::= _slot n-ary-predicate value-list_

_condition_ ::= (_predicate value_ _…_)

_option_ ::= scan _number_

_option_ ::= limit _number_

_option_ ::= group _slot_ _…_ by _slot_ _…_ into _symbol_

_option_ ::= merge _value_ _…_

_option_ ::= sort _ordering_ _…_

_action_ ::= deem _value1_ else _value2_

_action_ ::= do _expression_ _…_

_action_ ::= give _expression_

_action_ ::= list _value_ _…_

_action_ ::= tally

_action_ ::= yield _expression_

_ordering_ ::= _term comparator_

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| clauses / premises | expression | 1+  | Either one or more clauses, or, one or more premises |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |
| action | literal | 0-1 | Either deem, do, give, list, tally, yield. |
| expression | expression | 0+  | An expression |

##### Results

| Data Type | Description |
| --- | --- |
| expression | if the action is deem, then either the success or failure value is returned; if the action is do then the last expression value on the last iteration or nil; If the action is list, then a list of premises or an empty list; if the action is tally, then the number of matches or zero, if the action is give, then the expression is returned. |

##### Remarks

Note that a predicate is a truth function, scan tells the number of matches to attempt (default is infinity), and limit tells how many results to return (default is infinity). If the action is deem, then the subsequent value is returned if the final descriptor is matched, otherwise the else value is returned. If the action is do, then for each match the expressions are run, and for the last match, the last value of the last expression is returned, or nil is returned if all descriptors were false or had no matches. If the action is give, then the expression is immediately returned from the with call on the first match, akin to return from with. If the action is yield, then the expression is immediately returned from the with call, but may be resumed with a next function call. When all matches are completed, the done function is implicitly called to terminate the generator. If the action is group, followed by a list of slots and values from which the group is picked, then the literal by and a set of slots and values that determines the grouping inclusion , and finally the literal into followed by a symbol to which the group shall be bound on each iteration. If the action is either list (or merge), then a (merged) list is returned or an empty list if nothing matched. If the action is sort then the list of slots and comparators should follow. (Note that list is required if the sort action is selected.) If the action is tally, then the number of matched premises is returned, or zero if no matches.

##### Example

```

> (relation Fact :All :Are)

.:  Fact

> (new Fact :All people :Are mortal) (new Fact :All philosophers :Are people)

.:  Fact_1 Fact_2

> (function ExcludedMiddle {}

(with \[Fact :All as ?s :Are as ?m\]

\[Fact :All = ?m :Are as ?p\]

(no \[Fact :All = ?s :Are = ?p\])

list (premise (knew A :All ?s :Are ?p))))

.:  ExcludedMiddle

> (ExcludedMiddle)

.:  {\[Fact ^ Fact_3 :All philosophers :Are mortal\]}

> (which Fact ^ as ?a :Are = mortal list ?a)

.:  {Fact_1 Fact_3}

> (which Fact :Are mortal)

.:  {\[Fact ^ Fact_1 :All people :Are mortal\]

\[Fact ^ Fact_3 :All philosophers :Are mortal\]}

> (relation Fruit :Name :Size :Shape :Color)

.:  Fruit

> (step ?i from 1 to (random 1 to 1000)

(new Fruit :Size (pick {small medium large})

:Shape (pick {ellipsoid spheroid bananoid})

:Color (pick {red orange yellow green})))

.:  Fruit_387

> (with \[Fruit ^ as ?f :Name as ?name :Size as ?size :Shape = spheroid

:Color = orange\]

(null-p ?name)

(in {small medium} ?size)

deem Orange else Other)

.:  Orange

> (with

\[Fruit as ?f\]

(let ?f :Size ?size :Shape ?shape :Color ?color)

(in {small medium} ?size)

(= ?shape bananoid)

(= ?color yellow)

deem true else false)

.:  true

> (relation Customer :CustomerId :FirstName :LastName)

.:  Employee

> (relation Order :OrderId :CustomerId :Quantity :Product)

.:  Order

> (step ?i from 1 to (random 1 to 10)

(let ?c (new Customer))

(step ?j from 1 to (random 0 to 10)

(new Order :CustomerId ?c)))

.:  Order_347

> (with \[Customer as ?c\]

\[(which Order as ?o (= (:CustomerId ?o) (:CustomerId ?c))) each ?orders\]

tally)

.:  2

> (with

\[Customer as ?c :CustomerId ?x\]

\[(with Order :CustomerId = ?x) as ?orders\]

scan 30

limit 5

list

\[R :Customer ?c :Orders (# ?orders)\])

.:  {\[R :Customer Customer_1 :Orders 3\]

\[R :Customer Customer_2 :Orders 7\]

\[R :Customer Customer_4 :Orders 4\]

\[R :Customer Customer_3 :Orders 9\]}

> (relation Student

:First

:Last

:StudentNo

:Year

:Tests {})

> (do

(new Student :First John :Last Jones :No 20 :Year 2 :Tests {100 56 87 86})

(new Student :First Lexie :Last Bates :No 16 :Year 3 :Tests {67 68 98 87})

(new Student :First Yong :Last Lee :No 17 :Year 1 :Tests {78 79 90 95})

(new Student :First Paul :Last Gates :No 14 :Year 4 :Tests {86 89 88 89})

(new Student :First Jenny :Last Luria :No 15 :Year 3 :Tests {99 98 97 99})

(new Student :First Phillipa :Last Sanchez :No 18 :Year 2 :Tests {85 87 89 97})

(new Student :First Patrice :Last Jones :No 13 :Year 1 :Tests {99 95 94 72})

(new Student :First Jesus :Last Castaneda :No 12 :Year 4 :Tests {98 89 95 94})

(new Student :First Charlie :Last Rose :No 11 :Year 2 :Tests {97 98 98 97})

(new Student :First Boris :Last Pushkin :No 19 :Year 3 :Tests {100 85 100 100})

(new Student :First Alex :Last Sartre :No 22 :Year 1 :Tests {85 97 86 95})

(new Student :First Elizabeth :Last Wilson :No 21 :Year 4 :Tests {100 100 85 95}))

.:  Student_12

> (with Student ^ ?student

(let ?exam 3 ?score 90)

(> (@ (:Tests ?student) ?exam) ?score)

list {:Name (:Last ?student) :Score (@ (:Tests ?student) ?exam)})

.:  {{:Name Bates :Score 98}{:Name Luria :Score 97}{:Name Parker :Score 94}

{:Name Castaneda :Score 95}{:Name Rose :Score 98}{:Name Pushkin :Score 100}}

> (with \[Student as ?s\]

group ?s

by :Year into ?g

list ?g

sort 1 <)

.:  {{1 \[Student :First Yong :Last Lee :No 17 :Year 1 :Tests {78 79 90 95}\]

\[Student :First Patrice :Last Jones :No 13 :Year 1 :Tests {99 95 94 72}\]

\[Student :First Alex :Last Sartre :No 22 :Year 1 :Tests {85 97 86 95}\]}

{2 \[Student :First John :Last Jones :No 20 :Year 2 :Tests {100 56 87 86}\]

\[Student :First Phillipa :Last Sanchez :No 18 :Year 2 :Tests {85 87 89 97}\]

\[Student :First Charlie :Last Rose :No 11 :Year 2 :Tests {97 98 98 97}\]}

{3 \[Student :First Lexie :Last Bates :No 16 :Year 3 :Tests {67 68 98 87}\]

\[Student :First Jenny :Last Luria :No 15\] :Year 3 :Tests {99 98 97 99}\]

\[Student :First Boris :Last Pushkin :No 19 :Year 3 :Tests {100 85 100 100}\]}

{4 \[Student :First Paul :Last Gates :No 14 :Year 4 :Tests {86 89 88 89})

\[Student :First Jesus :Last Castaneda :No 12 :Year 4 :Tests {98 89 95 94}\]

\[Student :First Elizabeth :Last Wilson :No 021 :Year 4 :Tests {100 100 85 95})}\]}}}

> (which Student as ?s :Id as ?id

group ?id

by (given {?s} (@ ($ (:Last ?s)) 1)) into ?g

list ?g)

.:  {{"B" 16}{"C" 12}{"G" 14}{"P" 19}{"R" 11}{"L" 17 15}{"W" 21}{"S" 18 22}{"J" 20 13}}

> (with \[Student as ?s :Tests as ?t\]

(let ?percentile (/ (avg ?t) 10))

group ($ (:First ?s) (:Last ?s))

by ?percentile into ?g

list ?g

sort 1 < )

.:  {{8 "John Jones" "Lexie Bates" "Yong Lee" "Paul Gates" "Phillipa Sanchez"}

{9 "Jenny Luria" "Patrice Jones" "Jesus Castaneda" "Charlie Rose" "Boris Pushkin" "Alex Sartre" "Elizabeth Wilson"}}

> (with \[Student as ?s\]

group \[R :FirstLetter (@ ($ (:Last ?s)) 1)

:Score (:Score ?s)\]

by (given {?s} (> (@ (:Tests ?s) 1) 85)\])

into ?g

list ?g

sort (given {?x} (:FirstLetter ?x)) <)

.:  {{"C" \[R :FirstLetter "C" :Score 98\]}{"J" \[R :FirstLetter "J" :Score 100\]

\[R :FirstLetter "J" :Score 99\]}{"L" \[R :FirstLetter "L" :Score 99\]}

{"G" \[R :FirstLetter "G" :Score 86\]}{"P" \[R :FirstLetter "P" :Score 100\]}

{"R" \[R :FirstLetter "R" :Score 97\]}{"W" \[R :FirstLetter "W" :Score 100\]}}

```

##### Related

each, which

## within

True if a position is inside a sequence.

##### Syntax

(within _sequence position_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| position | variant | 1+  | A number or coordinate (i.e. a list of numbers). |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the position is in the sequence, false otherwise. |

##### Remarks

None.

##### Example

```

> (within "not empty" 5)

.:  true

> (within {not empty} 1)

.:  true

> (within "" 1)

.:  false

> (within {} 5)

.:  false

> (within {{a b}{c d}{e f}} {3 2})

.:  true

> (within {{a b}{c d}{e f}} {7 4})

.:  false

```

##### Related

@ _element_, beyond, length, empty, more

## wrap

Prohibits modifications to a module.

##### Syntax

(wrap _module_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| module | module | 1   | A module |

##### Results

| Data Type | Description |
| --- | --- |
| literal | The literal wrapped |

##### Remarks

None

##### Example

```

> (module Math

(function sum ?args (apply + ?args)))

.:  Math

> (wrap Math)

.:  wrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.:  \[Failure :Name Permission :Text "Can't modify a wrapped module"\]

> (unwrap Math)

.:  unwrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.:  Math

```

##### Related

unwrap

## write

Writes values to a writeable resource.

##### Syntax

(write _file value_ )

##### Module

IO

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| file | resource | 1   | A file or pipe. |
| value | variant | 1   | A value to write |
| bits | integer | 0-1 | The size of the byte or character in bits. Either 7, 8, 16,o,r 32. (Default is 8.) |

##### Results

| Data Type | Description |
| --- | --- |
| resource | Returns the resource |

##### Remarks

None.

##### Example

```

> (let ?file (file name "test.txt"))

.:  true

> (read ?file)

.:  "Hello"

> (seek ?file 1)

.:  File-1

> (write ?file ($ Goodbye my friends.))

.:  File-1

> ­(close ?file)

.:  closed

```

##### Related

bytes, close, file, read, reposition, write

## xnor

Logical equivalance.

##### Syntax

(xnor _truth truth_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 2   | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the argument values are equal |

##### Remarks

Implements logical equivalence as the result is true when both arguments are the same.

##### Example

```

> (xnor true false)

.:  false

> (xnor false true)

.:  false

> (xnor false false)

.:  true

> (xnor true true)

.:  true

```

##### Related

and, nand, void, nor, not, or, is, xor

## xor

Logical exclusive disjunction.

##### Syntax

(xor _truth truth_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 2   | A truth value |

##### Results

| Data Type | Description |
| --- | --- |
| truth | True if the argument values are not equal |

##### Remarks

None.

##### Example

```

> (xor true false)

.:  true

> (xor false true)

.:  true

> (xor false false)

.:  false

> (xor true true)

.:  false

```

##### Related

and, nand, void, nor, not, or, is, xnor

## yield

Returns a result from a series generator.

##### Syntax

(yield _value_)

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | Any value to be returned. Default is nil. |

##### Results

| Data Type | Description |
| --- | --- |
| variant | The returned value. |

##### Remarks

Yield exits from an encompassing generator. If the value is not specified, nil is returned. When yield is executed the encompassing generator immediately returns the value. To termine use done.

##### Example

```

> (generator myGenerator {?interrupt}

(yield 1)

(yield 2)

(if ?interrupt (done))

(yield 3)

(yield 4)

(done))

.:  myGenerator

> (collect ?x in (myGenerator true) ?x)

.:  {1 2}

> (collect ?x in (myGenerator false) ?x)

.:  {1 2 3 4}

```

##### Related

done, generator-p, series

## zap

Updates associations and sequences with nil values.

##### Syntax

(zap _container place_ _…_ )

##### Module

Base

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment |
| place | variant | 0+  | A slot, key, or position. |

##### Results

| Data Type | Description |
| --- | --- |
| container | Returns the modified container. |

##### Remarks

If no places are provided, then all keys, positions, or slots are set to nil.

##### Example

```

> (relation A :X 1 :Y 2 :Z 3)

.:  a

> (get (new A))

.:  \[A ^ A_1 :X 1 :Y 2 :Z 3\]

> (zap A_1 :Y)

.:  A_1

> (get A_1)

.:  \[A ^ A_1 :X 1 :Y nil :Z 3\]

> (zap A_1)

.:  A_1

> (get A_1)

.:  \[A ^ A_1 :X nil :Y nil :Z nil\]

```

##### Related

let, new, nix

## zero-p

True if a number is zero.

##### Syntax

(zero-p _number_)

##### Module

Math

##### Parameters

| Name | Data Type | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Data Type | Description |
| --- | --- |
| truth | Returns true if the number is zero. |

##### Remarks

None.

##### Example

```

> (zero-p 100)

.:  false

> (zero-p 0)

.:  true

> (zero-p -0)

.:  true

> (zero-p -30)

: false

```

##### Related

even-p, negative-p, odd-p, positive-p

# Bibliography

1\. Chambers, C. 1992  
The Design and Implementation of the SELF Compiler, an Optimizing Compiler for Object-Oriented Programming Languages

2\. Forgy, Charles 1981  
OPS5 User’s Manual, Technical Report CMU-CS-81-135 (Carnegie Mellon University)

3\. Krishnamurthi, Sriram 2017  
Programming Languages: Application and Interpretation, Second Edition

4\. Linker, Sheldon O. 2005  
A knowledge base and question answering system based on loglan and english

5\. Linker, Sheldon O., Miller, M. S. P. 2014  
Association for the Advancement of Artificial Intelligence  
Spring Symposium Series 2014 (AAAI SSS 14)  
Implementing Selves with Safe Motivational Systems and Self-Improvement Invited Talk “Premise: A Language for Cognitive Systems”

6\. Miller, Michael S. P. 2013  
The Construction of Reality in a Cognitive System

7\. Miller, Michael S. P. 2018  
Building Minds with Patterns, ISBN 978-0-692-54140-1

8\. Queinnec, Christian 1994  
Lisp in Small Pieces, Cambridge University Press, ISBN 0-521-54566-8

9\. Steele Jr , Guy L. 1981  
Common LISP: The Language, 2nd Ed., Digital Press, ISBN 978-1-55558-041-4.

# Index

\-- decrement 125

' _quote_ 141

\- _subtraction_ 126

# _size_ 128

$ _concatenate_ 129

$$ _elide_ 130

% _shell_ 131

_&_ _merge_ 132

&& _abridge_ 133

\* _multiplication_ 134

** _exponentiation_ 135

/ _division_ 136

// _nth root_ 137

/~ _dissimilarity_ 138

/= _unequal_ 139

@ _element_ 127

\\n _newline_ 154

\\s _space_ 155

^ _thought id_ 156

\` _expand_ 142

~ similarity 140

+ _addition_ 143

++ _increment_ 144

< _less_ 146

<-- before tie 39, 145

<= _less or equal_ 147

<== _before put_ 148

\= _equal_ 149

\==> _after put_ 150

\--> after tie 39, 152

> _greater_ 151

>= _greater or equal_ 153

abolish 157

abort 158

about 159

abs 160

absent 161

acosecant 162

acosine 163

acotangent 164

actual 165

add 166

address 167

agent 168

align 169

alike 170

all 171

alphabetic-p 173

alphanumeric-p 174

and 175

anonym 62

Anonymous Functions 62

any 176

append 178

apply 179

arity 180

array 181

asecant 182

asine 183

ask 184

atangent 186

atom 26

attach 187

Auto-named Functions 62

average 188

avg 189

await 190

before-p 191

beginning 192

best 193

beyond 195

big 28, 196

binary 27

bind 40, 197

bindings 198

bion 199

bitwise 200

bound 202

bound-p 203

bracket 204

break 70, 205

busy-p 206

but 207

bye 208

call 57, 209

can 210

cancel 211

cancelled-p 212

canonify 213

capitalize 214

case 64, 215

categorize 216

cede 217

ceiling 218

cell 219

char 220

choose 221

clear 222

clip 223

clone 224

close 225

closure 226

coalesce 228

collect 230

collection 45, 232

combine 233

common 234

comparable-p 235

compare 236

complete 75, 237

complex 29, 238

Complex numbers 29

compose 239

conceive 240

concurrent 75, 241

configuration 46, 242

confirm 69, 243

confute 69, 244

constant 34, 245

container 52

contains 246

continuation 48

continue 70, 247

convertible-p 248

copy 249

copyright 250

correlate 251

cosecant 252

cosine 253

cotangent 254

count 67, 255

critical 256

cut 257

data 48, 50, 258

date 31, 260

decimal 28

Declarative Programming 24

declared-p 261

decode 262

default 263

definitions 264

defunct 265

degrees 266

delete 267

dependencies 268

depends 270

deq 269

detach 271

did 273

difference 272

digit 274

digit-p 275

digits 276

dimensions 277

discard 278

disjoint-p 279

distinct 280

distribute 281

divide 282

divisible-p 283

do 65, 284

done 286

drop 287

duplicate 288

during-p 289

dynamic 290

Dynamic Scope 36

e 291

each 292

encode 296

endoym 62

enq 297

ensure 72, 298

entries 299

enum 300

enumeration 46, 301

enumerations 302

environment 46, 303

ephemerons 46

epoch 304

eradicate 305

erase 306

escape 73, 307

eternity 33

eval 308

even-p 309

every 310

exactly 311

exchange 312

excludes 313

exists-p 26, 314

exit 70

exit 315

exonym 57

exponential 316

expression 52, 317

extend 318

facility 319

few 321

file 49, 322

files 323

fill 324

filter 325

find 326

finishes-p 328

finishing 329

fix 38, 330

float 29, 331

floor 332

fold 333

folder 334

folders 335

for 66, 336

forever 337

forgo 338

format 339

fractional 340

free 341

full 342

function 343

Functional Programming 23

functions 346

gather 347

generator 348

get 350

given 351

global 353

Global Scope 35

go 74, 354

grok 355

group 356

halt 357

has 358

hash 359

help 360

here 361

hexadecimal 28

hexatridecimal 28

hyperlink 362

id 363

identical-p 364

identifier 34

identity 43, 365

idle 366

if 64, 367

imaginary 29, 368

Imaginary numbers 29

Imperative Programming 22

in 514

includes 369

indefinite 33

index 370

indices 371

_infinity_ 30

infix 372

insert 374

inside 373

insort 375

instance 54

instantiate 376

integer 27, 377

interleave 378

intersection 379

intersects-p 380

interval 31, 381

into 382

intrinsics 51

invoke 383

is 384

jiffy 31

junction 385

key 387

keys 388

keywords 389

knew 390

knowledge 391

known 393

lacks 394

last 395

left 396

let 38, 397

lexemes 398

Lexical Scope 36

lexicon 47, 399

lexicons 400

license 401

like 402

list 52, 403

literal 41, 404

local 405

location 406

log 407

long 28, 408

long number 28

loop 66, 409

lowercase 410

lowercase-p 411

macro 412

macros 413

make 414

map 415

max 416

maximum 417

may 418

median 419

meets-p 420

meron 421

meronomy 423

meron-p 422

method 424

methods 44

mid 427

min 428

minimum 429

missing 430

mod 431

modular 432

module 433

Module Scope 35

modules 51, 434

moment 32, 435

more-p 436

morph 437

most 438

move 439

my 440

nall 441

nand 443

negative-p 444

neternity 33

nevery 445

new 446

next 447

ngrams 448

nil-p 449

ninfinity 30

nix 450

no 451

none 453

nor 454

not 455

nothing 26, 456

null-p 26, 457

number 27

numerics 30

octal 27

odd-p 458

old 459

omit 460

on 65, 461

only 462

open 463

or 464

out 465

overlaps-p 466

pad 467

parameters 58

partition 468

path 469

pattern 55, 470

pause 471

perform 472

pi 473

pick 474

pipe 475

pop 476

posit 477

position 478

positions 479

positive-p 480

premise 481

probability 482

procedure 483

proceed 485

product 486

prototype 43

punctuation-p 487

push 488

put 489

qualified 490

qualifiers 491

quantify 492

quantity 493

radians 494

radix 27, 495

random 496

range 497

rational 29, 498

read 499

Read Evaluate Print Loop 22

ready-p 500

real 29, 501

Real numbers 29

reasoning 502

reclaim 503

reduce 504

reference 505

references 35

relation 506

relations 508

relatum 42

release 509

remove 510

repeat 67, 511

replace 512

require 513

reserved 51

reset 515

resize 516

resource 45

rest 517

Restricted Scope 37

retract 518

return 72, 519

reverse 522

right 523

rip 524

round 525

rule 526

rules 530

same 531

scale 532

scatter 76, 533

scope 534

seal 535

secant 536

seconds 31, 32, 537

securelink 538

seek 539

self 540

separator 541

sequence 52

series 542

service 543

set 40, 544

sever 545

shuffle 546

sigma 547

signal 71, 548

significand 549

signum 550

sine 551

so 552

socket 553

some 554

sort 555

split 557

start 558

starts-p 559

statistics 560

step 67, 561

stream 562

string 53, 563

structure 564

structures 41, 566

sub 567

subset-p 568

substitute 569

subsumes-p 570

sum 571

summation 572

supply 573

suppose 574

survey 579

swap 582

symbol 580

Symbol Scoping 35

symbols 34, 581

take 583

takeable 584

tally 585

tangent 586

tarry 587

task 49, 588

Task Scope 37

tasks 590

taxon 591

taxonomy 593

taxon-p 592

tell 594

temporal 33

there 596

thing 26

this 597

thought 47, 598

thunk 599

thunks 601

tick 32, 602

tie 39, 603

time 31, 604

top 606

transfer 607

traverse 608

trim 609

truncate 610

try 65, 611

tuple 613

Tuples 54

unbound 615

unbound-p 616

undefined 30

unicode 617

union 618

unique 619

unless 620

unlike 621

unqualified 622

unseal 623

unsigned 30, 624

until 68, 625

unwrap 626

uppercase 627

uppercase-p 628

url 629

use 630

User Defined Functions 57

User Defined Macros 63

using 631

uuid 614

values 632

var 38, 633

variant 26

vector 634

vectors 53

version 635

void-p 636

wait 637

which 638

while 68, 643

whitespace-p 644

with 645

within 651

wrap 652

write 653

xnor 654

xor 655

yield 656

zap 657

zero-p 658

