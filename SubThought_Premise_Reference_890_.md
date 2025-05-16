  
The SubSubThought Premise Language Reference

version 3.0

by

Michael S P Miller



Copyright © 2013 – 2023. thought Corporation.

All Rights Reserved. No part of this book may be reproduced in any form by any electronic or mechanical means (including photocopying, recording, or information storage and retrieval systems) without permission in writing from the author–except in the case of a reviewer who may quote brief passages embodied in critical articles or in a review.

Trademarked names may appear throughout this book. Rather than use a trademark symbol with every occurrence of a trademarked name, names are used in an editorial fashion, with no intention of infringement of the respective owner’s trademark or copyright. The same applies to quotations or synopses of copyrighted material.

The information in this book is distributed on an “as is” basis, without warranty. Although every precaution has been taken in the preparation of this work, neither the author nor the publisher shall have any liability to any person or entity with respect to any loss or damage caused directly or indirectly by the information contained in this book. The source code examples and specifications in this book are for illustrative purposes only, and are therefore provided as is, without warranty of any kind, neither expressed nor implied that the examples work or are fit for a particular purpose. The author and publisher assume no responsibility or liability for damages or losses, neither incidental nor consequential, incurred as a result of using the provided specifications or source code.

thought<sup>TM</sup>, The SubSubThought Premise Language<sup>TM</sup>, The thought Reference<sup>TM</sup>, and The thought Logo<sup>TM</sup>, The thought Programming Language<sup>TM</sup>, the [P] <sup>TM</sup> logo, are all Copyright © 2013 – 2022 thought Corporatoin. All Rights Reserved.

For all comments or electronic inquiries or permissions contact: <thought@hotmail.com>.

by mail: thought Corporation, 254 N. Lake Ave. #213, Pasadena, CA 91101 USA

This book was published in the United States of America.

Paperback ISBN-13: 978-1-795680-12-7 Paperback ISBN-10: 1-7956-8012-1

Cover by Michael S. P. Miller

Document version: 8.37

_For Mireille and Max._

# Contents

[Tables 11](#_Toc72468861)

[Acknowledgements 13](#_Toc72468862)

[Disclaimer 13](#_Toc72468863)

[Introduction 15](#_Toc72468864)

[1\. Foundation Modules 19](#_Toc72468865)

[2\. Quick Reference 20](#_Toc72468866)

[3\. Function Reference 31](#_Toc72468867)

[Bibliography 577](#_Toc72468868)

# Tables

[Table 1. Function Quick Reference 29](#_Toc536815138)

# Acknowledgements

“_Do you see over yonder, friend Sancho, thirty or forty_

_hulking giants? I intend to do battle with them and slay them._”

― Miguel de Cervantes Saavedra, Don Quixote

This work was not possible without the efforts and advice of Dr. Sheldon Linker, whose collaboration on terminology and functionality was most welcome, and combined with his proficient coding skills led to the 2013 Java implementation of a just in time interpreter: The Premise 0.1 Executive.  
Suzuki Hisao's lucid and concise C# implementation of Nukata Lisp Lite was insightful, as was Peter Norvig's implementation of JScheme. Allen Holub's book Compiler Design in C was also instructive, particularly in the area regarding approaches to tokenization and parsing. Christian Queinnec's tome, Lisp In Small Pieces, also provided invaluable insights on expression evaluation. Christian's encouragement on this project was greatly appreciated. Roland Hausser's left associative grammar was pivotal in the tokenizer design.

The author would also like to thank Aaron Hosford for his suggestions on numeric similarity metrics, Ryan Hewitt for his comments on prototype construction, Brian Shall for his ideas on restricted scoping, Dr. Ghassan Azar, Todd Kaufmann, Dr. Michael Schuresko, Robert Rossi, Jean-Louis Villecroze and the rest of the SubSubThought Premise Language group for their constructive feedback and suggestions.

# Disclaimer

The source code examples and specifications in this book are for illustrative purposes only, and are therefore provided as is, without warranty of any kind, neither expressed nor implied that the examples work or are fit for a particular purpose. The author and publisher assume no responsibility or liability for damages or losses, neither incidental nor consequential, incurred as a result of using the provided specifications or source code, up to and including loss of business, injury, or death.

# Introduction

The SubSubThought Premise Language is a functional prototype programming language which combines high level intrinsic primitives with seamless object persistence. The goal of the SubSubThought Premise Language is to provide a platform for artificial intelligence programming. Software agents written in Premise share a knowledge base where they can create, modify, and delete object instances amongst themselves in a stigmergic manner. Premise is influenced by Lisp, Self, JavaScript, OPS5, and CLIPS.

The SubSubThought Premise Language was developed by Michael S. P. Miller and Sheldon O. Linker during 2013 and 2014. In creating a platform for agent based programming for intelligent systems ( PAM-P2, JCB English ) they found a need for a very high level language in which to code asynchronous agent processes to perform complex pattern matching and inference. They explored the Sapir-Whorf hypothesis as it relates to computer programming–namely, that the primitive operations available in a computer language influence the way software developers frame and solve problems, and it was early determined that the primitives of the needed language should be very high level and include logical and similarity-based pattern matching, inference, messaging, stigmergy, and asynchrony. The language combines elements of declarative, functional, and imperative programming with seamless persistent object storage and retrieval. The goals of The SubSubThought Premise Language are simple:

- To define memory as a portable abstraction across different physical implementations. Premise uses a persistent object store as its memory.
- To facilitate the fast formation of relationships in a persistent memory. Constructing relationship instances in Premise is the same as asserting facts to the working memory of other declarative language platforms such as CLIPS or OPS.
- To allow rapid interrogation of relationships in the memory.
- To provide scalability to billions of relationship instances.
- To explore the Sapir Whorf hypothesis as it relates to computer programming: that the constructs available in computer languages influence the way people think about and solve problems.
- To explore the stigmergic programming paradigm, where objects constructed by one agent are later used or consumed by other agents.
- To provide a clear and concise API.

The SubSubThought Premise Language serves as a testbed for agent programming. Functions are the primary unit of processing. Numbers, strings, literals, relations, thoughts, lexicons, lists and calls provide the primary data types. The SubSubThought Premise Language opens up new possibilities for knowledge representation and artificial intelligence programming.

I hope you enjoy using this language.

Michael Miller

February 2019

## Document Conventions

The following are conventions used in this document.

### Source Code

Premise source code shall appear in Courier New font in a colored text region. The gray text region depicts a session in the Premise interpreter.

> (take "{a b c}")

.: {{a b c}}

A green text region depicts Premise source code snippets that appear in a file editor.

(relation Problem

:Name :Status

)

A blue text region depicts non-Premise source code snippets that appear in a file editor.

SELECT DISTINCT LENGTH(CategoryName)

FROM Category

### Source Code Comments

In-line comments are denoted by semicolons. Everything from the comment to the end of the line is ignored by the interpreter.

; this is an in-line comment

Multi-line comments are delimited by double quotation marks. Everything between the delimiters is treated as a single string and returned as-is by the interpreter. A free standing string, not part of a function or macro call, evaluates to itself, and thus can be used as a comment.

"this is a

multi-line

comment"

## Language Style Conventions

As a matter of style, each of the following language elements is written in a specific case:

Modules   are written in Pascal case.

Relations   are written in  Pascal case.  
:Slots           are written in Pascal case with a preceding colon.

!methods    are written in camel case with a preceding exclamation point.  
functions   use Camel case for verbs and Pascal Case for nouns.  
?locals (local variables) are in camel case with a preceding question mark.

?Modular (modular variables) are in Pascal case with a preceding question mark.

?Globals (global variables) are in Pascal case with a preceding question mark.

?CONSTANTS are written in upper case with a preceding question mark.  

# 1\. Foundation Modules

The SubSubThought Premise Language is divided into several modules which contain built-in (i.e., intrinsic) functions. Each module has a particular area of responsibility. For example, the IO module facilitates communication while the knowledge base module declares foundational functions.

### IO

This module contains functions which manage messaging, files, and the console.

### KB

This module provides the basic control structures and special forms of the language.

### Math

This module provides arithmetic, trigonometric, and statistical functions.

### Meta

This module contains the global environment.

### Tasks

This module has functions that manage asynchronous and concurrent tasks.

### User

This module contains the default environment.

# 2\. Quick Reference

A synopsis of each intrinsic function follows.

| No | Signature | Description |
| --- | --- | --- |
| 1   | (\-- number ) | Decrements a number by 1. |
| 2   | (\- number … ) | Subtraction. |
| 3   | (@ container place … ) | Retrieves elements from a sequence or assortment. |
| 4   | (\# container) | Returns the number of elements. |
| 5   | ($ value … ) | Creates a new string with intervening spaces . |
| 6   | ($$ value … ) | Creates a new string by eliding arguments. |
| 7   | (% command arguments ) | Performs an operating system command |
| 8   | (& value … ) | Merges arguments into a new sequence. |
| 9   | (&& value … ) | Mergs arguments into a new sequences and removes nils. |
| 10  | (\* number number … ) | Mulitplication. |
| 11  | (\*\* base exponent) | Exponentiation. |
| 12  | (/ dividend divisor … ) | Division. |
| 13  | (// number degree) | Nth Root. |
| 14  | (/~ value1 value2) | Calculates the dissimilarity between two values. |
| 15  | (/= value1 value2 … ) | Returns true if any values are not equal. |
| 16  | (~ value1 value2) | Calculates the similarity between two values. |
| 17  | ( ' variant ) | Quotes a variant. |
| 18  | ( \` variant ) | Expands a variant by substituting values. |
| 19  | (+ number number . . . ) | Addition. |
| 20  | (++ number ) | Increments a number by 1. |
| 21  | (<-- function symbol value … ) | The value before tying a symbol to a new value. |
| 22  | (< value value … ) | True if each value is less than the next. |
| 23  | (<= value value … ) | True if each value is less or equal to the next. |
| 24  | (<== container function place value … ) | The value before replacement. |
| 25  | (\= value value … ) | True if each value is equal to the next. |
| 26  | (\==> container function place value … ) | The value after replacement. |
| 27  | (> value value … ) | True if each value is greater than the next. |
| 28  | (\--> function symbol value … ) | The value after tying a symbol to a new value. |
| 29  | (\>= value value … ) | True if each value is greater or equal to the next. |
| 30  | (\n quantity) | Returns a string containing one or more new lines. |
| 31  | (\\s quantity) | Returns a string containing one or more spaces. |
| 32  | (^ thought) | Returns a thought identifier. |
| 33  | (abolish symbols environment ) | Deletes symbols from an environment. |
| 34  | (abort tasks ) | Forcibly terminates one or more tasks |
| 35  | (about) | Provides system and version information. |
| 36  | (abs number) | Calculates the absolute value. |
| 37  | (absent url ) | True if a file, folder, or ur does notl exist. |
| 38  | (acosecant number geometry metrum) | Calculates the inverse cosecant. |
| 39  | (acosine number geometry metrum) | Calculates the inverse cosine. |
| 40  | (acotangent number geometry metrum) | Calculates the inverse cotangent. |
| 41  | (actual symbol) | Returns the underlying symbol referenced by an alias. |
| 42  | (add assortment entry … ) | Modifies an assortment by adding entries. |
| 43  | (address url) | Returns the address of a URL web resource. |
| 44  | (agent job url handler delay) | Creates an agent. |
| 45  | (alias symbol) | Returns a reference to a symbol. |
| 46  | (align sequence ordering) | Returns a sorted list using the provided ordering. |
| 47  | (all condition … ) | True if all relevant knowledge satisfies all of the conditions. |
| 48  | (alphabetic-p value) | True if the first position of a string is alphabetic. |
| 49  | (alphanumeric-p value) | True if the first position of a string is whitespace. |
| 50  | (and truth truth … ) | Logical conjunction. |
| 51  | (any condition … ) | True if some relevant knowledge satisfies all of the conditions. |
| 52  | (append sequence value … ) | Inserts values at the end of a sequence. |
| 53  | (apply function arguments environment) | Applies a function to a list of arguments. |
| 54  | (arguments what ) | Returns a list of arguments to a call or task. |
| 55  | (arity function kind) | Returns the number of symbols in a function's parameter list. |
| 56  | (array dimensions option) | Returns a multi dimensional list. |
| 57  | (asecant number geometry metrum) | Calculates the inverse secant. |
| 58  | (asine number geometry metrum) | Calculates the inverse sine. |
| 59  | (ask who message timeout default ) | Sends a message to a recipient and awaits a response. |
| 484 | (assert premise … ) | Adds premises to the knowledge base. |
| 60  | (assign assignment … ) | Adds symbols in tandem to the current environment. |
| 61  | (assume premise … ) | Adds premises to the knowledge base. |
| 62  | (atangent number geometry metrum) | Calculates the inverse tangent. |
| 63  | (attach knowledge ) | Registers a knowledge base. |
| 64  | (average symbol … binding sequence expression … ) | The arithmetic mean of a sequence. |
| 65  | (avg value …) | The arithmetic mean. |
| 66  | (await task timeout default) | Returns the result of a task. |
| 67  | (before-p interval1 interval2 tolerance) | True if an interval finishes before a second interval. |
| 68  | (beginning interval) | Returns the beginning instant of an interval |
| 69  | (best probe candidates option ... ) | Returns the best matching candidates. |
| 70  | (beyond sequence position ) | True if a position is outside a sequence. |
| 71  | (big value ) | Converts a value to a big number. |
| 72  | (bind container assignment … ) | Assigns symbols to values in sequences or assortments. |
| 73  | (bion name work ) | Returns a resource that hosts a cluster of cells for doing tasks. |
| 74  | (bindings pattern ) | Returns a list of symbol value pairs for an environment or premise. |
| 75  | (bitwise number op … ) | Performs bitwise operations. |
| 76  | (bound function) | Returns the symbols that are bound in a function. |
| 77  | (bound-p symbol) | True if a symbol has a value. |
| 78  | (bracket truth) | Returns 1 if a truth expression is true, 0 otherwise. |
| 79  | (break value) | Terminates a loop. |
| 80  | (busy-p task) | True if a task has not completed. |
| 81  | (but sequence quantity) | Creates a subsequence of all except the last elements. |
| 82  | (bye) | Terminates the interpreter. |
| 83  | (call value … ) | Creates an unevaluated call. |
| 84  | (can expression result error ) | Evaluates an expression while suppressing failures. |
| 85  | (cancel tasks option … ) | Cooperatively cancels tasks. |
| 86  | (cancelled-p task) | True if a task has been cancelled. |
| 87  | (canonify variant ) | Makes equal values identical. |
| 88  | (capitalize string option) | Capitalizes a string. |
| 89  | (case probe clause … else-clause) | Branches execution based on a value. |
| 90  | (categorize sequence predicate …) | Creates a list of equivalence sets. |
| 91  | (cede alias ) | Transfers a value between symbols. |
| 92  | (ceiling number) | Rounds a number towards positive infinity. |
| 93  | (cell bion work ) | Returns a resource that hosts tasks. |
| 94  | (channel task ) | Returns a url to the arguments of a task. |
| 95  | (char unicode) | Converts a Unicode value into a one position string. |
| 96  | (choose sequence selector transform) | Returns the arguments satisfying a function. |
| 97  | (clear container) | Eliminates all entries from an assortment or sequence. |
| 98  | (clip value minimum maximum) | Returns a value within a clipped range. |
| 99  | (clone atom modification … ) | Clones an atom with possible modifications. |
| 100 | (close url) | Closes a file or data url. |
| 101 | (closure scope type name params expression …) | Creates a function or macro with a defined environment. |
| 102 | (coalesce symbol … gate expression … ) | Returns a merged sequence. |
| 103 | (collect symbol … gate expression … ) | Returns a transformed sequence. |
| 104 | (collection element … ) | Returns an unorderd collection of elements. |
| 105 | (combine assortment entry … ) | Creates a new assortment by combining entries. |
| 106 | (common sequences) | Creates a sequence of common elements among subsequences. |
| 107 | (comparable-p value1 value2 ) | Returns true if the values can be compared. |
| 108 | (compare value1 value2) | Returns &lt; (less), = (equal), or &gt; (greater). |
| 109 | (complete expression … ) | Runs expressions concurrently until completion. |
| 110 | (complex real imaginary) | Converts a value to a complex number. |
| 111 | (compose functions arguments) | Applies functions in reverse order using the arguments. |
| 112 | (conceive knowledge ) | Creates a knowledge base. |
| 113 | (concurrent expression … ) | Evaluates expressions asynchronously. |
| 114 | (configuration url association ... ) | Creates a configuration file. |
| 115 | (confirm condition since reason ) | Tests that a condition is true. |
| 116 | (confute condition since reason ) | Tests that a condition is false. |
| 117 | (connect data ) | Connects to a data resource. |
| 118 | (constant assignment … ) | Creates a constant. |
| 119 | (contains assortment value ) | True if a value is present in an assortment. |
| 120 | (continue result) | Continues to the next iteration of a loop. |
| 121 | (convertible-p value taxon) | True if the value can be converted to the taxon. |
| 122 | (copy sequence count ) | Copies a sequence. |
| 123 | (copyright) | Displays copyright information. |
| 124 | (correlate list1 list2) | Finds the correlation coefficient of two lists. |
| 125 | (cosecant number geometry metrum) | Calculates the cosecant. |
| 126 | (cosine number geometry metrum) | Calculates the cosine. |
| 127 | (cotangent number geometry metrum) | Calculates the cotangent. |
| 128 | (count symbol … binding sequence as counter expression … ) | Counts the iterations and returns the last expression. |
| 129 | (critical locks option … expression …) | Serializes evaluations across regions of code. |
| 130 | (cut assortment key … ) | Removes elements from assortments by key. |
| 131 | (data option … ) | Creates a data url. |
| 132 | (date yr mth day hrs mins secs zone zmins) | Creates a new date or returns the current date. |
| 133 | (declared-p symbol environment) | True if a symbol exists in an environment. |
| 134 | (decode source format) | Decodes a string. |
| 135 | (default value … ) | Returns the first non-nil value. |
| 136 | (definitions environment ) | Retrieves literal value pairs in an environment. |
| 137 | (defunct function) | Undefines a function in a module. |
| 138 | (degrees radians) | Converts radians into degrees. |
| 139 | (delete sequence value … ) | Modifies sequence by deleting values. |
| 140 | (dependencies module) | Returns a module's dependencies. |
| 141 | (deq container place option) | Removes an element from an embedded sequence. |
| 142 | (describe literal) | Returns descriptions of a literal. |
| 143 | (detach knowledge ) | Unregisters a knowledge base. |
| 144 | (difference sequence1 sequence2 operation) | Returns the difference of two sequences. |
| 145 | (did expression ) | Evaluates an expression and surpresses failures. |
| 146 | (digit number position) | Returns the digit in the specified position of a number. |
| 147 | (digit-p value) | True if the first position of a string is a digit. |
| 148 | (digits number) | Returns the digits comprising a number. |
| 149 | (dimensions sequence) | Returns the lengths of each dimension in a sequence. |
| 150 | (discard module) | Discards a module. |
| 151 | (disjoint-p sequence sequence … ) | True if no elements are common among sequences. |
| 152 | (distinct sequence ) | Creates a new sequence without duplicate elements. |
| 153 | (dstribute sequence function result) | Applies a function to a sequence in parallel. |
| 154 | (divide dividend divisor default) | Performs safe division. |
| 155 | (divisible-p dividend divisor) | True if the divisor evenly divides the dividend. |
| 156 | (do expression … ) | Creates a lexical scope. |
| 157 | (done) | Terminates a generator. |
| 158 | (drop index) | Removes a relation index. |
| 159 | (duplicate source target option) | Duplicates a file or contents of a folder. |
| 160 | (during-p interval1 interval2 tolerance) | True if an interval occurs within a second interval. |
| 161 | (dynamic assignments expression … ) | Creates a dynamic environment for symbols. |
| 162 | (e) | Returns Euler's number, 2.718281828459045. |
| 163 | (each symbol … binding reversal sequence … premises option … action ) | Combines for and with to iterate over sequences to match patterns against the knowledge base. |
| 164 | (encode source format) | Encodes a string. |
| 165 | (enq container place entry) | Inserts an element into an embedded sequence. |
| 166 | (ensure check … ) | Performs type checking. |
| 167 | (entries assortment ) | Retrieves key value pairs for an assortment. |
| 168 | (enumeration name element … ) | Defines an enumerated assortment. |
| 169 | (enumerations) | Returns a list of all enumerations. |
| 170 | (environment parent entry … ) | Creates a new context for symbols and functions. |
| 171 | (epoch time) | Returns a Unix epoch or the current epoch. |
| 172 | (eradicate knowledge ) | Deletes a knowledge base. |
| 173 | (erase file option … ) | Deletes files or folders. |
| 174 | (escape) | Escapes to the next resume tag in the stack. |
| 175 | (eval expression environment ) | Evaluates an expression. |
| 176 | (even-p number) | True if the number is even. |
| 177 | (every symbol … binding sequence expression … test) | True if a predicate is true for every element in a sequence. |
| 178 | (exactly quantity of sequence clause within margin ) | True if a number of elements satisfy a clause. |
| 179 | (exchange sequence substitution … ) | Creates a new sequence with values swapped. |
| 180 | (excludes sequence element option … ) | True if a sequence does not contain an element. |
| 181 | (exists-p value) | True if a value is a thing.. |
| 182 | (exit value) | Explicitly ends a task using a return value. |
| 183 | (exponential number significand) | Calculates the base ten exponent of a number. |
| 184 | (expression value … ) | Creates an expression. |
| 185 | (extend module expression … ) | Adds new definitions to a module. |
| 186 | (facility name parameters expression … ) | Creates a private function in a module. |
| 188 | (few symbol … binding sequence expression … test) | True if a predicate is true for less than half the elements in a sequence. |
| 189 | (file option … ) | Opens or creates a file. |
| 190 | (files option …) | Returns a list of file names. |
| 191 | (fill symbol from start to end by increment with expression) | Fills a list with the result of an expression. |
| 192 | (filter sequence predicate ) | Returns a sequence of elements that satisfy a predicate. |
| 193 | (find features candidates option ... ) | Returns the best matching candidates. |
| 194 | (finishes-p interval1 interval2 tolerance) | True if two intervals finish together. |
| 195 | (finishing interval) | Returns the finishing instant of an interval. |
| 196 | (fix declaration … ) | Adds symbols to the current environment |
| 197 | (float value ) | Converts a value to a floating number. |
| 198 | (floor number) | Rounds a number towards negative infinity. |
| 199 | (fold symbol … in sequence into expression … ) | Tranforms a sequence into a value. |
| 200 | (folder option … ) | Creates or locates a folder in the file system. |
| 201 | (folders option … ) | Returns a list of sub folders. |
| 202 | (for symbol … binding reversal sequence … expression … ) | Iterates over the elements in a sequence. |
| 203 | (forever expression … ) | Repeatedly evaluates expressions. |
| 204 | (forgo dependency module) | Removes a dependent module. |
| 205 | (format template value … ) | Formats a string. |
| 206 | (fractional number) | Returns the fractional portion of a number. |
| 207 | (free resources ) | Releases resources. |
| 208 | (full first second ) | True if values are equal or either value is nil. |
| 209 | (function scope name params returning expression … ) | Creates a public function in a module. |
| 210 | (functions module) | Returns a list of functions defined in a module. |
| 211 | (gather symbol … binding sequence expression … test) | Returns a sequence of elements that satisfy a predicate. |
| 212 | (generator name parameters expression … ) | Creates a series generator. |
| 213 | (get container key … ) | Retrieves a value using one or more keys. |
| 214 | (given { parameter … } expression … ) | Creates an anonymous function. |
| 215 | (global assignment … ) | Creates global symbols. |
| 216 | (globals) | Creates list of global symbols. |
| 217 | (go function argument … ) | Transfers control to a function. |
| 219 | (grok theory) | Evaluates expressions in a url or file. |
| 220 | (group list by key … into symbol expression … ) | Combines sublists by position or key. |
| 221 | (halt compute ) | Terminates a cell or bion. |
| 223 | (has assortment key ) | True if a key is present in an assortment. |
| 224 | (hash value option … ) | Computes a hash code. |
| 225 | (help function) | Describes a function. |
| 226 | (hyperlink option … ) | Creates a hyperlink. |
| 227 | (id resource ) | Returns a resource number. |
| 228 | (identical-p value value … ) | True if all values occupy the same memory location. |
| 229 | (identity value) | Returns the value itself. |
| 230 | (idle duration) | Pauses for a specified interval. |
| 231 | (if condition expression … or-clause … else-clause) | Branched conditional evaluation. |
| 232 | (imaginary value) | Converts a value to an imaginary number. |
| 233 | (in value container option … ) | True if a value is in a sequence or assortment. |
| 234 | (includes sequence element option … ) | True if a value is in a sequence. |
| 235 | (index relation slot … ) | Creates an index on slots of a relation. |
| 236 | (indices relation ) | Returns a list of indices for a relation. |
| 237 | (infix sequence delimeter) | Creates a new sequence with interposed delimeters. |
| 238 | (inside value ) | Creates an expression from a sequence or assortment. |
| 239 | (insert sequence position value … ) | Creates a new sequence by nserting values. |
| 240 | (insort sequence value option … ) | Inserts a value into a sorted sequence. |
| 241 | (instantiate expression ) | Creates an expression with premises in place of thoughts. |
| 242 | (integer value ) | Converts a value to an integer. |
| 243 | (interleave sequence sequence … ) | Merges arguments into a new sequence. |
| 244 | (intersection sequence sequence … ) | Creates a sequence of common elements. |
| 245 | (intersects-p sequence sequence … ) | True if any elements are common among sequences. |
| 246 | (interval start finish) | Creates a time interval. |
| 247 | (into relation thoughts) | Creates new thoughts based on existing thoughts. |
| 248 | (invoke call environment) | Invokes a call. |
| 249 | (is value predicate) | True if the value is true or if the applied predicate returns true. |
| 250 | (junction scope name params expression … ) | Creates a public function where arguments are evaluaed in parallel. |
| 251 | (key assortment value ) | Finds the key for a value in an assortment. |
| 252 | (keys assortment ) | Creates a list of keys for an assortment. |
| 253 | (keywords) | Creates the list of Premise keywords. |
| 254 | (knew relation criterion … ) | Finds or creates a thought. |
| 255 | (knowledge option … ) | Finds or creates a knowledge base. |
| 256 | (known pattern … option … ) | True if the patterns match. |
| 257 | (lacks assortment key ) | True if a key is absent from an assortment. |
| 258 | (last sequence count) | Creates a subsequence of the last elements. |
| 259 | (left first second ) | True if values are equal or the second value is nil. |
| 260 | (let manner assignment ... ) | Adds symbols to the current environment. |
| 261 | (lexemes string) | Creates an uppercase string with spaces between words. |
| 262 | (lexicon association … ) | Creates a lexicon. |
| 263 | (lexicons) | Creates a list of all lexicons. |
| 264 | (license) | Prints the software license. |
| 265 | (like sequence pattern) | Compares a pattern to a sequence. |
| 266 | (list value … ) | Creates a list. |
| 267 | (literal value) | Creates a literal. |
| 268 | (local assignments expression … ) | Creates a task level scope. |
| 269 | (location symbol) | Sets a symbol to the current location. |
| 270 | (log number base) | Logarithm. |
| 271 | (long value) | Converts a value to a long number. |
| 272 | (loop expression … gate ) | Repeatedly evaluates expressions. |
| 273 | (lowercase string) | Converts a string to lower case. |
| 274 | (macro name parameters expression … ) | Creates a public macro in a module. |
| 275 | (macros module) | Creates a list of macros defined in a module. |
| 276 | (make prototype term … ) | Creates a record by creating a relationship if it does not exist. |
| 277 | (map sequence ... function) | Applies a function to elements across sequences. |
| 278 | (max value … ) | Finds the maximum element. |
| 279 | (maximum symbol … binding sequence expression … ) | Finds the maximum element. |
| 280 | (may expression ) | Evaluates an expression while surpressing failures. |
| 281 | (median value …) | Finds the middle value of a sequence. |
| 282 | (meets-p interval1 interval2 tolerance) | True if an interval finishes when a second interval starts. |
| 283 | (meron value) | Returns the meronomic prototype of a value. |
| 284 | (meron-p value meron) | True if the value is a meron or is of the specific meronomic type. |
| 285 | (meronomy value) | Returns the meronomic prototypes of a value. |
| 286 | (method scope name params expression … ) | Creates a public method in a prototype. |
| 287 | (mid sequence start distance ) | Copies a subsequence of a sequence. |
| 288 | (min value … ) | Finds the minimum element. |
| 289 | (minimum symbol … binding sequence expression … ) | Finds the minimum element. |
| 290 | (missing assortment value ) | True if a value is absent from an assortment. |
| 291 | (mod dividend modulus) | Finds the remainder after division. |
| 292 | (modular module expression … ) | Evaluates expressions in module's scope. |
| 293 | (module name definition … ) | Creates a module. |
| 294 | (modules) | Creates a list of known modules. |
| 295 | (moment units secs mins hours days year ) | Creates a moment or returns the current moment. |
| 296 | (more-p sequence) | True if a container has more than zero elements. |
| 297 | (morph arguments functions) | Applies functions in succession using the arguments. |
| 298 | (most symbol … binding sequence expression … test) | True if the predicate is true for more than half of the elements in a sequence. |
| 299 | (move source destination) | Moves or renames one or more files. |
| 300 | (my) | Returns the current cell resource. |
| 301 | (nall condition … ) | True if not all relevant knowledge satisfies all of the conditions. |
| 302 | (nand truth truth … ) | Negated logical conjunction. |
| 303 | (negative-p number) | True if a number is negative. |
| 304 | (nevery symbol … binding sequence expression … test) | True if the predicate is false for any element in the sequence. |
| 305 | (new prototype term … ) | Creates a record. |
| 306 | (next series) | Advances a series to the next element. |
| 307 | (ngrams string length) | Creates a list of substrings. |
| 308 | (nix prototype) | Deletes a prototype. |
| 309 | (no condition … ) | True if no relevant knowledge satisfies all of the conditions. |
| 310 | (none symbol … binding sequence expression … test) | True if the predicate is false for all sequence elements. |
| 311 | (nor truth truth … ) | Negated logical disjunction. |
| 312 | (not value predicate) | True if a value is false, or if the applied predicate returns false. |
| 313 | (nothing) | Returns nothing. |
| 314 | (null-p value) | True if a value is not a thing.. |
| 315 | (odd-p number) | True if a number is odd. |
| 316 | (old thought) | Deletes a thought. |
| 317 | (omit sequence value … ) | Creates a new sequence with values removed. |
| 318 | (on condition true-case false-case ) | Branched conditional evaluation. |
| 319 | (only symbols expression … ) | Creates a restricted scope. |
| 320 | (open url) | Opens a file or data url. |
| 321 | (or truth truth … ) | Logical disjunction. |
| 322 | (out value sequence option … ) | True if a value is absent from a sequence. |
| 323 | (overlaps-p interval1 interval2 tolerance) | True if an interval finishes after a second interval starts. |
| 324 | (pad sequence length value side ) | Creates a new padded sequence. |
| 325 | (parameters what ) | Returns a list of parameters for a function, call, or task. |
| 326 | (partition sequence pivot comparer) | Creates a list of equivalence sets for a pivot element. |
| 327 | (path folder separator file) | Concatenates a folder and file name. |
| 328 | (pattern expression … ) | Creates a pattern containing the supplied expressions. |
| 329 | (perform environment method instance … ) | Invokes a method within an environment. |
| 330 | (pi) | Returns 3.141592653589793. |
| 331 | (pick sequence quantity) | Creates a list of randomly selected elements. |
| 332 | (pipe option … ) | Creates a pipe. |
| 333 | (pop sequence position ) | Returns the element removed from a sequence. |
| 334 | (posit module url) | Writes module expressions to a url. |
| 335 | (position sequence element option … ) | Finds the position of an element or subsequence in a sequence. |
| 336 | (positions sequence) | Returns positions of an element in a sequence or position value pairs. |
| 337 | (positive-p number) | True if a number is greater than zero. |
| 338 | (premise value ) | Creates a premise representation of a value. |
| 339 | (probability events A operation B) | Calculates the probability over a series. |
| 340 | (proceed … resumption … finally … ) | Evaluates expressions and resumes from an escape. |
| 341 | (product symbol … binding sequence expression …) | Multiplies an expression over a range of values. |
| 342 | (punctuation-p string) | True if the first position of a string is punctuation. |
| 343 | (push sequence value position ) | Modifies a sequence by inserting a value. |
| 344 | (put container entry … ) | Updates values in an assortment or sequence. |
| 345 | (qualified module function) | Prepends a module to a function name. |
| 346 | (qualifiers identifier) | Creates a list of modules associated with an identifier. |
| 347 | (quantify sequence predicate option … ) | Returns a quantifier for elements satisfying a test. |
| 348 | (quantity symbol … binding sequence expression … test) | Returns the number of elements satisfying a test. |
| 349 | (radians degrees) | Converts degrees to radians. |
| 350 | (radix number base ) | Converts a number to a base. |
| 351 | (random lower to upper precision) | Creates a random number. |
| 352 | (range first to last by increment) | Creates a list of numbers. |
| 353 | (rational numerator denominator) | Converts values to a rational number. |
| 354 | (read file count bits) | Creates a string or stream. |
| 355 | (ready-p task) | True if a task has completed. |
| 356 | (real value) | Converts a value to a real number. |
| 357 | (reasoning toggle) | Toggles asynchronous rule execution. |
| 358 | (reclaim) | Performs garbage collection. |
| 359 | (reduce sequence function) | Converts a sequence into a value. |
| 360 | (relation name inclusion … definition … ) | Creates a relation. |
| 361 | (relations) | Returns a list of defined relations. |
| 362 | (release locks) | Releases locks on critical sections. |
| 363 | (remove assortment value … ) | Creates a new assortment by removing values. |
| 364 | (repeat count expression … ) | Loops a specified number of times. |
| 365 | (replace container entry … ) | Creates a new assortment or sequence by updating values. |
| 366 | (require module as moniker from url …options …) | Retrieves an absent module from a url. |
| 367 | (reset series) | Resets a series for reuse. |
| 368 | (resize sequence length default) | Modifies the length of a sequence. |
| 369 | (rest sequence skip) | Creates a subsequence of all except the first elements. |
| 370 | (retract rules) | Eliminates rules. |
| 371 | (return value from function) | Terminates a function call. |
| 372 | (reverse sequence) | Creates a reversed sequence. |
| 373 | (right first second ) | True if values are equal or the first value is nil. |
| 374 | (rip assortment value … ) | Removes elements from assortments by value. |
| 375 | (round number) | Rounds a number to the nearest integer. |
| 376 | (rule name properties when premises option … action … ) | Creates a rule. |
| 377 | (rules) | Creates a list of all rules. |
| 378 | (same value value … ) | True if all values are equal or contain equal elements. |
| 379 | (scale list scalar … function) | Applies a function to a list of numbers and scalar values. |
| 380 | (scatter arguments functions) | Applies functions in parallel returning a list of results. |
| 381 | (scope keyval ... ) | Finds an environment or gets the current environment. |
| 382 | (seal prototype) | Prohibits new records. |
| 383 | (secant number geometry metrum) | Calculates the secant of the number. |
| 384 | (seconds seconds) | Creates a seconds value or returns seconds since year zero. |
| 385 | (seek file position) | Repositions a file resource to a new read/write location. |
| 386 | (self) | Returns the currently executing task resource. |
| 387 | (separator kind) | Creates a separator string. |
| 388 | (series iterable) | Creates a series. |
| 389 | (service url handler) | Creates and starts a web service. |
| 390 | (set assignment ... ) | Assigns symbols to values in tandem. |
| 391 | (settings url association ... ) | Creates a configuration file.. |
| 392 | (sever assortment key … ) | Creates a new assortment by removing keys. |
| 393 | (shuffle sequence seed) | Creates a reordered sequence. |
| 394 | (sigma list ) | Calculates the sigma of a sequence. |
| 395 | (sign number option … ) | Returns the sign of a number as a number, sigil, or word. |
| 396 | (signal type term …) | Signals a failure. |
| 187 | (resignal tuple) | resignals a failure. |
| 397 | (significand number kind) | Calculates the modified significand as a number between 1 and 10, or zero. |
| 398 | (sine number geometry metrum) | Calculates the sine of a number. |
| 399 | (so expression … ) | Creates a task level scope. |
| 400 | (socket option … ) | Creates a TCP socket. |
| 401 | (some symbol … binding sequence expression … test) | True if the test is true for any element in the sequence. |
| 402 | (sort sequence ordering option … ) | Creates a sorted sequence. |
| 403 | (split sequence delimiter) | Creates a list of subsequences divided at a delimiter. |
| 404 | (starts-p interval1 interval2 tolerance) | True if two intervals start together. |
| 405 | (statistics numbers ) | Finds the mean, median, sigma, and count of a list of numbers. |
| 406 | (step symbol from i limit j by k expression … ) | Loops a symbol over a numeric range to evaluate expressions. |
| 407 | (stream streamable ) | Creates a stream. |
| 408 | (string value … ) | Converts a value to a string. |
| 409 | (structure name inclusion … definition … ) | Creates a structure. |
| 410 | (structures) | Creates a list of all structures. |
| 411 | (sub sequence entry … ) | Replaces a subsequence within a sequence. |
| 412 | (subset-p subset superset ) | True if all elements in a subset are in a superset. |
| 413 | (substitute sequence entry … ) | Copies a sequence and replaces subsequences. |
| 414 | (subsumes-p superset subset …) | True if all elements in each subset are in the superset. |
| 485 | (such symbol that premises option) | Returns a list of thoughts. |
| 415 | (sum value …) | Calculates the arithmetic sum. |
| 416 | (summation symbol … binding sequence expression … ) | Adds an expression over a set of values. |
| 417 | (supply arguments function environment) | Applies a function to an argument list. |
| 418 | (suppose facts action goals by strategies via operators limit quantity gate condition within timeframe before timepoint options options) | Performs hypothetico-deductive reasoning. |
| 419 | (survey format relation slot) | Creates a list of referents or referent-count pairs. |
| 420 | (swap sequence substitution …) | Modifies a sequence by interchanging values. |
| 421 | (symbol name ) | Creates a symbol. |
| 422 | (symbols environment ancestors ) | Lists the symbols in an environment. |
| 423 | (take readable count) | Creates an expression from a readable sequence. |
| 424 | (takeable readable desired) | Calculates the number of expressions that can be read. |
| 425 | (tally pattern ) | Returns the number of matches in the knowledge base. |
| 426 | (tangent number geometry metrum) | Calculates the tangent. |
| 427 | (tarry tasks expression … ) | Allows tasks to complete on their own. |
| 428 | (task scope expression … ) | Creates a list of tasks for deferred evaluation. |
| 429 | (tasks) | Creates a list of all tasks. |
| 430 | (taxon value) | Returns the datatype of a value. |
| 431 | (taxon-p value taxon) | True if the value is of the specific taxonomic type. |
| 432 | (taxonomy value) | Returns a list of datatypes for a value. |
| 433 | (tell who message timeout) | Sends a message to a recipient. |
| 434 | (there url ) | True if a file, folder, or url exists. |
| 435 | (this series) | The current element of a series. |
| 436 | (thought relation id ) | Finds an extant thought. |
| 437 | (thunk expression … ) | Creates a thunk in a module. |
| 438 | (thunks module) | Returns a list of thunks defined in a module. |
| 439 | (tick nanoseconds) | Creates a tick or returns nanoseconds since year zero. |
| 440 | (tie assignment ... ) | Assigns symbols to values in parallel. |
| 441 | (time unit operation time … ) | Performs time operations. |
| 442 | (top sequence count) | Creates a subsequence of the first elements. |
| 443 | (transfer source destination option … ) | Transfers a value from one sequence to another. |
| 444 | (traverse symbol binding sequence limit dimensions expression … ) | Loops through the coordinates of a sequence. |
| 445 | (trim sequence option … ) | Creates a sequence without front and rear delimiters. |
| 446 | (truncate number) | Rounds a number towards zero. |
| 447 | (try expression … learn symbol recovery … finally cleanup … ) | Evaluates expressions and recovers from signals. |
| 448 | (tuple value … ) | Creates a tuple. |
| 449 | (uid) | Creates a unique identifier. |
| 450 | (unbound function) | Creates a list of free symbols for a function. |
| 451 | (unbound-p symbol) | True if a symbol is unbound. |
| 452 | (unicode string) | The Unicode of a string’s first position. |
| 453 | (union sequence sequence … ) | Concatenates sequences removing duplicates. |
| 454 | (union sequence sequence … ) | Concatenates sequences removing duplicates. |
| 455 | (unique prefix) | Creates a unique literal based on a prefix. |
| 456 | (unless condition false-case true-case ) | Branched conditional execution. |
| 457 | (unlike sequence pattern) | True if a pattern does not match a sequence. |
| 458 | (unqualified function) | The function literal without the module prefix. |
| 459 | (unseal prototype) | Permits new records for a protoytpe. |
| 460 | (unsigned value ) | Converts a value to an unsigned number. |
| 461 | (until condition expression … ) | Loops expressions until a condition is true. |
| 462 | (unwrap module) | Permits modifications to a module. |
| 463 | (uppercase string) | Converts a string to uppercase. |
| 464 | (uppercase-p value) | True if a string's first position is upper case. |
| 465 | (url option … ) | Creates a URL resource. |
| 466 | (use knowledge expression …) | Evaluates expressions in a knowledge base scope. |
| 467 | (values assortment) | Creates a list of values for an assortment. |
| 468 | (vector atom … ) | Creates a vector of atoms. |
| 469 | (version) | Provides version information. |
| 470 | (void-p sequence) | True if a container has zero elements. |
| 471 | (wait tasks timeout ) | Waits for tasks to end. |
| 472 | (which pattern options ...) | Creates a list of thoughts for a pattern. |
| 473 | (while condition expression … ) | Loops expressions while a condition is true. |
| 474 | (whitespace-p value) | True if the first position of a string is whitespace. |
| 475 | (with premises option … action expression ) | Matches patterns against the knowledge base. |
| 476 | (within sequence position ) | True if a position is inside a sequence. |
| 477 | (wrap module) | Prohibits modifications to a module. |
| 478 | (write writeable value … ) | Writes values to a writeable resource. |
| 479 | (xnor truth truth) | Logical equivalance. |
| 480 | (xor truth truth) | Logical exclusive disjunction. |
| 481 | (yield value) | Returns a result from a series generator. |
| 482 | (zap container place … ) | Updates associations and sequences with nil values. |
| 483 | (zero-p number) | True if a number is zero. |

Table . Function Quick Reference

# 3\. Function Reference

This chapter outlines each function in detail.

## \-- decrement_

Decrements a number by 1.

##### Syntax
```
(\-- number )


```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1   | A number or list to be decremented by 1. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The decremented number. |

##### Remarks

This function decrements the argument by 1. If an argument is a list, then each element of the list is decremented.

##### Example

```

> (-- 1)

.: 0

> (-- -1)

.: -2

> (-- -1000+i)

.: -1001+i

> (-- {5 -8 90 32})

.: {4 -9 89 31}

```

##### Related

++ increment

## \- subtraction

Subtraction.

##### Syntax
```

(\- number … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1+  | A number or list to be subtracted. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The difference of all supplied numbers as a number or a list of differences. |

##### Remarks

If there is one argument, the sign is reversed. If there are two or or more arguments, all arguments are subtracted from the first. If any of the arguments are unknown, infinity or ninfinity (i.e. negative infinity), the result shall respectively be unknown, infinity, or ninfinity. If an argument is a list, then each element of the list is subtracted. If a scalar and a list are subtracted, then the scalar is subtracted from each element of the list.

##### Example


```

> (- 1 2 3 4 5)

.: -13

> (- 1)

.: -1

> (- (- 1))

.: 1

> (- {3 4 5} 2 {1 0 2})

.: {0 2 1}
```


##### Related

\+ addition, / division , \* multiplication

## @ element

Retrieves elements from a sequence or assortment.

##### Syntax
```

(@ container place … )

place ::= integer

place ::= #

place ::= { integer … }

place ::= key

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | A sequence, assortment, or record. |
| place | variant | 0+  | An integer position, the literal # for the last item, or a list of positions designating a coordinate, or an assortment key. |

##### Results

| Taxon | Description |
| --- | --- |
| expression | Returns the item(s) at the position(s). |

##### Remarks

For sequences, this function returns the element(s) at the one-based position in the sequence. If place is not specified, the first element is returned. If place is the literal #, then the last item is returned. If place is a number or list of numbers, the item at the place within the sublist is returned. If the sequence is empty, or if a coordinate or position does not exist, the function fails. For assortments, the place is a required parameter and must correspond to a key within the assortment, otherwise the function fails.

##### Example
```

> (@ "abcde")

.: "a"

> (@ {{{a}{b}}{{c}{d}}} {1 2 1})

.: b

> (@ (lexicon a 1 b 2 c 3) a c)

.: 1 3

```

##### Related

# size, add, append, cut, put, enq, deq, has, lacks

## # size_

Returns the number of elements.

##### Syntax
```

(\# container)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | A sequence, assortment or resource. |

##### Results

| Taxon | Description |
| --- | --- |
| integer | The number of elements. |

##### Remarks

Returns the number of elements in a sequence or assortment. If a file resource is provided, then it returns the file size in bytes.

##### Example
```

> (# {a b c d e})

.: 5

> (# "she sells sea shells")

.: 20

> (# (lexicon a b c d))

.: 2

> (# (environment (scope) ?a 1 ?b 2 ?c 3 ?d 7))

.: 4

> (# (enumeration Colors red orange yellow))

.: 3

> (# (file (path "." "/" "premise.out")))

.: 436

```

##### Related

@ element 

## $ concatenate

Creates a new string with intervening spaces .

##### Syntax
```

($ value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| string | The concatenated string. |

##### Remarks

Returns the concatenation of all values presented. All values are converted to strings, then concatenated. A space is preserved between each argument. Leading and trailing spaces are omitted. Any occurrence of the literal \\s is replaced with a space. Any occurrence of the literal \n is replaced with a newline.

##### Example
```

> ($ the quick "brown" fox)

.: "the quick brown fox"

> ($ "the quick" \\s "brown fox")

.: "the quick brown fox"

> ($ {the quick} {} {brown fox})

.: "{the quick} {} {brown fox}"

> ($ atom \n molecule)

.: "atom

molecule"

> ($)

.: ""

```

##### Related

$$ elide, string

## $$ elide

Creates a new string by eliding arguments.

##### Syntax
```

($$ value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| string | The concatenated string without spaces. |

##### Remarks

Returns the elision of all values presented. All values are converted to strings, then concatenated. Spaces are removed between arguments as are leading and traling spaces. Any occurrence of the literal \\s is replaced with a space. Any occurrence of the literal \n is replaced with a newline.

##### Example
```

> ($$ the quick "brown" fox)

.: "thequickbrownfox"

> ($$ the quick \\s \\s brown fox)

.: "thequick brownfox"

> ($$ {the quick} {} {brown fox})

.: "{the quick}{}{brown fox}"

> ($$ atom \n molecule)

.: "atom

molecule"

> ($$)

.: ""

```

##### Related

$ concatenate, string

## % shell

Executes a shell command.

##### Syntax
```

(% command argument … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| command | literal | 1   | A shell command. |
| argument | Expression | 0+  | An argument to the command |

##### Results

| Taxon | Description |
| --- | --- |
| expression | The output of the command as a list of strings and an integer result. |

##### Remarks

Returns an expression containing a list of strings from the output of the command and an integer result.

##### Example
```

> (% pwd)

.: {"/user/moi"} 0

> (% mkdir tmp)

.: {} 0

> (% ls)

.: {"tmp"} 0

> (% rmdir tmp)

.: {} 0

```

##### Related

files, folders

## & merge

Merges arguments into a new sequence.

##### Syntax
```

(& value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The merged sequence. |

##### Remarks

Returns a flattened sequence merging all subsequences of the same type. If the first element is not a sequence, then a list is treturned. The sequence type shall be that of the first element.

##### Example
```

> (& {1 2 3} 4 5 {6} {7} {8 9} 10)

.: {1 2 3 4 5 6 7 8 9 10}

> (& [1 2 3] 4 5 [6] [7] [8 9] 10)

.: [1 2 3 4 5 6 7 8 9 10]

> (& |1 2 3| |4 5| |6| |7| |8 9| |10|)

.: |1 2 3 4 5 6 7 8 9 10|

> (& {the quick} {} [brown fox])

.: {the quick brown fox}

> (& atom)

.: {atom}

> (&)

.: {}

```

##### Related

&& abridge, mid, insert, pop, push, swap, transfer

## && abridge

Mergs arguments into a new sequences and removes nils.

##### Syntax
```

(&& value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The merged sequence without nils. |

##### Remarks

The && function returns a flattened sequence concatenating all values except nils.

##### Example
```

> (&& {} the quick brown fox {} nil nil jumped)

.: {the quick brown fox jumped}

> (&& [the quick] nil [] nil [brown [fox]])

.: [the quick brown [fox]]

> (&&)

.: {}

> (&& nil nil nil)

.: {}

```

##### Related

& merge, mid, insert, pop, push, swap, transfer

## \* multiplication

Multiply.

##### Syntax
```

(\* number number … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 2+  | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The product of all factors or a list of products. |

##### Remarks

Returns the product of the arguments. If an argument is a list, then each element of the list is multiplied. If a scalar and a list are multiplied, then the scalar is multiplied with each element of the list. All lists must be of the same length.

##### Example
```

> (\* 1 2 3)

.: 6

> (\* {1 2 3} 5 {2 4 6})

.: {10 40 90}

```

##### Related

/ division, % modulo, + addition, - subtraction, \*\* exponent_

## \*\* exponentiation

Raises a base number to an exponent.

##### Syntax
```

(\*\* root exponent)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| root | variant | 1   | A number or list of numbers. |
| exponent | variant | 1   | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The root raised to the indicated power or list of the same. |

##### Remarks

If (\*\* root exponent ) = number , and (/ 1 exponent) = degree then (// number degree) = root_. If no denominator is specified, this function returns the square root of the number..

##### Example
```

> (\*\* 2 3)

.: 8

> (\*\* (e) 2)

.: 7.3890461484

> (\*\* {2 4 6} 2)

.: {4 16 36}

> (\*\* 2 {2 3 4})

.: {4 8 16}

> (\*\* {2 3 4} {2 3 4})

.: {4 27 256}

> (\*\* 4 0.5)

.: 2

```

##### Related

\* multiplication, / division, root

## / division

Division.

##### Syntax
```

(/ dividend divisor … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number or list of numbers. |
| divisor | .aogalk | 0+  | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the quotient of the numbers or a list of quotients. |

##### Remarks

Returns the quotient of the values. If there is one value presented, this function returns the reciprocal of the value. If there are two values, it divides the first value by the second. If there are more than two values, it divides the result by each successive number. Division by zero shall result in the literal unknown being returned. All list arguments must be the same length. If an argument is a list, then each element of the list is divided. If a scalar and a list are divided, then the scalar is divided by each element of the list.

##### Example
```

> (/ 5.0 2)

.: 2.5

> {/ {4 5 6} 4.0)

.: {1 1.25 1.5}

> (/ {4 5 6} {1.0 2.0 3.0})

.: {4 2.5 2}

> (/ 5 0)

.: undefined

```

##### Related

// safe divide, \* multiplication, + addition, - subtraction, % modulo

## // nth root

Returns the n_th root of a number.

##### Syntax
```

(// number degree)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| degree | number | 0-1 | A number (Default is 2) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The root. |

##### Remarks

If (\*\* root exponent ) = number , and (/ 1 exponent) = degree then (// number degree) = root_. If no denominator is specified, this function returns the square root of the number.

##### Example
```

(// 866020)

.: 930.6019557254326

(// 9)

.: 3

(// 8 3)

.: 2

(// 27 3)

.: 3

```

##### Related

\*\* exponentiation, log

## // safe divide

Performs division or returns a default value in case of an undefined result.

##### Syntax
```

##### Syntax

(// dividend divisor default)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number.or a list. |
| divisor | variant | 1   | A number.or a list. |
| default | variant | 0-1 | A number or a list. If not supplied, unknown is returned. |

##### Results

| Taxon | Description |
| --- | --- |
| number | Returns either the quotient of the numerator and denominators or the default. |

##### Remarks

Returns the quotient of the values or the default. It divides the dividend by the divisor. If the default is not supplied, undefined is returned. All list arguments must be the same length. If an argument is a list, then each element of the list is divided. If a scalar and a list are divided, then the scalar is divided by each element of the list.

##### Example
```

> (// 1.0 2)

.: 0.5

> (// 5 0 0)

.: 0

> {// {4 5 6} 0)

.: {undefined undefined undefined}

> {// {4 5 6} {1 2 0} -1)

.: {4 2.5 -1}

```

##### Related

/ division, \* multiplication, + addition, - subtraction, % modulo

## /~ dissimilarity

Calculates the dissimilarity between two values.

##### Syntax
```

(/~ value<sub>1</sub> value<sub>2</sub>)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | Any value |

##### Results

| Taxon | Description |
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

.: 0.73333333333333334

> (/~ "a b c" "a d e")

.: 0.21428571428571425

> (/~ 57 890)

.: 0.9988009592326139

```

##### Related

~ similarity, like, unlike, = equal, /= unequal

## /= unequal

Returns true if any values are not equal.

##### Syntax
```

(/= value<sub>1</sub> value<sub>2</sub> … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if all values are not the same |

##### Remarks

Returns true if any values are not the same. Once two values are determined to be equal, the function short circuits and no further processing occurs.

For example (/= 1 2 3 5 3 6). Since 1≠2, we need to keep looking. Since 2≠3, we need to keep looking. Since 3≠5, we need to keep looking. Since 5≠3, we need to keep looking. However, since 3=3 (positions 3 and 5), false can be returned.

In the case of (/= (f ?x) (g ?x) (h ?x)), if f(?x) ≠ g(?x), h(?x) gets called. But, if f(x) = g(x), h(x) does not get called and false is returned.

##### Example
```

> (/= 1 2 3)

.: true

> (/= 1 1 1)

.: false

```

##### Related

\= equal, ~ similarity, /~ dissimilarity_

## ~ similarity

Calculates the similarity between two values.

##### Syntax
```

(~ value<sub>1</sub> value<sub>2</sub>)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | Any value |

##### Results

| Taxon | Description |
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

.: 0.26666666666666666

> (~ "a b c" "a d e")

.: 0.21428571428571425

> (~ 57 890)

.: 0.001199040767386091

```

##### Related

/~ dissimilarity, = equal, /= unequal, like, unlike  

## ' quote

Quotes a variant.

##### Syntax
```

( ' variant )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| variant | variant | 1   | A variant to be quoted |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The value after quoting. |

##### Remarks

The quote character signifies the quote function. All arguments are returned unevaluated.

##### Example
```

> (' foo)

.: foo

> (' (+ 1 2 3))

.: (+ 1 2 3)

> (' "a string")

.: "a string"

> (' (foo))

.: (foo)

> (' (+ 1 , (\* 2 3)))

.: (+ 1 , (\* 2 3))

```

##### Related

\` expand, eval, function, macro, quote, unquote

## \` expand

Expands a variant by substituting values.

##### Syntax
```

( \` variant )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| variant | variant | 1   | A variant to be expanded |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The argument after expansion. |

##### Remarks

The backquote character is the expand function. The argument is returned unevaluated unless it is preceded by or contains a comma (and underscore), in which case the value following the comma shall be evaluated in the present scope (or in which case the value following the underscore must evaluate to a list which shall be merged into the existing expression).

##### Example
```

> (\` (+ 1 2 "3"))

.: (+ 1 2 "3")

> (let {?a 1 ?b 2 ?c {3 4 5}} (\` {, ?a , ?b , ?c}))

.: {1 2 {3 4 5}}

> (let {?a 1 ?b 2 ?c {3 4 5}} (\` {, ?a , ?b , ?c}))

.: {1 2 3 4 5}

> (\` (foo))

.: (foo)

> (\` (+ (+ 1 1) ,(\* 2 3)))

.: (+ (+ 1 1) 6)

```

##### Related

' quote, eval, function, macro

## + addition

Addition.

##### Syntax
```

(+ number number . . . )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 2+  | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The sum or a list of sums. |

##### Remarks

Calculates the sum of the values. The values must all be numbers or lists containing numbers. If an argument is a list, then each element of the list is added. If a scalar and a list are added, then the scalar is added to each element of the list. All lists must be the same length.

##### Example
```

> (+ 1 2 3)

.: 6

> (+ 5 {6 7 8 9 10})

.: {11 12 13 14 15}

> (+ {1 2 3} {4 5 6} 8)

.: {13 15 17}

```

##### Related

\- minus, \* multiply, / divide

## ++ increment

Increments a number by 1.

##### Syntax
```

(++ number )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1   | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The incremented number or list of numbers. |

##### Remarks

This function increments the argument by 1. If the argument is a list then each number in the list Is incremented by one.

##### Example
```

> (++ 1)

.: 2

> (++ 100)

.: 101

> (++ {99 -101 0})

.: {100 -100 1}

```

##### Related

\-- decrement

## <-- before tie

The value before tying a symbol to a new value.

##### Syntax
```

(<-- function symbol value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 1   | A function |
| symbol | symbol | 1   | A symbol |
| value | value | 0+  | A value used in the function call. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the value bound to the symbol before the function is applied. |

##### Remarks

None

##### Example
```

> (let ?n 0)

.: true

> (<-- + ?n 7)

.: 0

> ?n

.: 7

```

##### Related

\--> after tie, assume, assign, global, local, put, set, swap, tie

## < less

True if each value is less than the next.

##### Syntax
```

(< value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if values are increasing. |

##### Remarks

Returns true if each value is less than its successor from left to right, and false otherwise. All values must be of the same type (either a literal, number, or string)

##### Example
```

(< a b c)

.: true

(< "johnny" "ralph" "sam")

.: true

(< 3 6 2 8)

.: false

(< Amanda Samantha Zelda)

.: true

```

##### Related

&lt;= less or equal, &gt; greater, >= greater or equal , = equal , /= unequal

## <= less or equal

True if each value is less or equal to the next.

##### Syntax
```

(<= value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if values are increasing. |

##### Remarks

Returns true if each value is less than its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings.

##### Example
```

> (<= a b b c)

.: true

> (<= "johnny" "ralph" "sam")

.: true

> (<= 3 6 2 8)

.: false

```

##### Related

< less, > greater, >= greater or equal , = equal , /= unequal

## <== before put

The value before replacement.

##### Syntax
```

(<== container function place value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment. |
| function | function | 1   | A function |
| place | variant | 1   | A key or position. |
| value | value | 0+  | a value used in the function call. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the new place value |

##### Remarks

None

##### Example
```

> (relation Q :X 0)

.: Q

> (global ?Q (new Q))

.: true

> (<== ?Q + :X 1)

.: 0

> (<== ?Q ++ :X)

.: 1

> (:X ?Q)

.: 2

```

##### Related

\==> after put

## \= equal

True if each value is equal to the next.

##### Syntax
```

(\= value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are the same |

##### Remarks

Returns true if each value is the same as its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are = if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical).

##### Example
```

> (= a a a a)

.: true

> (= "johnny" "ralph" "sam")

.: false

> (= 3 3)

.: true

```

##### Related

< less , <= less or equal, > greater, >= greater or equal, /= unequal, identical

## \==> after put

The value after replacement.

##### Syntax
```

(\==> container function place value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment. |
| function | function | 1   | A function |
| place | variant | 1   | A key or position. |
| value | value | 0+  | a value used in the function call. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the new place value |

##### Remarks

None

##### Example
```

> (relation Q :X 0)

.: Q

> (global ?Q (new Q))

.: true

> (==> ?Q + :X 1)

.: 1

> (==> ?Q ++ :X)

.: 2

> (:X ?Q)

.: 2

```

##### Related

<== before put

## > greater

True if each value is greater than the next.

##### Syntax
```

(> value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | value | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if values are decreasing. |

##### Remarks

Returns true if each value is greater than its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings.

##### Example
```

> (> c b a)

.: true

> (> "johnny" "ralph" "sam")

.: false

> (> 3 6 2 8)

.: false

```

##### Related

< less , <= less or equal, >= greater or equal , = equal , /= unequal

## \--> after tie

The value after tying a symbol to a new value.

##### Syntax
```

(\--> function symbol value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 1   | A function |
| symbol | symbol | 1   | A symbol |
| value | value | 0+  | A value used in the function call. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last value bound to the symbol. |

##### Remarks

None

##### Example
```

> (let {?length 0}

(for ?m in (modules)

(--> + ?length (# ?m))))

.: 23

> (# (reduce (modules) $))

.: 23

```

##### Related

<-- before tie, constant, dynamic, global, local, put, set, swap, tie, use

## \>= greater or equal

True if each value is greater or equal to the next.

##### Syntax
```

(\>= value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | value | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if values are increasing. |

##### Remarks

Returns true if each value is greater or equal to its successor from left to right, and false otherwise. All values must be of the same type, and must be numbers, literals, or strings.

##### Example
```

> (>= c b a)

.: true

> (>= "johnny" "ralph" "sam")

.: false

> (>= "sam" "ralph" "johnny")

.: true

> (>= 8 7 6 3)

.: true

```

##### Related

< less , <= less or equal, > greater, = equal , /= unequal

## \n newline

Returns a string containing one or more new lines.

##### Syntax
```

(\n quantity)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| quantity | number | 0-1 | The number of new lines to create. Default is 1. |

##### Results

| Taxon | Description |
| --- | --- |
| string | A string containing a single new line character. |

##### Remarks

None.

##### Example
```

> (\n)

.: "

"

> (\n 3)

.: "

"

```

##### Related

$ concatenate, $$ elide, \\s space, string

## \\s space

Returns a string containing one or more spaces.

##### Syntax
```

(\\s quantity)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| quantity | number | 0-1 | The number of spaces to create. Default is 1. |

##### Results

| Taxon | Description |
| --- | --- |
| string | A string containing a single space. |

##### Remarks

None.

##### Example
```

> (\\s)

.: " "

> (\\s 15)

.: " "

```

##### Related

$ concatenate, $$ elide, \n newline, string

## ^ thought id

Returns a thought identifier.

##### Syntax
```

(^ thought)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| thought | variant | 1   | A SubThought Premise or thought identifier |

##### Results

| Taxon | Description |
| --- | --- |
| thought | Returns the thought identifier. |

##### Remarks

Returns the identifier for a thought.

##### Example
```

> (relation A :S1 0 :S2 1)

.: A

> (new A)

.: A_1

> (premise A_1)

.: [A ^ A_1 :S1 0 :S2 1]

> (^ (premise A_1))

.: A_1

> (^ A_1)

.: A_1

> (^ FOO)

.: nil

```

##### Related

id, instantiate, premise, type

## abolish

Deletes symbols from an environment.

##### Syntax
```

(abolish smybols environment )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbols | variant | 1   | A symbol or a list of symbols. |
| environment | environment | 0-1 | The environment containing the symbol(s). |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns the literal abolished. |

##### Remarks

Disassociates the symbol or symbols from their respective values in the specified environment. If unspecified, each symbol is sought in the current scope or an ancestor environment, all the way up to the global environment. If the symbol is found, it is disassociated, then deleted. If the symbol is not found, it is ignored..

##### Example
```

> (assign ?person DrWho)

.: DrWho

> ?person

.: DrWho

> (abolish ?person)

.: abolished

> ?person

.: [Failure :Name UnboundSymbol :Text "The symbol ?person is unbound"]

```

##### Related

<-- before tie, --> after tie, assign, assume, constant, dynamic, given, global, local, only, presume

## abort

Forcibly terminates one or more tasks.

##### Syntax
```

(abort tasks )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| tasks | variant | 1   | A single task resource or a list of task resources. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the tasks or list of tasks. |

##### Remarks

Immediately terminates an executing task.

##### Example
```

> (concurrent (step ?i from 1 to 100000 (if (cancelled-p (self)) (break oops)) finished)

(step ?i from 1 to 100000 finished))

.: {Task-57 Task-58}

> (cancel task-57)

.: task-57

> (await task-57)

.: oops

> (abort task-58)

.: task-58

> (free {task-57 task-58})

.: freed

```

##### Related

await, cancel, cancelled-p, complete, critical, do, done-p, reclaim , start, task, task-p, tasks

## about

Provides system and version information.

##### Syntax
```

(about)

```
##### Module

KB

##### Parameters

None

##### Results

None

##### Remarks

Returns system and version information.

##### Example
```

> (about)

.: [Premise :Version 1.1.0 :Build 20200430.001 :OS Win64 :Edition Community]

```

##### Related

bye, eval, quote

## abs

Returns the absolute value.

##### Syntax
```

(abs number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | variant | 1   | A number or a list. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | A non-negative number or a list of non-negative numbers. |

##### Remarks

Returns a non-negative number or a list of non-negative numbers. If the number is negative it is multiplied by -1. If the number is positive no change occurs.

##### Example
```

> (abs 100)

.: 100

> (abs -100)

.: 100

> (abs ninfinity)

.: ninfinity

> (abs unkown)

.: unknown

> (abs {0 -2 -99 24 56 infinity})

.: {0 2 99 24 56 infinity}

```

##### Related

\- subtraction , + addition , % modulo, / division, \* multiplication

## absent

True if a file, folder, or url does not exist.

##### Syntax
```

(absent url )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the url does not exist. |

##### Remarks

This function checks whether or not the url exists.

##### Example
```

> (let ?url (ul path "quick.txt"))

.: true

> (if (absent ?url)

(let ?file (file url ?url seek 1 mode write erase yes))

(write ?file "The quick brown fox")

(close ?file))

.: closed

```

##### Related

file, folder, there, url

## acosecant

Returns the inverse cosecant.

##### Syntax
```

(acosecant number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The inverse cosecant of the number. |

##### Remarks

##### Example
```

> (acosecant 0.3927)

.: 1.570796326-1.58686085i

> (acosecant 0.3927 cir radians)

.: 1.570796326-1.58686085i

> (acosecant 135 cir degrees)

.: 0.438313704

> (acosecant (pi) hyp radians)

.: 0.31316588045

> (acosecant 45 hyp degrees)

.: 1.06202877524

```

##### Related

cosine, tangent

## acosine

Returns the inverse cosine.

##### Syntax
```

(acosine number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The inverse cosine of the number. |

##### Remarks

None.

##### Example
```

> (acosine 1.570796326794)

.: 0+1.0322747855i

> (acosine cir 1.570796326794 radians)

.: 0+1.0322747855i

> (acosine cir 22.5 degrees)

.: 1.1672317198

> (acosine hyp 4.712388980384 radians)

.: 2.23188925305

> (acosine hyp 90 degrees)

.: 0.9136433572987  


```

##### Related

cosine, tangent

## acotangent

Returns the inverse cotangent.

##### Syntax
```

(acotangent number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The inverse cotangent of the number. |

##### Remarks

##### Example
```

> (acotangent 0.785398163397)

.: 0.905022576

> (acotangent cir 0.785398163397 radians)

.: 0.905022576

> (acotangent cir 180 degrees)

.: 0.3081690711

> (acotangent hyp 2.356194490192 radians)

.: 0.453062565662

> (acotangent hyp 120 degrees)

.: 0.519695325409

```

##### Related

cosine, tangent

## actual

Returns a the underlying symbol referenced by an alias.

##### Syntax
```

(actual alias)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| alias | alias | 1   | A symbol reference |

##### Results

| Taxon | Description |
| --- | --- |
| symbol | Returns the symbol referenced by the alias. |

##### Remarks

The convention for denoting alias symbols is to use two question marks: ??name.

##### Example
```

> (structure ListNode :Val :Next)

.: ListNode

> (function IsPalindrome2 {ListNode ?tail alias ??head}

(ensure ListNode (actual ??head))

(if (null-p ?tail)

(return true)

or (and (IsPalindrome2 (:Next ?tail)) (= (:Val ?tail) (:Val ??head)))

(set ??head (:Next ??head))

(return true)

else (return false)))

.: IsPalindrome2

> (function IsPalindrome {?head}

(ensure ListNode ?head)

(return (IsPalindrome2 ?head (alias ?head))))

.: IsPalindrome

> (IsPalindrome  
(new ListNode :Val a :Next (new ListNode :Val b :Next (new ListNode :Val a))))

.: true

```

##### Related

alias, assume, dynamic, given, global, let, scope, set, tie

## add

Modifies an assortment by adding entries.

##### Syntax
```

(add assortment entry … )

entry ::= key value

entry ::= key

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment or sequence |
| entry | expression | 1+  | A key, or key value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The modified assortment. |

##### Remarks

Collections require only a key for each entry. Assortments require a key and value for each entry.

##### Example
```

> (entries (add (lexicon) a 1 b 2 c 3))

.: {{a 1}{b 2}{c 3}}

> (entries (add (collection) 1 2 3 4 5))

.: {{1 1}{2 2}{3 3}{4 4}{5 5}}

```

##### Related

\# size, cut, deq, enq, get, insert, key, keys, push, put, rip, values, zap

## address

Returns the address of a URL web resource.

##### Syntax
```

(address url)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | URL | 1   | A url web resource. |

##### Results

| Taxon | Description |
| --- | --- |
| string | A valid URL in a string. |

##### Remarks

If no arguments are provided, then this function returns the universal resource locator for the SubSubThought Premise Language interpreter running on the current cell.

##### Example
```

> (address (url))

.: "http://localhost"

> (address (url scheme https))

.: "https://localhost"

> (url scheme https host "www.youtube.com" path "watch" query "v=ja76cnLKSL4")  
<br/>.: Url-3

> (address Url-3)

.: "https://www.youtube.com/watch?v=ja76cnLKSL4"

```

##### Related

url, url-p

## agent

Creates an agent.

##### Syntax
```

(agent job url handler delay )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| job | function | 1   | A niladic function for the agent to repeatedly perform. |
| url | url | 1   | A Universal Resource Locator.. |
| handler | function | 1   | An message handler function. |
| delay | time | 0-1 | The delay between job executions. Default is 1 second. |

##### Results

| Taxon | Description |
| --- | --- |
| agent | The agent task. |

##### Remarks

This function creates an asynchronous agent task that repeatedly performs a job and also processes incoming messages. The message handler function should receive a sender url and a message string.

##### Example
```

> (let ?url (url scheme tcp port 5001))

.: true

> (function reply {url ?sender string ?message} (tell ?sender "OK"))

.: reply

> (function job {} (tell user ($ 1)))

.: job

> (agent job ?url reply 0.5s)

.: Agent-1

> (do (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1))

111111.: freed

```

##### Related

ask, cancel, service, pause, perform, start, tell

## alias

Returns a reference to a symbol.

##### Syntax
```

(alias symbol)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol |

##### Results

| Taxon | Description |
| --- | --- |
| alias | Returns a symbol reference. |

##### Remarks

The convention for denoting alias symbols is to use two question marks: ??name.

##### Example
```

> (structure ListNode :Val :Next)

.: ListNode

> (function IsPalindrome2 {ListNode ?tail alias ??head}

(ensure ListNode (actual ??head))

(if (null-p ?tail)

(return true)

or (and (IsPalindrome2 (:Next ?tail)) (= (:Val ?tail) (:Val ??head)))

(set ??head (:Next ??head))

(return true)

else (return false)))

.: IsPalindrome2

> (function IsPalindrome {?head}

(ensure ListNode ?head)

(return (IsPalindrome2 ?head (alias ?head))))

.: IsPalindrome

> (IsPalindrome  
(new ListNode :Val a :Next (new ListNode :Val b :Next (new ListNode :Val a))))

.: true

```

##### Related

actual, assume, dynamic, given, global, let, scope, set, tie

## align

Returns a sorted list using the provided ordering.

##### Syntax
```

(align sequence ordering)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence of unordered elements. |
| ordering | sequence | 1   | An ordered sequence. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | An ordered sequence. |

##### Remarks

Places items in the sequence in the specified ordering. If items in the sequence do not appear in the ordering, they are appended to the result in the order of appearance.

##### Example
```

> (align {b d c f} {a b c d})

.: {b c d f}

> (align "72qaj8x" "zyx123a")

.: "x2a7qj8"

```

##### Related

insort, sort

## all

True if all relevant knowledge satisfies all the premises.

##### Syntax
```

(all premise … )

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot is unary-predicate

condition ::= slot not value

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| premise | variant | 1+  | A pattern, call, or truth value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are not nil. |

##### Remarks

True if all values are not nil, false otherwise. Evaluates values one at a time. If a vaue is nil then it returns immediately, ignoring remaining values. . If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.  

##### Example
```

> (all one two three)

.: true

> (all a b nil)

.: false

```

##### Related

any, no, nall

## alphabetic-p

True if the first position of a string is alphabetic.

##### Syntax
```

(alphabetic-p value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is a string and the first position is alphabetic. |

##### Remarks

Can be upper case or lower case.

##### Example
```

> (alphabetic-p {a b c})

.: false

> (alphabetic-p "a b c")  


.: true

> (alphabetic-p " a b c")

.: false

> (alphabetic-p 450)

.: false

> (alphabetic-p "450")

.: false

> (alphabetic-p "Hello World.")

.: true

```

##### Related

capitalized-p, letter-p, lowercase-p, uppercase-p

## alphanumeric-p

True if the first position of a string is a number or a letter.

##### Syntax
```

(alphanumeric-p value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is a string and the first position is alphanumeric. |

##### Remarks

True if the first position of the value is an upper or lower case alphabetic character or a digit.

##### Example
```

> (alphanumeric-p {a b c})

.: false

> (alphanumeric-p "a b c")  


.: true

> (alphanumeric-p " a b c")

.: false

> (alphanumeric-p 450)

.: false

> (alphanumeric-p "450")

.: true

```

##### Related

capitalized-p, letter-p, lowercase-p, uppercase-p

## and

Logical conjunction.

##### Syntax
```

(and truth truth … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 2+  | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all arguments are true. |

##### Remarks

Evaluates the values presented one at a time. If any of the values is false, this function returns false immediately, ignoring any remaining values. This function fails if any argument is not truth.

##### Example
```

> (and (is 234 (given {?x} (= (taxon ?x) number)))

(is abc (given {?x} (= (taxon ?x) literal))))

.: true

> (and true true true true false)

.: false

```

##### Related

exists, nand, nil, nor, not, or, xor

## any

True if any relevant knowledge satisfies all the premises.

##### Syntax
```

(any premise … )

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot is unary-predicate

condition ::= slot not value

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| premise | variant | 1+  | A pattern, call, or truth value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if any value is not nil. |

##### Remarks

True if any value is not nil. Returns immediately upon encountering the first non-nil value. If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.

##### Example
```

> (any nil nil apple)

.: true

> (any one two three four)

.: true

> (any nil nil)

.: false

```

##### Related

all, default, is, nall, no

## append

Inserts values at the end of a sequence.

##### Syntax
```

(append sequence value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| value | variant | 1+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The modified sequence. |

##### Remarks

Inserts the value into the end of a sequence.

##### Example
```

> (let ?s {})

.: true

> (append ?s a b c)

.: {a b c}

> (append ?s d e f)

.: {a b c d e f}

> ?s

.: {a b c d e f}

```

##### Related

@, add, fix, insert, pop, push, swap

## apply

Applies a function to a list of arguments.

##### Syntax
```

(apply function arguments environment)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | The name of a function to invoke |
| arguments | list | 1   | A list containing actual parameters. |
| environment | environment | 0-1 | An optional environment. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The result from applying the function. |

##### Remarks

Applies the function to the list using the supplied environment, or the current scope if no environment is provided. The function is applied to the entire list and the result is returned.

##### Example
```

> (apply + {1 2 3})

.: 6

> (so (let ?x 9

?s (scope))

(so (let ?x 3)

(apply + {1 2 ?x} ?s)))

.: 12

```

##### Related

count, gather, invoke, map, morph, reduce, supply

## arguments

Returns a list of arguments to a call, or task.

##### Syntax
```

(arguments what )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| what | variant | 1   | A task or call. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of arguments to the task or call. |

##### Remarks

Functions are defined using the function intrinsic function. If the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example
```

> (function {?n} (+ 1 ?n))

.: fn-1

> (function plusN {?n + ?i = 1} (+ ?n ?i))

.: plusN

> (function addAll {& ?nums} (apply + ?nums))

.: addAll

> (fn-1 100)

.: 101

> (plusN 100)

.: 101

> (function tryParseNum {?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

> (tryParseNum "foo")

.: {false nil}

> (tryParseNum "123")

.: {true 123}

> (function dont {{try ?what} + {at ?where = nil}}

(apply (given {?s}(tell user ?s))

($ don't try ?what (unless (any ?where) "" ($ at ?where))))

.: dont

> (dont try "skydiving into a volcano")

don't try skydiving into a volcano

.: told

> (dont try this at home)

don't try this at home

.: told

```

##### Related

arguments, call, function, task, parameters

## arity

Returns the number of symbols in a function's parameter list.

##### Syntax
```

(arity function kind)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function or function name . |
| kind | literal | 0-1 | One of required, optional, variadic, or all (default). |

##### Results

| Taxon | Description |
| --- | --- |
| integer | Returns the number of symbols matching the parameter kind. |

##### Remarks

None

##### Example
```

> (function foo {?a + ?b ?c & ?d}

(tell user ($ (&& ?a ?b ?c ?d))))

.: foo

> (arity foo)

.: 4

> (arity foo required)

.: 1

> (arity foo optional)

.: 2

> (arity foo variadic)

.: 1

```

##### Related

has, in, member, within

## array

Returns a multi dimensional list.

##### Syntax
```

(array dimensions option)

dimensions ::= size

dimensions ::= { size …}

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dimensions | variant | 1   | A number or list of numbers for each dimension |
| option | expression | 1   | A key value pair, either of expression (default), or each function. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list. |

##### Remarks

If option is of then all elements of the list are initialized to the same value. If option is each, during initialization, the function receives the current coordinate and the value is used for the position.

##### Example
```

> (array 5)

.: {nil nil nil nil nil}

> (array 5 of 0)

.: {0 0 0 0 0}

> (array 5 each (given {?x}(random 0 to 9))

.: {7 5 8 2 4}

> (array {2 2} each (given {?coordinate}(reduce ?coordinate +)))

.: {{2 3}{3 4}}

```

##### Related

@, bind, edit, make

## asecant

Returns the inverse secant.

##### Syntax
```

(asecant number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The inverse secant of the number. |

##### Remarks

##### Example
```

> (asecant 2.356194490192)

.: 1.13248262224

> (asecant cir 2.356194490192 radians)

.: 1.13248262224

> (asecant cir 120 degrees)

.: 1.0730291831

> (asecant hyp 0.3927 radians)

.: 1.58686

> (asecant hyp 45 degrees)

.: 0.72336752453

```

##### Related

cosecant, secant

## asine

Returns the inverse sine.

##### Syntax
```

(asine number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The inverse sine of the number. |

##### Remarks

##### Example
```

> (asine 0.3927)

.: 0.403566

> (asine cir 0.3927 radians)

.: 0.403566

> (asine cir 95 degrees)

.: 1.570796326+1.092133189i

> (asine hyp 3.141592653589 radians)

.: 1.862295743311

> (asine hyp 120 degrees)

.: 1.4850704719

```

##### Related

cosine, sine

## ask

Sends a message to a recipient and awaits a response.

##### Syntax
```

(ask who message option ... )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| who | literal | 1   | A URL or the literal user for the console. |
| message | string | 0-1 | A message or query. |
| option | expression | 0+  | Key value pairs timeout instant – delay before terminating request,  <br>default value – value to return upon timeout, columns list – a column list is the first record,  <br>if omitted then no columns are listed. (default). skip number – skips a number of records limit number – number of records or #. (default is 1).  <br>meta where – either before or within. (default is before). |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The response. The value nil is returned if no response was given. |

##### Remarks

Sends a message to the recipient and waits for a response. If user is specified for who, then the input is taken from the console. If the url is a data url, then this function retrieves query results from the data url. If the option columns is provided along with a list of columns, and the option meta is provided along with a location (before or within) then each column name is inserted either in the list element before the data, or within each data list.

##### Example
```

> (ask user "What is your name?")

What is your name? Michael

.: "Michael"

> (service (url scheme tcp port 5950)

(function reply {?sender ?message}

(tell ?sender ($ received ?message))))

.: Service-1

> (start Service-1)

.: Service-1

> (ask (url scheme tcp port 5950) "secret" timeout 5s default NobodyHome)

.: "received secret"

> (assign ?data (data driver sqlserver server "//servername" port 1433

database mydata user "myUid" password "123456")

.: Data-1

> (open ?data)

.: Data-1

> (ask Data-1 "select top 10 empid, name, salary from employee" record values)

.: {{1 "John Smith" 10.50}{2 "Jane Johnson" 12.00} …}

> (ask ?data

"select empid, name, wage from employee limit 2”

columns {empid name wage}

limit 2)

.: {{empid name wage} {1 "John Smith" 10.50} {2 "Jane Johnson" 12}}

> (ask ?data "select empid, name, wage from employee" limit 2)

.: {{1 "John Smith" 10.50}{2 "Jane Johnson" 12}}

> (ask ?data "select top 2 empid, name, wage from employee" meta within

columns {:Id :Name :Rate})

.: {{:Id 1 :Name "John Smith" :Rate 10.50}

{:Id 2 :Name "Jane Johnson" :Rate 12}}

> (ask ?data "select top 2 empid, name, wage from employee"  
columns {:Id :Name :Rate} meta before)

.: {{:Id :Name :Rate} {1 "John Smith" 10.50} {2 "Jane Johnson" 12}}

> (close ?data)

.: Data-1

```

##### Related

cancel, free, Service, start, tell

## assert

Adds premises to the knowledge base

##### Syntax
```

(assert premise … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| premise | premise | 1+ | an ephemeron or thought premises |


##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list of ephemerons or thoughts. |

##### Remarks

Each thought premise is added to the knowledge base.


##### Example
```

> (use (conceive)  
    (let ?parent (unique Parent) ?Sibling (unique Sibling))
    (relation ?parent :Who :Child)
	(relation ?sibling :Who :Sibling)
	
	(let ?people 
	  (assert
	     [?parent :Who John :Child Mary]
	     [?parent :Who John :Child Jane]
	     [?sibling :Who Jane :Sibling Mary]))

    (append ?people
      (knew ?sibling :Who Mary :Sibling Jane))
	  
    (for ?p in ?people (tell user ($ (premise ?p) \n)))
	
    (old ?people))

[Parent1 :Who John :Child Mary]
[Parent1 :Who John :Child Jane]
[Sibling1 :Who Jane :Sibling Mary]
[Sibling1 :Who Mary :Sibling Jane]
.: 4


```

##### Related

assume, suppose, old, new 

## assign

Adds symbols in tandem to the current environment.

##### Syntax
```

(assign assignment ... )

assignment ::= symbol value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| binding | expression | 1+  | A symbol and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last assigned value. |

##### Remarks

Sequentially creates symbols in the current environment. Each symbol shall replace any extant symbol with the same name in the environment. Returns the value of the last assignment.

##### Example
```

> (assign ?person DrWho)

.: DrWho

> ?person

.: DrWho

```

##### Related

<-- before tie, --> after tie, assume, constant, dynamic, given, global, local, presume

## assume

Adds premises to the knowledge base

##### Syntax
```

(assume premise … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| premise | premise | 1+ | an ephemeron or thought premises |


##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true |

##### Remarks

Each thought premise is added to the knowledge base.

##### Example
```

> (use (conceive)  
    (let ?parent (unique Parent) ?Sibling (unique Sibling))
    (relation ?parent :Who :Child)
	(relation ?sibling :Who :Sibling)
	
	(assume 
	   [?parent :Who John :Child Mary]
	   [?parent :Who John :Child Jane]
	   [?sibling :Who Jane :Sibling Mary])

    (let ?people (& (which ?parent) (which ?sibling)))
	
    (append ?people
      (knew ?sibling :Who Mary :Sibling Jane))
	  
    (for ?p in ?people (tell user ($ (premise ?p) \n)))
	
    (old ?people))

[Parent1 :Who John :Child Mary]
[Parent1 :Who John :Child Jane]
[Sibling1 :Who Jane :Sibling Mary]
[Sibling1 :Who Mary :Sibling Jane]
.: 4


```

##### Related

assert, suppose, old, new 

## atangent

Returns the inverse tangent.

##### Syntax
```

(atangent number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The inverse tangent of the number. |

##### Remarks

None.

##### Example
```

> (atangent 2.356194490192)

.: 1.4691228248

> (atangent 2.356194490192 cir radians)

.: 1.4691228248

> (atangent 120 cir degrees)

.: 1.12533883288

> (atangent 0.785398163397 hyp radians)

.: 1.05930617082

> (atangent 85 hyp degrees)

.: 0.8181615399-1.5707963267i

```

##### Related

tangent

## attach

Registers a knowledge base.

##### Syntax
```

(attach knowledege)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base |

##### Results

| Taxon | Description |
| --- | --- |
| knowledge | The opened knowledge base. |

##### Remarks

Enables lookup and modification of a knowledge base.

##### Example
```

> (assign ?kb (knowledge url "file:///c:/premise/kb/defultKb.mdb"))

.: Knowledge-1

> (attach ?kb)

.: Knowledge-1

> (relation Fact :All :Are)

.: Fact

> (detach ?kb)

.: Knowledge-1

> (free (cede (alias ?kb)))

.: freed

```

##### Related

conceive, detach, each, eradicate, get, knowledge, knowing, put, using, which, with

## average

The arithmetic mean of a sequence.

##### Syntax
```

(average symbol … binding sequence expression … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 1   | The literal in or per. |
| sequence | sequence | 1   | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result of applying the plus function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the symbols then the function fails. The last expression shall be evaluated and the average function shall be applied to both that expression and any prior result. The final value returned is the sum of all expressions divided by the length of the sequence.

##### Example
```

> (average ?x in (range 1 to 4) ?x)

.: 2.5

> (average ?fruit ?count per {{apple 1}{pear 2}{banana 3}{coconut 4}} ?count)

.: 2.5

```

##### Related

fold, product, summation

## avg

The arithmetic mean.

##### Syntax
```

(avg value …)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | An number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The arithmetic mean of all elements in the sequence. |

##### Remarks

Returns the arithmetic mean. If the list or expression is empty, it returns zero. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared

##### Example
```

> (avg {1 2 3 4 5})

.: 3

> (avg {})

.: 0

> (avg 1 2 3 4 5)

.: 3

> (avg {1 2 3} 4 {6 3 2})

.: {3.66667 3 3}

```

##### Related

max, median, min, statistics, sigma, sum

## await

Returns the result of a task.

##### Syntax
```

(await task timeout default)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource |
| timeout | instant | 0-1 | The amount of time to wait for the task. The default is eternity which implies to wait indefinitely |
| default | variant | 0-1 | The value to return once the timeout is reached. If unspecified, then nil is returned. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The task result, or nil. |

##### Remarks

The await function waits for either the timeout duration or the task to complete.

##### Example
```

> (concurrent (repeat 10000000 foo))

.: Task-2

> (await Task-2 100000t timed-out)

.: timed-out

> (await Task-2)

.: foo

```

##### Related

wait, busy-p, complete, do, done-p, free, task, tarry

## before-p

True if an interval finishes before a second interval.

##### Syntax
```

(before-p interval<sub>1</sub> interval<sub>2</sub> tolerance)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if interval1 finishes some time before interval2. |

##### Remarks

None.

##### Example
```

> (before-p 1s~2s 2s~4s)

.: false

> (before-p 1s~5s 6s~8s)

.: true

> (before-p 1s~9s 4s~6s)

.: false

> (before-p 4s~6s 8s~9s)

.: true

> (before-p 4s~6s 6s~9s 1s)

.: false

```

##### Related

during-p, finishes-p, meets-p, overlaps-p, starts-p  

## beginning

Returns the instant an interval begins.

##### Syntax
```

(beginning interval)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval | interval | 1   | An interval |

##### Results

| Taxon | Description |
| --- | --- |
| instant | The beinning value of the interval. |

##### Remarks

None.

##### Example
```

> (beginning 1s~2s)

.: 1s

> (beginning 1s~5s)

.: 1s

> (beginning 4s~6s)

.: 4s

```

##### Related

finishing

## best

Returns the best matching candidates.

##### Syntax
```

(best probe candidates option ... )

option ::= key value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| probe | variant | 1   | The value to compare to the candidates |
| candidates | list | 1   | The candidates to be compared |
| option | expression | 0+  | Key value pairs , where a key is one of: limit - The number of matches to return.  <br>(default is 1) minscore - value below which candidates shall not be considered. Default is ninfinity maxscore – Value above which candidates are acceptable. Default is 1. transform – The literal name of a value transformation function. comparer - The literal name of a comparison function |

##### Results

| Taxon | Description |
| --- | --- |
| list | A sorted list of lists containing candidate - score pairs. |

##### Remarks

Best compares a probe to candidates and returns the best matching candidate(s) with match score(s). It uses the similarity function (~) as the default comparer. If provided, transforms are applied before comparison. Finally, a comparer can accept two values and returns a score representing the degree of similarity where higher means more similar.

##### Example
```

> (best "this" {"there" "that" "though" "thin"})

.: {{"thin" 0.142857}}

> (best 345 (range 1 to 1000000) limit 5 minscore -1 maxscore 1 comparer ~)

.: {{345 1}{344 0.5}{346 0.5}{343 0.333333}{347 0.3333333}}

```

##### Related

~ similarity, /~ dissimilarity

## beyond

True if a position is outside a sequence.

##### Syntax
```

(beyond sequence position )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| position | variant | 1   | A number or coordinate (i.e. a list of numbers). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the position is not in the sequence, false otherwise. |

##### Remarks

None.

##### Example
```

> (beyond "not empty" 5)

.: false

> (beyond {not empty} 1)

.: false

> (beyond "" 1)

.: true

> (beyond {{a b}{c d}{e f}} {3 2})

.: false

> (beyond {{a b}{c d}{e f}} {7 4})

.: true

```

##### Related

@ element, length, void, more, within

## big

Converts a value to a big number.

##### Syntax
```

(big value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Taxon | Description |
| --- | --- |
| monadic | An monadic number. |

##### Remarks

A big number is bounded by memory. if the value cannot be converted to a big number, the function fails. The fractional part of the number is truncated. A suffix b denotes a big number.

##### Example
```

> (big {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (big "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not a number."]

> (big 500.3)

.: 500b

> (big "23.4")

.: 23b

> (big "2982039842304982039842187591823741209250293823978298234187235897234234237429387903984203948203984209813719875209856087197129871")

.: 2982039842304982039842187591823741209250293823978298234187235897234234237429387903984203948203984209813719875209856087197129871b

```

##### Related

ceiling, complex, floor, integer, long, radix, rational, real, round, truncate, unsigned

## bind

Assigns symbols to values in sequences or assortments.

##### Syntax
```

(bind container assignment … )

assignment ::= slot variable

assignment ::= function variable

assignment ::= position variable

assignment ::= {slot … } as variable

assignment ::= {function … } as variable

assignment ::= {position … } as variable

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment |
| assignment | expression | 1+  | A key symbol, or position symbol, or list symbol pair. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

The key may be a position, function, slot, method, list of functions, or other value.

##### Example
```

> (relation Node :Data :Next)

.: Node

> (new Node :Data C :Next (new Node :Data B :Next (new Node :Data A)))

.: Node_3

> (bind Node_3 :Data ?last {:Next :Next :Data} ?first)

.: true

> (bind {a b {c {d e}}} 1 ?a {3 2 2} ?e (given {?x} (uppercase ($ (@ ?x)))) ?a)

.: true

```

##### Related

dynamic, given, global, scope, set, tie

## bindings

Returns a list of symbol value pairs for a pattern.

##### Syntax
```

(bindings pattern option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| pattern | variant | 1   | A premise or pattern |
| option | expression | 0+  | An option for retrieving the bindings. limit n - the number of results to return. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of all symbol value pairs |

##### Remarks

Returns a series containing binding lists that match the pattern. If no symbols are in the pattern, then a premise is returned for each match and nil is specified for the symbol.

##### Example
```

> (relation Poll :Response)

.: Poll

> (step ?i from 1 to 1000

(new Poll :Response (on (> (radom 0 to 1) 0) Yes No)))

.: Poll_1000

> (for ?bindings in (bindings [Poll :Respones as ?response] limit 5)

(tell user ($ ?bindings))

{?response yes} {?response no} {?response yes} {?response no} {?response no}

.: told

> (for ?bindings in (bindings [Poll :Respones yes] limit 4)

(tell user ($ ?bindings))

{nil [Poll ^ Poll_1 :Response yes]} {nil [Poll ^ Poll_3 :Response yes]}

{nil [Poll ^ Poll_8 :Response yes]} {nil [Poll ^ Poll_9 :Response yes]}

.: told

```

##### Related

tally, using, which, with

## bion

Returns a resource that hosts a cluster of cells for doing tasks.

##### Syntax
```

(bion name work )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | string | 0-1 | The name of the bion |
| work | string | 0-1 | The work to be done. |

##### Results

| Taxon | Description |
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

.: main

> (main)

Hello World

.: freed

```

##### Related

cell, halt, start, task

## bitwise

Performs bitwise operations.

##### Syntax
```

(bitwise number op … )

op ::= operation number

op ::= not

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| op  | expression | 1+  | an operation or operation value pair where the operation is either and, or, not, nand, nor, xor, <<, \>>, or count and where the value is a number y such that: and y – performs logical and or y – performs logical or not – performs complement nand y – performs logical nand nor y – performs logical nor xor y – performs exclusive or xnor y – performs exclusive or << y – performs left shift of x for y iterations \>> y – performs right shift of x for y iterations count y – returns the number of bits that = y (where y is either 1 or 0) |

##### Results

| Taxon | Description |
| --- | --- |
| number | Result depends on the operation. |

##### Remarks

Each operation is performed in succession and the final result is returned.

##### Example
```

> (bitwise 2 and 3)

.: 2

> (bitwise 31 or 14)

.: 31

> (unsigned (bitwise 31 or 14 and 2))

.: 2

> (function countOneBits {?a}

(bitwise ?a count 1))

.: countOneBits

> (countOneBits 255)

.: 8

> (bitwise 31 xor 14 count 1)

.: 2

> (function countConversionBits {?a ?b}

(bitwise ?a xor ?b count 1))

.: countConversonBits

```

##### Related

\+ plus, - minus, unsigned

## bound

Returns the symbols that are bound in a function.

##### Syntax
```

(bound function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | variant | 1   | A function. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of symbols. |

##### Remarks

None.

##### Example
```

> (function foo {?x ?y + ?z}

(bar ?x ?y)

(baz ?z ?a))

.: foo

> (bound foo)

.: {?x ?y ?z}

> (unbound foo)

.: {?a}

> (bound (' (given {?s} (@ ?s ?p))))

.: {?s}

> (unbound (' (given {?s} (@ ?s ?p))))

.: {?p}

```

##### Related

unbound

## bound-p

True if a symbol has a value.

##### Syntax
```

(bound-p symbol)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol. |

##### Results

| Taxon | Description |
| --- | --- |
| bool | True if the symbol is bound. |

##### Remarks

None.

##### Example
```

> (let ?a 1 ?b 2)

.: true

> (bound-p ?a)

.: true

> (bound-p ?b)

.: true

> (bound-p ?c)

.: false

```

##### Related

unbound-p

## bracket

Returns 1 if a truth expression is true, 0 if false, and -1 if unknown.

##### Syntax
```

(bracket truth)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 1   | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| integer | Returns 1 if the truth value is true, 0 if false, and -1 if unknown.. |

##### Remarks

None.

##### Example
```

> (bracket true)

.: 1

> (bracket false)

.: 0

> (bracket banana)

.: [Failure :Name InvalidType :Text "A truth was expected instead of banana."]

> (bracket unknown)

.: -1

```

##### Related

all, any, convert, every, nall, nevery, no, none, some,

## break

Terminates a loop.

##### Syntax
```

(break value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | Any value to be returned. Default is nil. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the value if provided, otherwise returns nil |

##### Remarks

Exits a loop with a return value or nil if no return value is specified. Can be used for a do loop.

##### Example
```

> (for ?item in (range 1 to 1000000)

(if (= ?item 123456) (break))

done)

.: nil

> (for ?item in (range 1 to 1000000)

(if (= ?item 123456) (break foo))

done)

.: foo

```

##### Related

fail, resume, return, try

## busy-p

True if a task has not completed.

##### Syntax
```

(busy-p task)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the task has not completed |

##### Remarks

Returns true if the task has not completed, false otherwise. The opposite of this function is ready-p.

##### Example
```

> (let ?task (@ (concurrent (idle 100s))))

.: true

> (do (idle 20s)

(if (busy-p ?task)

running

else

(free ?task)))

.: running

```

##### Related

cancel, cancelled-p, wait, await, complete, ready-p, reclaim, tarry, task

## but

Creates a subsequence of all except the last elements.

##### Syntax
```

(but sequence quantity)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |
| quantity | number | 0-1 | The number of elements to omit. Defaults to 1. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The selected sub sequence |

##### Remarks

If quantity is omitted, then all but the last item is returned. This is the opposite of rest.

##### Example
```

> (but {a b c d e f})

.: {a b c d e}

> (but {a b c d e f} 3)

.: {a b c}

> (but "abcde" 2)

.: "abc"

```

##### Related

@ element, last, rest, top

## bye

Terminates the interpreter.

##### Syntax
```

(bye)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
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
```

(call value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| call | The concatenated call. |

##### Remarks

Returns an unevaluated call. Note the call must have at least one value, preferably a literal. Note that an empty call cannot be invoked.

##### Example
```

> (call foo {})

.: (foo {})

> (call tell me "hello world")

.: (tell user "hello world"))

> (call)

.: [Failure :Name ArgumentRequired :Text "A required argument was not supplied."]

> (call given {?x} (+ ?x ?x))

.: (given {?x} (+ ?x ?x))

```

##### Related

$, &, closure, eval, invoke, list, tuple, quote

## can

Evaluates an expression while suppressing failures.

##### Syntax
```

(can expression result error )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | An expression to evaluate. |
| result | alias | 0-1 | A symbol alias. |
| error | alias | 0-1 | A symbol alias |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if no failure occurred;. result and error shall contain respective values |

##### Remarks

If the expression succeeds, the result symbol shall contain the result the evaluated expression and the error symbol shall be nil. If the expression fails, the result shall be nil and the error symbol shall contain the failure.

##### Example
```

> (let ?result nil ?error nil)

.: true

> (can (string x) (alias ?result) (alias ?error))

.: true

> ?result ?error

.: "x" nil

.: (can (integer x) (alias ?result) (alias ?error))

.: false

> ?result ?error

.: nil [Failure :Name TypeConversion :Text "Cannot convert x to Integer."]

```

##### Related

assert, did, ensure, fail, finally, may, try

## cancel

Cooperatively ancels tasks.

##### Syntax
```

(cancel tasks )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| tasks | variant | 1   | A single task resource or a list of task resources. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the tasks or list of tasks. |

##### Remarks

Cancels an executing task. The task shall be signaled to terminate. The task must call cancelled-p to determine whether to terminate, and if so, call exit or return.

##### Example
```

> (concurrent (step ?i from 1 to 100000 (if (cancelled-p (self)) (break oops)) finished)

(step ?i from 1 to 100000 finished))

.: {Task-57 Task-58}

> (cancel task-57)

.: task-57

> (await task-57)

.: oops

> (abort task-58)

.: task-58

> (free {task-57 task-58})

.: freed

```

##### Related

wait, abort, await, cancelled-p, complete, critical, do, done-p, reclaim , start, task, task-p, tasks

## cancelled-p

True if a task has been cancelled.

##### Syntax
```

(cancelled-p task)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the task has been cancelled. |

##### Remarks

The task may be cancelled using the cancel function. The cancel function sets a flag which must be recognized by the running task so that it can cooperatively terminate itself. Therefore all tasks should routinely invoke the cancelled-p function to determine whether they must terminate.

##### Example
```

> (concurrent (step ?i from 1 to infinity

(if (cancelled-p (self)) (break quitting))

finished))

.: {Task-57}

> (idle 5s)

.: ready

> (cancel task-57)

.: cancelled

> (await task-57)

.: quitting

```

##### Related

wait, abort, await, cancel, cancelled-p, complete, do, reclaim, self, task

## canonify

Makes equal values identical.

##### Syntax
```

(canonify value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | A thing.. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The canonified value. |

##### Remarks

Calling canonify with no arguments shall clear the canon of all stored values.

##### Example
```

> (global ?Original "The quick brown fox" ?Clone (clone ?Original))

.: true

> (= ?Original ?Clone)

.: true

> (identical-p ?Original ?Clone)

.: false

> (set ?Original (canonify ?Original) ?Clone (canonify ?Clone))

.: true

> (identical-p ?Original ?Clone)

.: true

```

##### Related

\=, clone, copy, make, identical-p, identity, same

## capitalize

Capitalizes a string.

##### Syntax
```

(capitalize string option )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A string to capitalize |
| option | expression | 0-1 | A key value pair words which\- where which is all or first (default). |

##### Results

| Taxon | Description |
| --- | --- |
| string | The capitalized string |

##### Remarks

Capitalizes the string.

##### Example
```

> (capitalize "the quick brown fox")

.: "The quick brown fox"

> (capitalize "the quick brown fox" words all)

.: "The Quick Brown Fox"

> (capitalize "the quick brown fox" words first)

.: "The quick brown fox"

```

##### Related

lowercase, uppercase

## case

Branches execution based on a value.

##### Syntax
```

(case probe clause … else-clause)

clause ::= of value expression …

clause ::= in {value … } expression …

else-clause ::= else expression …

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| probe | variant | 1   | a value to compare |
| clause | expression | 1+  | Test value and expressions to be evaluated |
| else-clause | expression | 0-1 | A default case and expressions to be evaluated |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last value in the successful clause |

##### Remarks

The first expression is evaluated and its result is matched against the of or in values. The comparison stops as soon as the first match is made. When that happens, the various expressions following the value are evaluated, one at a time. If no of or in expression is matched, then if an else clause exists, the expressions are evaluated, otherwise nil is returned.

##### Example
```

> (global ?Value a)

.: true

> (case ?Value

of b nope

in {c d} nope

else not-found)

.: not-found

```

##### Related

and, if, not, or, unless

## categorize

Returns a list of equivalence sets.

##### Syntax
```

(categorize sequence predicate …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| predicates | function | 1+  | Unary truth predicates. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of sublists each containing elements partitioned by a predicate.. |

##### Remarks

A result sublist is returned for each predicate which determines if each item belongs in the respective equivalence set. If the predicate is true for the item, it is added to the result sublist.

##### Example
```

> (categorize (3 5 2 0 5 8 9} even odd zero)

.: {{even 2 0 8}{odd 3 5 5 9}{zero 0}}

> (categorize "abcdefghijk" (given {?x} (< ?x "e")))

.: {{(given {?x} (< ?x "e")) "a" "b" "c" "d"}}

```

##### Related

partition

## cede

Transfers a value between symbols.

##### Syntax
```

(cede alias )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| alias | alias | 1   | A symbol alias |

##### Results

| Taxon | Description |
| --- | --- |
| variant | the value formerly held by the symbol . |

##### Remarks

Transfers a value from one symbol to another, ensuring only one symbol is pointing to a value.

##### Example
```

> (function matrix+ {??a ??b}

(ensure Alias ??a Alias ??b)

(let ?r (cede ??a))

(traverse ?i into ??b limit (dimensions ?r)

(==> ?r + ?i (@ ??b ?i)) )

(set ??b nil)

(return ?r))

.: matrix+

> (let ?x (array {9000 9000} each (given {?c}(random 0 to 1)))

?y (array {9000 9000} each (given {?c}(random 0 to 1)))

?z (matrix+ (alias ?x)(alias ?y)))

.: true

> (is ?x null-p) (is ?y null-p) (is ?z null-p)

.: true true false

```

##### Related

copy, new, relation

## ceiling

Rounds a number towards positive infinity.

##### Syntax
```

(ceiling number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| number | The next higher positive integer. |

##### Remarks

Returns the next highest positive integer.

##### Example
```

> (ceiling 100.5)

.: 101

> (ceiling -100.5)

.: -100

```

##### Related

floor, round, truncate

## cell

Creates a resource for performing tasks.

##### Syntax
```

(cell bion work )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| bion | bion | 1   | A bion resource. |
| work | string | 0-1 | The work to be done. |

##### Results

| Taxon | Description |
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

.: main

> (main)

Hello World

.: freed

```

##### Related

bion, halt, start, task

## channel

Returns a url to the arguments of a task.

##### Syntax
```

(channel task )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task. |

##### Results

| Taxon | Description |
| --- | --- |
| url | A url. |

##### Remarks

Functions are defined using the function intrinsic function. If the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example
```

> (function {?n} (+ 1 ?n))

.: fn-1

> (function plusN {?n + ?i = 1} (+ ?n ?i))

.: plusN

> (function addAll {& ?nums} (apply + ?nums))

.: addAll

> (fn-1 100)

.: 101

> (plusN 100)

.: 101

> (function tryParseNum {?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

> (tryParseNum "foo")

.: {false nil}

> (tryParseNum "123")

.: {true 123}

> (function dont {{try ?what} + {at ?where = nil}}

(apply (given {?s}(tell user ?s))

($ don't try ?what (unless (any ?where) "" ($ at ?where))))

.: dont

> (dont try "skydiving into a volcano")

don't try skydiving into a volcano

.: told

> (dont try this at home)

don't try this at home

.: told

```

##### Related

arguments, call, function, task, parameters

## char

Converts a Unicode value into a one position string.

##### Syntax
```

(char unicode)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| unicode | variant | 1   | A unicode value between 0 and 65535 or the literal maximum or minimum. |

##### Results

| Taxon | Description |
| --- | --- |
| string | A string containing the character. |

##### Remarks

None.

##### Example
```

> (char 65)

.: "A"

```

##### Related

unicode

## choose

Returns the elements of a sequence that satisfies a function.

##### Syntax
```

(choose sequence selector transform)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence of values. |
| selector | function | 1   | The function to be applied. |
| transform | function | 0-1 | A function that returns a key given a sequence element prior to computing the selector. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of elements satisfying the function. |

##### Remarks

Returns the elements in the sequence that satisfy the function. If the sequence is empty, it returns an empty list. The transform function takes elements of the sequence and returns numbers before computing the function of the transformed sequence.

##### Example
```

> (choose {1 2 3 4 5} max)

.: {5}

> (choose {a b c d e} max)

.: {e}

> (choose {} max)

.: {}

  
> (choose {{a 0}{b 1}{c 2}{d 0}} min (given {?item} (@ ?item 2)))

.: {{a 0}{d 0}}

```

##### Related

max, min, partition

## clear

Eliminates all entries from an assortment or sequence.

##### Syntax
```

(clear container)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |

##### Results

| Taxon | Description |
| --- | --- |
| thing | The modified assortment or sequence. |

##### Remarks

This function clears dynamic assortments and sequences. The clear function shall fail on fixed assortments (i.e. enumerations, records, and prototypes) . For fixed assortments use zap to set slots values to nil.

##### Example
```

> (assign ?s (lexicon a 1 b 2 c 3 d 4) ?list {a b c})

.: {a b c}

> (entries ?s)

.: {{a 1}{b 2}{c 3}{d 4}}

> (entries (clear ?s))

.: {}

> (clear ?list)

.: {}

> ?list

.: {}

```

##### Related

add, includes, item, items, keys, reclaim, #, tie, values

## clip

Returns a value within a clipped range.

##### Syntax
```

(clip number minimum maximum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| minimum | number | 1   | A number (default is ninfinity) |
| maximum | number | 1   | A number (default is infinity) |

##### Results

| Taxon | Description |
| --- | --- |
| number | Returns the number constrained to the range. |

##### Remarks

If the value is greater than the maximum, the maximum is returned. If the value is less than the minimum, the minimum is returned, otherwise the value is returned.

##### Example
```

> (clip 3 0 5)

.: 3

> (clip 7 0 5)

.: 5

> (clip -4 0 5)

.: 0

> (clip 84 ninfinity 100)

.: 84

\>(clip 84 0 infinity)

.: 84

```

##### Related

max, min

## clone

Clones an atom with possible modifications.

##### Syntax
```

(clone atom modification … )

modification ::= key value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| atom | atom | 1   | An atomic value.. |
| modification | expression | 0+  | A key value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| thing | The copy. |

##### Remarks

A duplicate or shallow copy of the original value is made. Zero or more modifications may be specified and applied after the value is cloned. If the value is a thought and the relation has an !onNew method defined, that method is first run on the clone. If an !onClone event method is defined, then the onClone method is invoked thereafter. The clone event (!onClone) requires two parameters {?clone ?original}. To clone sequences use the copy function.

##### Example
```

> (relation Car

:Make :Model :Year :Version 1

!onClone (function Car_clone {?m ?o}(==> ?m ++ :Version (:Version ?o))))

.: Car

> (premise (new Car :Make oole :Model civic :Year 2000))

.: [Car ^ Car_1 :Make oole :Model civic :Version 1 :Year 2000 !onClone Car_clone]

> (premise (clone Vehicle_1 :Year 2016))

.: [Car ^ Car_2 :Make oole :Model civic :Version 2 :Year 2016 !onClone Car_clone]

```

##### Related

copy, new, relation

## close

Closes a file or data url.

##### Syntax
```

(close url)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A file or data url. |

##### Results

| Taxon | Description |
| --- | --- |
| url | The url. |

##### Remarks

Closes an open url.

##### Example
```

> (assign ?file (file name "kwikfox.txt"))

.: File-1

> (open ?file)

.: File-1

> (let ?contents (read ?file #))

.: true

> ?contents

.: "The quick brown fox jumped over the lazy dogs."

> (close ?file)

.: File-1

```

##### Related

close, data, file, open

## closure

Creates a public function in a module.

##### Syntax
```

(closure scope type name parameters expression … )

parameters ::=

parameters ::= { }

parameters ::= {required … }

parameters ::= {required … + optional … }

parameters ::= { \+ optional … }

parameters ::= {required … \+ optional … & remaining }

parameters ::= { & remaining }

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment or module name. |
| type | literal | 1   | The literal function or macro |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing symbols, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

The closure intrinsic defines a function or macro with an explicit scope. a new scope shall be constructed for the function (or macro) using symbols and function definitions contained in the ancestral scopes. If the name is supplied, then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example
```

> (closure (scope) function {?n} (+ 1 ?n))

.: fn-1

> (closure (scope) function plusN {?n + ?i = 1} (+ ?n ?i))

.: plusN

> (fn-1 100)

.: 101

> (plusN 100)

.: 101

> (closure (scope go -1)

function tryParseNum {?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

.: tryParseNum

> (tryParseNum "foo")

.: {false nil}

> (tryParseNum "123")

.: {true 123}

> (closure (scope of User)

macro set2 {?value ?var1 ?var2}

"puts value into two variables in parallel"

(eval (\` (set , ?var1 , ?value , ?var2 , ?value))))

.: set2

> (let ?x1 nil ?x2 nil) ?x1 ?x2

.: true nil nil

(set2 (+ 2 2) ?x1 ?x2)

> ?x1 ?x2

.: 4 4

```

##### Related

arguments, call, extend, function, macro, module, modules, parameters

## coalesce

Returns a merged sequence.

##### Syntax
```

(coalesce symbol … gate expression … )

gate ::= in sequence

gate ::= per sequence

gate ::= from expression … until predicate

gate ::= from expression … while predicate

gate ::= from i limit j by k

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| gate | expression | 1   | One of the gates expressions listed above. where i is the initial value of the symbol, limit is any of to, above, below or go. where j is the final value of the symbol, and k is the optional increment. |
| expression | variant | 1+  | An expression that potentially transforms the iteration variable |

##### Results

| Taxon | Description |
| --- | --- |
| list | A new merged list after the transformation is applied |

##### Remarks

In the case of in or per For each element in the sequence, the element is stored in the symbol, and then the expressions are evaluated. If from is specified, each symbol is bound to the initally evaluated expression. If to is specified, the symbol is assumed to be a number, and the last number is included in the iteration. If below or above is specified the last number is excluded from the iteration. If go is specified, then the j value is the number of iterations. On each iteration the expressions are evaluated, and the last expression is collected into a merged result list.

##### Example
```

> (collect ?n in {1 2 3 4} {(\* ?n 3) (\* ?n 2)})

.: {{3 2}{6 4}{9 6}{12 8}}

> (coalesce ?n from 1 while (<= ?n 4) {(\* ?n 3) (\* ?n 2)}))

.: {3 2 6 4 9 6 12 8}

> (collect ?x ?y per {{1 1}{1 2}{2 5}} {(/ ?x ?y) (\* ?x y)})

.: {{1 1}{0.5 2}{0.4 10}}

> (coalesce ?x ?y per {{1 1}{1 2}{2 5}} {(/ ?x ?y) (\* ?x y)})

.: {1 1 0.5 2 0.4 10}

> (coalesce ?n in {1 2 3 4} {(\* ?n 3)})

.: {3 6 9 12}

> (coalesce ?i from 1 to 9 by 2 {?i})

.: {1 3 5 7 9}

> (coalesce ?n from 1 below 5 {(\* ?n 3)})

.: {3 6 9 12}

> (coalesce ?i from 1 go 4 (pick {a b c d e f g h i j} ?i))

.: {c h b e a c d j c f e b h j c}

```

##### Related

collect, filter, map , reduce, scale

## collect

Returns a transformed sequence.

##### Syntax
```

(collect symbol … gate expression … )

gate ::= in sequence

gate ::= per sequence

gate ::= from expression … until predicate

gate ::= from expression … while predicate

gate ::= from i limit j by k

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| gate | expression | 1   | One of the gates expressions listed above. where i is the initial value of the symbol, limit is any of to, above, below or go. where j is the final value of the symbol, and k is the optional increment. |
| expression | variant | 1+  | An expression that potentially transforms the iteration variable |

##### Results

| Taxon | Description |
| --- | --- |
| list | A new list after the transformation is applied |

##### Remarks

In the case of in or per For each element in the sequence, the element is stored in the symbol, and then the expressions are evaluated. If from is specified, each symbol is bound to the initally evaluated expression. If to is specified, the symbol is assumed to be a number, and the last number is included in the iteration. If below or above is specified the last number is excluded from the iteration. If go is specified, then the j value is the number of iterations. On each iteration the expressions are evaluated, and the last expression is collected into a result list.

##### Example
```

> (collect ?n in {1 2 3 4} (\* ?n 3))

.: {3 6 9 12}

> (collect ?x ?y per {{1 1}{1 2}{2 5}} (/ ?x ?y))

.: {1 0.5 0.4}

> (collect ?i from 1 to 9 by 2 ?i)

.: {1 3 5 7 9}

> (collect ?n from 1 below 5 (\* ?n 3))

.: {3 6 9 12}

> (collect ?i from 1 go 4 (pick {a b c d e f g h i j} ?i))

.: {{c} {h b} {e a c} {d j c f} {e b h j c}}

```

##### Related

coalesce, filter, map , reduce, scale

## collection

Returns an unorderd collection of elements.

##### Syntax
```

(collection element … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| element | variant | 0+  | A key. |

##### Results

| Taxon | Description |
| --- | --- |
| collection | A collection. |

##### Remarks

A collection is an unordered set of elements.

##### Example
```

> (collection

{a b c} "foo" bar 500 [Fruit :Name Apple])

.: Collection-1

> (has Collection-1 foo)

.: false

> (has Collection-1 "foo")

.: true

```

##### Related

enumeration, environment, lexicon

## combine

Creates a new assortment by combining entries.

##### Syntax
```

(combine assortment entry … )

entry ::= key value

entry ::= key

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment or sequence |
| entry | expression | 1+  | A key, or key value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The modified assortment. |

##### Remarks

Collections require only a key for each entry. Assortments require a key and value for each entry.Use the add function to modify an assortment.

##### Example
```

> (entries (add (lexicon) a 1 b 2 c 3))

.: {{a 1}{b 2}{c 3}}

> (entries (add (collection) 1 2 3 4 5))

.: {{1 1}{2 2}{3 3}{4 4}{5 5}}

```

##### Related

add

## common

Creates a sequence of common elements among subsequences.

##### Syntax
```

(common sequences )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequences | sequence | 1   | A sequence containing sequences |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A list of common items |

##### Remarks

Returns the intersection of the subsequences, i.e., the elements common to all subsequences.

##### Example
```

> (common {{1 2 3 4} {2 3 4 5}})

.: {2 3 4}

> (common {{2 3 4 5} {4 5 6 7}})

.: {4 5}

> (common (map {[Data :A {1 2 3 4}] [Data :A {2 3 4 5}]} (given {?d} (:A ?d))))

.: {4}

> (common {"abc" "bcd" "cde"})

.: "c"

```

##### Related

difference, intersection, union

## comparable-p

Returns true if the values can be compared.

##### Syntax
```

(comparable-p value<sub>1</sub> value<sub>2</sub> )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | A value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the values can be compared. |

##### Remarks

Returns true if the values are of the same type and their elements are of the same type, false otherwise.

##### Example
```

(comparable-p 1 2)

.: true

(comparable-p 2 x)

.: false

(comparable-p {1 2 3 4}{2 3 4 5})

.: true

(comparable-p {1 2 3 4}{a b c d})

.: false

(comparable-p b a)

.: true

(comparable-p z {a b c})

.: false

```

##### Related

\= equal, /= unequal

## compare

Returns less, equal, or greater.

##### Syntax
```

(compare value<sub>1</sub> value<sub>2</sub>)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2   | A value |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns < (less than), \= (equals), or > (greater than). |

##### Remarks

Returns the less than literal if the first value is less than the second value, the equal literal if the values are equal, and the greater than literal if the first value is greater than the second value. The function fails if the values are not comparable (i.e., of the same type).

##### Example
```

(compare 1 2)

.: <

(compare 2 1)

.: >

(compare {1 2 3 4}{2 3 4 5})

.: <

(compare a a)

.: =

(compare b a)

.: >

```

##### Related

\= equal, /= unequal

## complete

Runs expressions concurrently.

##### Syntax
```

(complete expression … )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of task resources. |

##### Remarks

Executes the expressions concurrently, and returns after the last expression completes, returning a list of task handles. If expression is not a task, then the expression is converted to a task prior to execution.

##### Example
```

> (complete

(step ?i from 0 to 50000000 (do nothing))

(step ?i from 1 to 10000000 (do something))))

.: {task-1 task-2}

> (free (wait {task-1 task-2}))

.: freed

```

##### Related

abort, await, concurrent, do, busy-p, free, ready-p, start, tarry, task, tasks, wait

## complex

Converts a value to a complex number.

##### Syntax
```

(complex real imaginary)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| real | real | 1   | A number value or the literal minimum or maximum |
| imaginary | imaginary | 1   | A number value or the literal minimum or maximum |

##### Results

| Taxon | Description |
| --- | --- |
| complex | A complex number. |

##### Remarks

If the values cannot be converted to a complex number, the function fails.

##### Example
```

> (complex {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (complex "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not a number."]

> (complex 500 8i)

.: 500+8i

> (complex 500.3 0)

.: 500.3+0i

> (complex "23.4" "0i")

.: 23.4+0i

```

##### Related

ceiling, complex, floor, long, rational, real, round, truncate,

## compose

Applies functions in reverse order using the arguments.

##### Syntax
```

(compose functions arguments)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| functions | list | 1   | A list of functions to be applied in reverse order. |
| arguments | variant | 0-1 | The arguments to the last function in the functions list. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The result of the last call |

##### Remarks

If the arguments parameter is an empty list, the rightmost function is assumed to be niladic (requiring no arguments). The rightmost function is applied to the arguments parameter, then the second from rightmost is applied to the result, and so on, until all functions are applied. The final result is returned. The opposite function is morph. The scatter function applies functions in parallel.

##### Example
```

> (function double {?x} (\* ?x 2))

.: double

> (compose {double ++ ++ ++} {0})

.: 6

> (compose {rest but rest but}

{{the quick brown fox jumped over the lazy dogs}})

.: {brown fox jumped over the}

> (compose {double ++ ++ +} {2 3 4})

.: 22

```

##### Related

apply, map, morph, scatter

## conceive

Creates a knowledge base.

##### Syntax
```

(conceive knowledege)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base |

##### Results

| Taxon | Description |
| --- | --- |
| knowledge | The opened knowledge base. |

##### Remarks

Constructs a new knowledge base if one does not already exist.

##### Example
```

> (conceive (assign ?kb (knowledge name defaultKB path "c://premise/kb/")))

.: defaultKB

> (attach ?kb)

.: defaultKB

> (use ?kb)

.: defaultKB

> (relation Fact :All :Are)

.: Fact

> (detach ?kb)

.: defaultKB

> (free (cede (alias ?kb)))

.: freed

```

##### Related

attach, detach, each, eradicate, get, knowing, knowledge, put, using, which, with

## concurrent

Evaluates expressions asynchronously.

##### Syntax
```

(concurrent expression … )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| list | The executing task resources. |

##### Remarks

If expression is not a task, then the expression is converted to a task. Each taks is then started asynchronous and a list of the executing tasks is returned.

##### Example
```

> (concurrent (+ 1 2 3 4) (/ 1000 57) (\*\* 4 20))

.: {Task-1 Task-2 Task-3}

> (await task-1)

.: 10

> (await task-2)

.: 17.54385964912281

> (await task-3)

.: 1099511627776

> (free task-1 task-2 task-3)

.: nil

> (free (tarry (concurrent (+ 1 2 3 4) (/ 1000 57) (\*\* 4 20))))

.: freed

```

##### Related

await, busy-p, cancel, cancelled-p, conclude, critical, is, free , ready-p, self, tarry, task, tasks, wait

## configuration

Creates a configuration file.

##### Syntax
```

(configuration url association ... )

association ::= section settings

settings ::= { setting setting }

setting ::= key value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url. |
| association | expression | 0+  | A section literal and list of key value pairs. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The value associated with the key. |

##### Remarks

This function creates a configuration file at the specified URL. The file constis of sections that have key value pairs.

##### Example
```

> (configuration "c$/apps/premise/myApp.cfg" security {User John password "foo"}))

.: :Configuration-1

> (get Configuration-1 security password)

.: "foo"

> (put (get Gonfiguration-1 security) password "bar")

.: Lexicon-248

> (get Configuration-1 security password)

.: "bar"

```

##### Related

add, cut, erase, get, put

## confirm

Tests that a condition is true.

##### Syntax
```

(confirm condition since reason)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | The test. If it evaluates to false the function fails |
| since | literal | 0-1 | The literal since. |
| reason | string | 0-1 | The failure text to display. Defaults to "Assertion failure." if not supplied. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if test is true. |

##### Remarks

If the since keyword and reason are omitted, the failure text shall be "Failed condition." The failure name is always "Confirmation" .

##### Example
```

> (confirm (= red blue) since "colors must be the same")

.: [Failure :Name Assertion :Text "colors must be the same"]

> (function reducing {?sequence ?function}

(ensure sequence ?sequence function ?function)

(confirm (> (# ?sequence) 1) since "Two or more elements are required.")

(let ?result (@ ?sequence))

(for ?element in (rest ?sequence) (--> ?function ?result ?element)))

.: reducing

> (reducing {1} +)

.: [Failure :Name Confirmation :Text "Two or more elements are required."]

```

##### Related

confute, ensure, fail, signal, try

## confute

Tests that a condition is false.

##### Syntax
```

(confute condition since reason)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | The test. If it evaluates to false the function fails |
| since | literal | 0-1 | The literal since. |
| reason | string | 0-1 | The failure text to display. Defaults to "Rejection failure." if not supplied. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns false if test is false. |

##### Remarks

If the since keyword and reason are omitted, the failure text shall be "Failed condition." The failure name is always "Confutation." .

##### Example
```

> (confute (= red blue) since "colors must be different")

.: false

> (function reducing {?sequence ?function}

(ensure sequence ?sequence function ?function)

(confute (<= (# ?sequence) 1) since "Two or more elements are required.")

(let ?result (@ ?sequence))

(for ?element in (rest ?sequence) (--> ?function ?result ?element)))

.: reducing

> (reducing {1} +)

.: [Failure :Name Confutation :Text "Two or more elements are required."]

```

##### Related

confirm, ensure, fail, signal, try

## constant

Creates a constant.

##### Syntax
```

(constant assignment … )

assignment ::= symbol value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assignment | expression | 1+  | Symbol and value pairs. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates constant symbols in the current environment. Any attempts to put a different value into the symbol shall create a failure. Calling constant again on the symbols is allowed.

##### Example
```

> (constant ?SECRET "mysecret")

.: true

> ?SECRET

.: "mysecret"

> (constant ?MIN_ENTRIES 300

?MAX_ENTRIES 400)

.: true

> ?MAX_ENTRIES

.: 400

```

##### Related

<-- before tie, --> after tie, global, dynamic, modular, local

## contains

True if a value is present in an assortment.

##### Syntax
```

(contains assortment value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | A sequence or assortment |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the key is present. or false if the key is absent. |

##### Remarks

None

##### Example
```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.: Lexicon-1

> (contains Lexicon-1 3)

.: true

> (contains Lexicon-1 X_foo)

.: true

> (contains Lexicon-1 elephant)

.: false

```

##### Related

has, lacks, missing

## continue

Continues to the next iteration of a loop.

##### Syntax
```

(continue value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | A return value for the next iteration. |

##### Results

| Taxon | Description |
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

.: nil

> (for ?item in (range 1 to 1000000)

(if (< ?item 123456)

(continue)

else

(break foo)))

.: foo

```

##### Related

break, fail, return, try

## convertible-p

True if the value can be converted to the datatype.

##### Syntax
```

(convertible-p value taxon)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | The value to be converted |
| taxon | literal | 1   | The name of the target data type |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the value can be converted to the data type. |

##### Remarks

If the value can be converted converted to the given data type, then this function returns true, otherwise it returns false.

##### Example
```

> (convertible-p {a b c} string)

.: true

> (convertible-p "500" number)

.: true

> (convertible-p "500" literal)

.: false

> (convertible-p "{wxy}" number)

.: false

```

##### Related

datatype, datais, relation-p, type, is

## copy

Copies a sequence.

##### Syntax
```

(copy sequence count )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| count | integer | 0-1 | The number of times to repeat the sequence. Default is 1. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The copied sequence. |

##### Remarks

A shallow copy of the original sequence is made and replicated. All elements of the sequence are repeated the specified number of times.

##### Example
```

> (copy "a" 5)

.: "aaaaa"

> (copy {the quick brown fox} 3)

.: {the quick brown fox the quick brown fox the quick brown fox}

> (copy "hello")

.: "hello"

> (copy ($ hello world \\s) 2)

.: "hello world hello world"

```

##### Related

copy, new, relation

## copyright

Displays copyright information.

##### Syntax
```

(copyright)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| nil | The value nil. |

##### Remarks

Prints copyright information.

##### Example
```

> (copyright)

(c)2014-2020 Michael S P Miller All Rights Reserved

.: nil

```

##### Related

bye, help, license

## correlate

Finds the correlation coefficient of two lists.

##### Syntax
```

(correlate list<sub>1</sub> list<sub>2</sub>)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| list | list | 2   | Lists. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The correlation coefficient. |

##### Remarks

Compares only the number of elements in the shorter of the two lists.

##### Example
```

(correlate {1 2 3 4 5} {4 3 2 1 0})

.: -1

(correlate {1 2 3 4 5} {6 7 8 9 10})

.: 1

(correlate {1 2 3 4 5} {6 3 8 2 10})

.: 0.33071891

```

##### Related

probability, statistics, survey

## cosecant

Returns the cosecant.

##### Syntax
```

(cosecant number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The cosecant of the number. |

##### Remarks

##### Example
```

> (cosecant 0.785398)

.: 1.414213793

> (cosecant cir 0.785398 radians)

.: 1.414213793

> (cosecant cir 45 degrees)

.: 1.4142135623

> (cosecant hyp 1.5708 radians)

.: 0.434535467

> (cosecant hyp 90 degrees)

.: 0.434537208

```

##### Related

asecant, secant

## cosine

Returns the cosine.

##### Syntax
```

(cosine number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The cosine of the number. |

##### Remarks

None.

##### Example
```

> (cosine 0.785398)

.: 0.707106896

> (cosine cir 0.785398 radians)

.: 0.707106896

> (cosine cir 45 degrees)

.: 0.707106896

> (cosine hyp 1.5708 radians)

.: 2.50918693

> (cosine hyp 90 degrees)

.: 2.509178478

```

##### Related

asine, sine

## cotangent

Returns the cotangent.

##### Syntax
```

(cotangent number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The cotangent of the number. |

##### Remarks

##### Example
```

> (cotangent 0)

.: infinity

> (cotangent cir 1.5708 radians)

.: 0

> (cotangent cir 45 degrees)

.: 1

> (cotangent hyp 1.5708 radians)

.: 1.09033

> (cotangent hyp 90 degrees)

.: 1.0903314107

```

##### Related

atangent, tangent

## count

Counts the iterations and returns the last expression.

##### Syntax
```

(count symbol … binding sequence as counter expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A sequence (string or list) |
| as | literal | 1   | The literal as |
| counter | symbol | 1   | A counter variable |
| expression | expression | 0+  | An expression. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last expression in the sequence. |

##### Remarks

None.

##### Example
```

> (count ?word in {the quick brown fox} as ?n

(tell user ($ ?n ?word \n)) ?n)

1 the

2 quick

3 brown

4 fox

.: 4

```

##### Related

collect, exactly, filter, gather, quantify, quantity

## critical

Serializes evaluations across regions of code.

##### Syntax
```

(critical locks option … expression …)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| locks | list | 0-1 | A list of literals representing critical section locks |
| option | expression | 0+  | A key value pair: retries integer - number of times to retry any lock. (default is 0) lockwait time - how long to wait for a lock.  <br>(default is 2,000,000 ticks) within time - the overall time to obtain all locks  <br>(default is1 second) |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The value of the last expression. |

##### Remarks

The critical section is used to serialize the execution of the contained expressions. Any other sections with the same tags shall be blocked. Generates failure if the locks cannot be obtained on the tags under the default or indicated conditions, or if a lock was forcibly released during execution.

##### Example
```

> (function sayHello {}

(critical {printing}

(for ?c in "hello " (tell user ?c))))

.: sayHello

> (free (wait (concurrent (sayHello) (sayHello) (sayHello))))  


hello hello hello .: freed

```

##### Related

release

## cut

Removes elements from assortments by key.

##### Syntax
```

(cut assortment key … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment. |
| key | variant | 0+  | A key. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The modified assortment or sequence. |

##### Remarks

Assortments are modified destructively. To delete nondestructively use the remove function.

##### Example
```

> (entries (collection a b c d))

.: {{a a} {b b} {c c} {d d}}

> (entries (cut (lexicon a 1 b 2 c 3 d 4) b d))

.: {{a 1}{c 3}}

```

##### Related

rip, remove

## data

Creates a data url.

##### Syntax
```

(data option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 1+  | Any key value pair of the following: connect string - use the specified connection string. poolsize poolsize \- maximum # of connections provider platform - either mssql, odbc, maria, pgsql or build the connection string from the following elements. driver name - the driver server address - server address version number - server version class class - class name of driver host address \- host address port port \- server port for database service instance instance \- server instance name integratedSecurity truth \- true or false database name - database name user username - user name password password - user password trusted yesorno - trusted connection yes or no. source name - data source name protocol protocol - database protocol subprotocol subprotocol - database sub protocol subname subname - sub name |

##### Results

| Taxon | Description |
| --- | --- |
| url | A data url. |

##### Remarks

None

##### Example
```

> (open (data driver sqlserver server "//servername" port 1433

database mydata user "myUid" password "123456"))

.: Data-1

> (ask Data-1 "select top 2 empid, name, salary from employee"

format row columns {name wage})

.: {{1 "John Smith" 10.50}{2 "Jane Johnson" 12.00} }

> (close Data-1)

.: Data-1

> (open (data host "localhost" database "sample" user "username"

password "secret" connections 3)))

.: Data-2

> (tell Data-2 "update employee set wage = wage + 1.00;")

.: executed

> (close Data-2)

.: Data-2

> (global ?data

(open (data class "com.microsoft.jdbc.sqlserver.SQLServerDriver"

subprotocol "sqlserver"

subname "//serverName:port;database=db;user=uid;password=pwd")))

.: true

> (function valueslist {?rows}

($ (inside (infix (map (collect ?row in ?rows (inside (infix ?row ,)))

call)

, ))))

.: valuelist

> (tell ?data ($ "insert Employee (name, hours, wage) values "

(valueslist {{"Jane Johnson" 40 10.50}

{"John Smith" 5 10.50}})))

.: 2

> (close ?data)

.: Data-3

```

##### Related

disconnect, tell, fetch, store

## date

Creates a new date or returns the current date.

##### Syntax
```

(date yr mth day hrs mins secs zone zmins)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
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

| Taxon | Description |
| --- | --- |
| date | The UTC date. |

##### Remarks

If no arguments are provided, this function returns the current date in Coordinated Universal Time. Otherwise, it attempts to construct a date from the supplied arguments.

##### Example
```

> (date)

.: 2014-09-16T02:15:51.97152+00:00

> (date 2018 5 18 0 0 0 0 0)

.: 2018-05-18T00:00:00.00000+00:00

```

##### Related

epoch, moment, tick

## declared-p

True if a symbol exists in an environment.

##### Syntax
```

(declared-p symbol environment)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol |
| environment | environment | 0-1 | An environment. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the symbol has been declared. |

##### Remarks

If location is omitted, the symbol is sought in the current environment.

##### Example
```

> (use (module Example))

.: Example

> (modular ?hello World)

.: bar

> (use User)

.: User

> (declared-p ?hello (scope of User))

.: false

> (declared-p ?hello (scope of Example))

.: true

```

##### Related

function-p, symbol-p,

## decode

Decodes a string.

##### Syntax
```

(decode source format)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| source | string | 1   | A string to decode. |
| format | literal | 1   | One of { base16, base32, base64, utf8, none } |

##### Results

| Taxon | Description |
| --- | --- |
| string | The encoded string |

##### Remarks

Each entry in the elements list may be a literal or a list containing a literal and an index.

##### Example
```

> (encode "The quick brown fox" base16)

.: "54686520717569636B2062726F776E20666F78"

> (encode "The quick brown fox" base64)

.: "VGhlIHF1aWNrIGJyb3duIGZveA=="

> (encode "The quick brown fox" none)

.: "The quick brown fox"

> (decode "54686520717569636B2062726F776E20666F78" base16)

.: "The quick brown fox"

> (decode "VGhlIHF1aWNrIGJyb3duIGZveA==" base64)

.: "The quick brown fox"

> (decode "The quick brown fox" none)

.: "The quick brown fox"

```

##### Related

encode

## default

Returns the first non-nil value.

##### Syntax
```

(default value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value to be returned. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The first value that is not nil. |

##### Remarks

Returns the first value which is not nil. If all values are nil, then nil is returned.

##### Example
```

> (default nil 1 2 3)

.: 1

> (default nil a b c)

.: a

> (default nil)

.: nil

> (default nil nil nil nil 1)

.: 1

```

##### Related

any, is , no

## definitions

Retrieves literal value pairs in an environment.

##### Syntax
```

(definitions environment )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| environment | environment | 1   | An environment |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of all symbol value pairs |

##### Remarks

Returns a list containing all literal value pairs.

##### Example
```

> (use User)

.: User

> (definitions (scope))

.: {}

> (function foo {} hello)

.: foo

> (function bar {} world)

.: bar

> (definitions (scope))

.: {{foo "(function foo {} hello)"}

{bar "(function bar {} world)"}}

```

##### Related

symbols

## defunct

Undefines a function in a module.

##### Syntax
```

(defunct function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 1   | A fully qualified function name. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the function. |

##### Remarks

Undefines a function or causes a failure if the function does not exist. Returns the name of the function if successful. Looks for the function in the current module if module is omitted.

##### Example
```

> (function foo bar)

.: foo

> (describe foo)

.: {"(function User.foo {} bar)"}

> (defunct foo)

.: foo

> (describe foo)

.: nil

```

##### Related

defined, describe, function, macro, nix, relation

## degrees

Converts radians into degrees.

##### Syntax
```

(degrees radians)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| radians | real | 1   | a number in radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The number of degrees. |

##### Remarks

The radians are multiplied by 180 / π, or roughly 57.29578049044297, for the conversion.

##### Example
```

> (round (degrees (\* (/ 4 9) (pi))))

.: 80

> (round (degrees 1.4))

.: 80

> (round (degrees 0.7864815))

.: 45

```

##### Related

cosine, radians, sine, tangent

## delete

Modifies a sequence by deleting values.

##### Syntax
```

(delete sequence value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| value | variant | 0+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The modified assortment |

##### Remarks

Destructively modifies a sequence by deleting the values. To create a new sequence with values omitted use the omit function.

##### Example
```

> (delete {a b c d e f g} a b)

.: {c d e f g}

> (delete {a 1 nil b 2 c 3 nil nil d nil 4} nil)

.: {a 1 b 2 c 3 d 4}

```

##### Related

pop, push,

## dependencies

Returns a module's dependencies.

##### Syntax
```

(dependencies module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | A module |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of modules upon which the argument depends. |

##### Remarks

Returns dependencies of a module.

##### Example
```

> (module a

(function foo bar))

.: a

> (module b

(function bar baz))

.: b

> (module c

(require a)

(require b)

(function baz {}

{(foo) (bar)}))

.: c

> (dependencies c)

.: {a b}

```

##### Related

discard, extend, forgo, module, require, grok, using

## deq

Removes an element from an embedded sequence.

##### Syntax
```

(deq container place option)

option ::= all value

option ::= at position

option ::= the value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |
| place | variant | 1   | A key or position. |
| option | expression | 0-1 | One of all value - Removes all occurrences of the value. at position - A number or the literal #. Default is 1.  <br>the value - Removes the first occurrence of the value. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the container. |

##### Remarks

If no options are provided, the last item of the sequence is removed.

##### Example
```

> (deq (lexicon 1 {a a b} 2 {d e f}) 2)

.: Lexicon-1

> (get Lexicon-1 2)

.: {d e}

> (get (deq Lexicon-1 1 all a) 1)

.: {b}

```

##### Related

add, cut, enq, get, has, key, keys, peek, put, values

## describe

Returns descriptions of a literal.

##### Syntax
```

(describe literal)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| literal | literal | 1   | A function, module, relation, or other defined item. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A possibly empty list of descriptions. |

##### Remarks

Returns a list of string descriptions.

##### Example
```

  
> (describe foo)

.: {}

> (relation Foo :Bar :Baz)

.: Foo

> (function foo {} bar)

.: foo

> (describe foo)

.: {"(function User.foo {} bar)" "(relation Foo :Bar nil :Baz nil)"}

```

##### Related

defined, defunct, function, macro, nix, relation

## detach

Unregisters a knowledge base.

##### Syntax
```

(detach knowledge)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base. |

##### Results

| Taxon | Description |
| --- | --- |
| knowledge | The knowledge base. |

##### Remarks

Unregisters an attached knowledge base.

##### Example
```

> (assign ?kb (knowledge url "file://c:/premise/kb/esoteric.mdb"))

.: Knowledge-1

> (attach ?kb)

.: Knowledge-1

> (use ?kb)

.: Knowledge-1

> (relation Fact :All :Are)

.: Fact

> (detach ?kb)

.: Knowledge-1

> (free (cede (alias ?kb)))

.: freed

```

##### Related

attach, conceive, each, eradicate, knowledge, knowing, get, put, using, which, with

## difference

Returns the difference of two sequences.

##### Syntax
```

(difference sequence<sub>1</sub> sequence<sub>2</sub> operation)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2   | A list or string |
| operation | literal | 0-1 | One of : set - returns the set difference. (default) sym - returns symmetric difference |

##### Results

| Taxon | Description |
| --- | --- |
| list | Set difference of sequence1 and sequence2 |

##### Remarks

If the operation is set, this function returns a sequence containing elements from the first sequence not in the second. If the operation is symmetric, it returns items that are not in the intersection of the provided sequences. Sequences must be of the same data type, e.g., either all lists or all strings.

##### Example
```

> (difference "abcd" "abef" set)

.: "cd"

> (difference {1 2 3 4} {2 3 4 5} sym)

.: {1 5}

> (difference {1 2 3} {5 4 3 2})

.: {1}

```

##### Related

common, intersection, union

## did

Evaluates an expression and surpresses failures.

##### Syntax
```

(did expression )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | An expression to evaluate. |

##### Results

| Taxon | Description |
| --- | --- |
| expression | Returns a truth success value, the result , and a possible failure |

##### Remarks

If the expression fails, success shall be false, the result shall be nil, and the failure shall contain the generated failure.

##### Example
```

> (did (string x))

.: true "x" nil

> (did (integer x))

.: false nil [Failure :Name TypeConversion :Text "Cannot convert x to Integer."]

> (bind ?success ?result ?error (did (string "hello world")))

.: true

> ?success ?result ?error

.: true "hello world" nil

```

##### Related

assert, can, ensure, fail, finally, may, try

## digit

Returns the digit in the specified position of a number.

##### Syntax
```

(digit number position)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |
| position | number | 1   | The position of the digit within the number |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The indicated digit (a number between 0 an 9) or nil. |

##### Remarks

Returns the digit in the position of the fractional normed significand (0.nnnnn) of a number. If the position is out of range, nil is returned.

##### Example
```

> (digit 500 1)

.: 5

> (digit 500 2)

.: 0

> (digit 500 3)

.: 0

> (digit 500 4)

.: nil

> (digit (pi) 7)

.: 2

```

##### Related

digits, exponential, fractional, sign, significand,

## digit-p

True if the first position of a string is a digit.

##### Syntax
```

(digit-p value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A variant. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the first position is a digit. |

##### Remarks

None

##### Example
```

> (digit-p "The Quick BROWN fox")

.: false

> (digit-p "100")

.: true

> (digit-p foo)

.: false

> (digit-p 100)

.: false

```

##### Related

alphabetic-p, alphanumeric-p, capitalized-p, lowercase-p, uppercase-p

## digits

Returns the digits comprising a number.

##### Syntax
```

(digits number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |

##### Results

| Taxon | Description |
| --- | --- |
| string | The digits. |

##### Remarks

Returns the fractional digits in the normed significand (0.nnnnn) of a number as a string. Trailing zeros are deleted while leading fractional zeros are preserved.

##### Example
```

> (digits 500)

.: "500"

> (digits 0.00465)

.: "00465"

> (digits -1050.064)

.: "1050064"

> (digits -2302.023900)

.: "23020239"

> (digits 000.003500)

.: "0035"

```

##### Related

digit, exponential, fractional, sign, significand

## dimensions

Returns the lengths of each dimension in a sequence.

##### Syntax
```

(dimensions sequence)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Taxon | Description |
| --- | --- |
| list | The length of each dimension in a sequence. |

##### Remarks

This function returns the length of each nested sequence as a list. The function assumes that the entire sequence has a uniform number of elements in each dimension.

##### Example
```

> (dimensions {{{a}{b}{c}}{{d}{e}{f}}})

.: {2 3 1}

> (dimensions {a b c d})

.: {4}

> (dimensions {{a b c}{d e f}})

.: {2 3}

> (dimensions "abc")

.: {3}

```

##### Related

array

## discard

Discards a module.

##### Syntax
```

(discard module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | A module |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The literal discarded |

##### Remarks

Removes an unwrapped module from the modules collection if no functions are defined in the module, causes a failure otherwise.

##### Example
```

> (module module1

(function foo {} bar))

.: module1

> (for ?fn in (functions module1)

(defunct (qualified module1 ?fn)))

.: nil

> (discard module1)

.: discarded

```

##### Related

dependencies, discard, extend, forgo, module, require, grok, use

## disjoint-p

True if no elements are common among sequences.

##### Syntax
```

(disjoint-p sequence sequence … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | A sequence |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if no elements are common to any sequences. |

##### Remarks

Returns true if, for the provided sequences, no elements are common to any sequences.

##### Example
```

> (disjoint-p {1 2 3 4}{2 3 4 5)

.: false

> (disjoint-p {2 3 4 5}{1 6 7 8})

.: true

> (disjoint-p {1 2 3 4}{2 3 4 5}{3 4 5 6}{4 5 6 7})

.: false

> (disjoint-p "abc" "def" "ghi")

.: true

```

##### Related

intersects-p, subset-p

## distinct

Creates a new sequence without duplicate elements.

##### Syntax
```

(distinct sequence )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A new sequence with duplicates removed |

##### Remarks

Creates a new sequence containing unique items.

##### Example
```

> (distinct {1 2 2 2 3 4 2 3 4 5})

.: {1 2 3 4 5}

> (distinct "abcbcdcde")

.: "abcde"

```

##### Related

difference, intersection, union

## distribute

Applies a function in parallel to a sequence.

##### Syntax
```

(distribute sequence function result)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | list | 1   | A list containing the arguments to each function. |
| function | function | 1   | The function to be distributed and processed in parallel. |
| result | literal | 0-1 | The literal tasks or values (default). |

##### Results

| Taxon | Description |
| --- | --- |
| list | If tasks is specified, a list of tasks is returned immediately, otherwise a list of values are returned upon completion of all the tasks. |

##### Remarks

Returns a list of tasks for each element of the sequence by applying the function to each elment.

##### Example
```

> (distribute {5 6 7} (given {?x} (\* ?x 2)))

.: {10 12 14}

> (distribute {5 6 7} (given {?x} (\* ?x 2)) tasks)

.: {task-1 task-2 task-3}

> (map {task-1 task-2 task-3} await)

.: {10 12 14}

> (distribute {2 3 4} (given {?x} (morph {?x} {++ ++ ++})) values)

.: {5 6 7}

```

##### Related

apply, concurrent, complete, compose,map, mete, morph, scatter

## divide

Safe division.

##### Syntax
```

(divide dividend divisor default)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number.or a list. |
| divisor | variant | 1   | A number.or a list. |
| default | variant | 0-1 | A number or a list. If not supplied, unknown is returned. |

##### Results

| Taxon | Description |
| --- | --- |
| number | Returns the quotient of the numerator and denominators or the default. |

##### Remarks

Returns the quotient of the values or the default. It divides the dividend by the divisor. If the default is not supplied, unknown is returned. All list arguments must be the same length. If an argument is a list, then each element of the list is divided. If a scalar and a list are divided, then the scalar is divided by each element of the list.

##### Example
```

> (divide 1.0 2)

.: 0.5

> (divide 5 0 0)

.: 0

> {divide {4 5 6} 0)

.: {undefined undefined undefined}

> {divide {4 5 6} {1 2 0} -1)

.: {4 2.5 -1}

```

##### Related

/ division, \* multiplication, + addition, - subtraction, % modulo

## divisible-p

True if the divisor evenly divides the dividend.

##### Syntax
```

(divisible-p dividend divisor)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dividend | number | 1   | The value to be divided |
| divisor | number | 1   | The value to divide by |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the modulus of the dividend and divisor equals zero. |

##### Remarks

Causes a failure if the arguments are not numbers, or if the arguments cannot be converted to the same type for comparison (for example, an imaginary compared to an integer).

##### Example
```

> (divisible-p 501 10)

.: false

> (divisible-p 500 10)

.: true

> (divisible-p 28 7)

.: true

```

##### Related

datatype, type, is

## do

Creates a lexical scope.

##### Syntax
```

(do expression …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 0+  | Expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the value of the last executed expression. |

##### Remarks

Each expression is executed in succession and the value of the last expression is returned.

##### Example
```

> (do foo)

.: foo

> (do foo bar baz)

.: baz

> (do (step ?x from 1 to 500 nothing)

(step ?y from 501 to 1000 nothing)

(step ?z from 1000 to 2000 nothing)

done)

.: done

```

##### Related

wait, abort,, await, complete, done-p, reclaim, use, for, iterate, loop, step, task, until, while

## done

Terminates a generator.

##### Syntax
```

(done)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
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

.: myGenerator

> (collect ?x in (myGenerator true) ?x)

.: {1 2}

> (collect ?x in (myGenerator false) ?x)

.: {1 2 3 4}

```

##### Related

generator, generator-p, yield

## drop

Removes a relation index.

##### Syntax
```

(drop index … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| index | index | 1+  | A relation index or list of indicies |

##### Results

| Taxon | Description |
| --- | --- |
| expression | The literal dropped and the number of indices dropped. |

##### Remarks

Removes an index from a relation if one exists, otherwise causes a failure.

##### Example
```

> (relation Car :Make :Model :Year)

.: Car

> (index Car :Make :Model)

.: Car_Index_1

> (index Car :Year)

.: Car_Index_2

> (drop Car_Index_1)

.: dropped 1

> (drop Car_Index_2)

.: dropped 1

```

##### Related

relation, index, indices

## duplicate

Duplicates a file or contents of a folder.

##### Syntax
```

(duplicate source target option)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| source | url | 1   | A source url. |
| target | url | 1   | A target url. |
| option | expression | 0-1 | A key value pair, one of overwrite yes \| no – (default is no). |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The literal duplicated. |

##### Remarks

Duplicates files on a file system.

##### Example
```

> (let ?f (file name "foo.txt"))

.: true

> (write ?f "The quick brown fox")

.: File-1

> (close ?f)

.: closed

> (duplicate (url ?f) (url path "bar.txt"))

.: duplicated

> (duplicate (url ?f) (url path "baz.txt") overwrite yes)

.: duplicated

```

##### Related

erase, move

## during-p

True if an interval occurs within a second interval.

##### Syntax
```

(during-p interval<sub>1</sub> interval<sub>2</sub> tolerance)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if interval1 occurs within interval2. |

##### Remarks

None.

##### Example
```

> (during-p 1s~2s 3s~4s)

.: false

> (during-p 1s~5s 1s~8s)

.: true

> (during-p 1s~9s 4s~6s)

.: false

> (during-p 4s~6s 1s~9s)

.: true

> (during-p 7s~9s 3s~8s 1s)

.: true

```

##### Related

before-p, finishes-p, meets-p, overlaps-p, starts-p

## dynamic

Creates a dynamic environment for symbols.

##### Syntax
```

(dynamic assignments expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assignments | list | 1   | A list of symbol value pairs |
| expression | variant | 0+  | An expression |

##### Results

| Taxon | Description |
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

.: appendToFile

```

##### Related

<-- before tie, --> after tie, assume, assign, constant, global, local, modular, presume

## e

Returns Euler's number, 2.718281828459045.

##### Syntax
```

(e)

```
##### Module

Math

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| real | Returns the constant 2.718281828459045 . |

##### Remarks

None.

##### Example
```

> (e)

.: 2.7182818284590451

```

##### Related

pi

## each

Combines for and with to iterate over sequences matching patterns to the knowledge base.

##### Syntax
```

(each symbol … binding reversal sequence … premises option … action )

premises ::= premise

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= in

binding ::= per

binding ::= over

binding ::= across

reversal ::= across

condition ::= slot \= value

condition ::= slot /= value

condition ::= slot is unary-predicate

condition ::= slot not unary-predicate

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

option ::= scan number

option ::= limit number

option ::= group slot … by slot … into symbol

option ::= merge value …

option ::= sort ordering …

action ::= deem value1 else value2

action ::= do expression …

action ::= give expression

action ::= list value …

action ::= tally

action ::= yield expression

ordering ::= term comparator

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, over, or across. |
| reversal | literal | 0-1 | The literal reverse. |
| sequence | sequence | 1+  | A list or string |
| premises | expression | 1+  | O­ne or more premises |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |
| action | literal | 0-1 | Either deem, do, give, list, tally, yield. |
| expression | expression | 0+  | An expression |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last value returned on the last iteration. |

##### Remarks

Symbols and sequences are required for in, per, and over. If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If the binding across is specified, each symbol is bound to elements of the corresponding sequence (i.e, first symbol to the first sequence, second to the second, etc.). If there are insufficient elements to bind to the symbols then the function fails. If the literal reverse is present, the sequence is traversed in reverse. On each iteration, all the premises are evaluated. Note that a predicate is a truth function, scan tells the number of matches to attempt (default is infinity), and limit tells how many results to return (default is infinity). If the action is deem, then the subsequent value is returned if the final descriptor is matched, otherwise the else value is returned. If the action is do, then for each match the expressions are run, and for the last match, the last value of the last expression is returned, or nil is returned if all descriptors were false or had no matches. If the action is give, then the expression is immediately returned from the each call on the first match, akin to return from each. If the action is yield, then the expression is immediately returned from the each call, but may be resumed with a next function call. When all matches are completed, the done function is implicitly called to terminate the generator. If the action is group, followed by a list of slots and values from which the group is picked, then the literal by and a set of slots and values that determines the grouping inclusion , and finally the literal into followed by a symbol to which the group shall be bound on each iteration. If the action is either list (or merge), then a (merged) list is returned or an empty list if nothing matched. If the action is sort then the list of slots and comparators should follow. (Note that list is required if the sort action is selected.) If the action is tally, then the number of matched premises is returned, or zero if no matches.

(each symbol … binding reversal sequence … premises option … action expression … ))

Is equivalent to  

(for symbol … binding reversal sequence … (with premises option … action expression … ))

The difference between for and each is that in a for expression, on every iteration, all the expressions following the sequence(s) are evaluated and the return value is the result of the last expression evaluated on the last iteration. In the each expression, the premises following the sequence(s) are evaluated, and if any premise is false, the next iteration occurs, otherwise, if all the premises are true, the action is taken, and the action expressions are evaluated.

##### Example
```

> (relation Sport

:Name

:PlayersPerTeam)

.: Sport

> (relation Team

:Name

:Sport

:Players {})

.: Team

> (relation Person

:Name

:Skills

:Teams {})

.: Person

> (relation Skill

:Sport

:Level)

.: Skill

> (repeat (random 1 to 10)

(let ?sport (new Sport :Name (unique "sport")

:PlayersPerTeam (random 1 to 12)))

(repeat (\* (random 1 to 10) 2) ; even number of teams

(let ?team (new Team :Name (unique "team") :Sport ?sport)))

Leagues)

.: Leagues

> (let {?sports (which Sport)

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

.: Players

> (collect ?sport in (which Sport)

{?sport (avg (which Skill :Sport = ?sport :Level as ?level list ?level))}))

.: {{sport3 4.9} {sport1 7.898} {sport2 6.382} {sport4 8.452}}

```

##### Related

which, with

## encode

Encodes a string.

##### Syntax
```

(encode source format)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| source | string | 1   | A string to encode. |
| format | literal | 1   | One of { base16, base64, utf8, utf16, none } |

##### Results

| Taxon | Description |
| --- | --- |
| string | The encoded string |

##### Remarks

Converts a string to the specified format.

##### Example
```

> (encode "The quick brown fox" base16)

.: "54686520717569636B2062726F776E20666F78"

> (encode "The quick brown fox" base64)

.: "VGhlIHF1aWNrIGJyb3duIGZveA=="

> (encode "The quick brown fox" none)

.: "The quick brown fox"

> (decode "54686520717569636B2062726F776E20666F78" base16)

.: "The quick brown fox"

> (decode "VGhlIHF1aWNrIGJyb3duIGZveA==" base64)

.: "The quick brown fox"

> (decode "The quick brown fox" none)

.: "The quick brown fox"

```

##### Related

decode

## enq

Inserts an element into an embedded sequence.

##### Syntax
```

(enq container place entry)

entry ::= position value

entry ::= unique value

entry ::= value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | assortment | 1   | An assortment or tuple |
| place | variant | 1   | A key or position. |
| entry | expression | 1   | Any of the following: value - appends the value to the sequence. position value - inserts the value at the position. coordinate value - inserts the value in the list coordinate. unique value - appends value if it is not already present. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The modified container. |

##### Remarks

If only a single value is provided for entry, then the value is appended to the sequence. If an integer position and value is provided, then the value is inserted at the position. If the keyword unique is provided, then the value is appended to the sequence if it does not already exist

##### Example
```

> (let ?a {{}{1 2 3}{}})

.: true

> (enq ?a {2 2} 8)

.: {{}{1 8 2 3}{}}

```

##### Related

add, cut, deq,get,has, key, keys, peek, put, values

## ensure

Performs type checking.

##### Syntax
```

(ensure check … )

check ::= kind value

check ::= {kind … } value

kind ::= taxon

kind ::= meron

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| check | expression | 1+  | A datatype, prototype, or list containing datatypes and prototypes. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if all values correspond to their indicated types. |

##### Remarks

If any of the values do not correspond to their designated types, then the function fails; otherwise the function returns true.

##### Example
```

> (function multiply {?a ?b + ?c}

(ensure number ?a number ?b {number nil} ?c)

(\* ?a ?b (default ?c 1)))

.: multiply

> (multiply 10 banana)

.: [Failure :Name InvalidArg :Text "Expected a number, encountered banana."]

> (multiply 10 5)

.: 50

```

##### Related

assert, can, did, fail, may, try

## entries

Retrieves key value pairs for an assortment.

##### Syntax
```

(entries assortment )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of all key value pairs |

##### Remarks

Returns a list containing key value pairs for an association.

##### Example
```

> (entries (lexicon a 1 b 2 c 3 d 4))

.: {{a 1} {b 2} {c 3} {d 4}}

> (entries (structure Foo :X :Y :Z apple))

.: {{relation Foo} {:X nil} {:Y nil} {:Z apple}}

```

##### Related

bindings, definitions, positions

## enumeration

Defines an enumerated assortment.

##### Syntax
```

(enumeration name element … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of an enumeration |
| element | expression | 1+  | A literal or literal number pair. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the enumeration |

##### Remarks

Each entry in the elements list may be a literal or a list containing a literal and a number. If a number is present, the number shall be assigned to the preceding literal as the index of that literal, and the next literal shall have an index of the number plus one, unless another index is present. For example, the arguments a, b 7, c: a shall be assigned the value 1, b shall be assigned the value 7, and c shall be assigned the value 8. An enumeration is an immutable assortment so it cannot be modified.

##### Example
```

> (enumeration MySimpleType a b 7 c)

.: MySimpleType

> (keys MySimpleType)

.: {a b c}

> (entries MySimpleType)

.: {{a 1}{b 7}{c 8}}

> (values MySimpleType)

.: {1 7 8}

```

##### Related

add, cut, elem, enumerations, elems, entries, size

## enumerations

Returns a list of all enumerations.

##### Syntax
```

(enumerations)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list of enumerations. |

##### Remarks

None.

##### Example
```

> (enumerations)

.: {}

> (enumeration MySimpleType {a b c})

.: MySimpleType

> (enumerations)

.: {MySimpleType}

```

##### Related

enumeration

## environment

Creates a new context for symbols and functions.

##### Syntax
```

(environment parent entry … )

entry ::= symbol value

entry ::= function definition

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| parent | environment | 0-1 | An environment or the value nil. |
| entry | expression | 0+  | A symbol and value pair or function and definition pair. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | A resource to the environment |

##### Remarks

Entries with literal keys are retrieved via the definitions function, while entries with symbol keys are retrieved with the bindings function. All entries may be retrieved using the entries function.

##### Example
```

> (environment nil (symbol A) "hello world")

.: Environment-1

> (add Environment-1 foo (given {?x}(+ ?x 1)))

.: Environment-1

> (add Environment-1 bar (function bar {?x} (\* ?x 2)))

.: Environment-1

> (entries Environment-1)

.: {{?A "hello world"} {foo (given {?x}(+ ?x 1))} {bar (fn bar {?x} (\* ?x 2))}}

```

##### Related

@, add, includes, cut, entries, environment-p, keys, reclaim, #, values

## epoch

Returns a Unix epoch or the current epoch.

##### Syntax
```

(epoch time)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| time | time | 0-1 | A date, moment, seconds or tick value. |

##### Results

| Taxon | Description |
| --- | --- |
| epoch | The Unix time in seconds since January 1, 1970 (UTC). |

##### Remarks

Converts the supplied time to a Unix epoch.

##### Example
```

> (epoch 2014-11-29T23:39:29.741)

.: 1417333169p

> (epoch 2014939313515537m)

.: 1481565910p

> (epoch 63573798191026000t)

.: 1481565910p

> (epoch (date))

.: 1533235279p

> (epoch)

.: 1533235284p

> (epoch (tick))

.: 1533235295p

```

##### Related

date, moment, tick

## eradicate

Deletes a knowledge base.

##### Syntax
```

(eradicate knowledege)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| knowledge | knowledge | 1   | A knowledge base |

##### Results

| Taxon | Description |
| --- | --- |
| knowledge | The opened knowledge base. |

##### Remarks

Deletes an existing knowledge base.

##### Example
```

> (conceive (assign ?kb (knowledge name defaultKB path "c://premise/kb/")))

.: defaultKB

> (attach ?kb)

.: defaultKB

> (relation Fact :All :Are)

.: Fact

> (detach ?kb)

.: defaultKB

> (eradicate ?kb)

.: defaultKB

> (free (cede (alias ?kb)))

.: freed

```

##### Related

attach, conceive, detach,each, get, knowledge, knowing, put, using, which, with

## erase

Deletes files or folders.

##### Syntax
```

(erase file option … )

option ::= key value

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| file | file | 1   | A file resource. |
| option | expression | 0-1 | Key value pairs where a key is one of force yes\|no - forcibly erase the file. Default is no. type {file or folder} - what to erase. Default is file. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The literal erased. |

##### Remarks

This function attempts to delete a file. If successful it returns erased, otherwise it causes a failure.

##### Example
```

> (let ?path (file path (path "quick.txt")))

.: true

> (erase ?path force yes)

.: erased

> (erase (url scheme folder path (folder "c:/foo")) type folder)

.: erased

```

##### Related

close, file-p, files, folders, file, read, seek, write

## escape

Escapes to the next resume tag in the call graph.

##### Syntax
```

(escape)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| Failure | A failure. |

##### Remarks

Returns control to the most proximate resume tag of a try function on the expression call graph.

##### Example
```

> (try

(try

(fail :Name User :Text "A big problem")

learn ?e

(tell user ($ Learned ?e \n))

(tell user ($ Rethrowing... \n))

(escape))

learn ?f

(tell user ($ Learned ?f again. \n))

resume

(tell user ($ Resuming \n))

finally

done)

Learned [Failure :Name User :Text "A big problem"]

Rethrowing...

Resuming

.: done

```

##### Related

confirm, confute, ensure, fail, signal, try

## eval

Evaluates an expression.

##### Syntax
```

(eval expression environment )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1   | An expression to be evaluated |
| environment | environment | 0-1 | An environment |

##### Results

| Taxon | Description |
| --- | --- |
| value | The result of evaluating the expression |

##### Remarks

Evaluates the expression and returns the resulting value. If no environment is provided, the current scope is used. The environment parameter is always evaluated in the current scope while the expression is evaluated in the provided scope, or the current scope if argument 2 is omitted.

##### Example
```

> (eval (+ 1 2 3 4))

.: 10

> (' (+ 1 2 3 4))

.: (+ 1 2 3 4)

> (eval (' (' (+ 1 2 3 4))) (scope))

.: (+ 1 2 3 4)

> (eval (eval (' (' (+ 1 2 3 4))))

.: 10

```

##### Related

' quote, \` expand, apply, call, invoke

## even-p

True if the number is even.

##### Syntax
```

(even-p number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the number is even. |

##### Remarks

None.

##### Example
```

> (even-p 500)

.: true

> (even-p 0)

.: true

> (even-p -23)

.: false

```

##### Related

odd-p, negative-p, positive-p, zero-p

## every

True if a predicate is true for every element in a sequence.

##### Syntax
```

(every symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if every element satisfies the predicate, else false. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example
```

> (every ?n in {1 2 3 4} (= number (taxon ?n)))

.: true

> (every ?m ?n per {{1 2} {3 4}} (< ?m ?n))

.: true

> (every ?m ?n over {4 3 2 1} (divisible-p ?m ?n))

.: false

```

##### Related

few, most, nevery, none, some

## exactly

True if a number of elements satisfy a clause.

##### Syntax
```

(exactly quantity of sequence clause within margin )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| quantity | number | 1   | A number |
| of  | literal | 1   | The literal of |
| sequence | sequence | 1   | A sequence |
| clause | expression | 1   | A key value pair. One of is value - a sequence element, are value - a sequence element, satisfies predicate - a unary truth function. satisfy predicate - a unary truth function. |
| within | literal | 0-1 | The literal within |
| margin | number | 0-1 | A number. (default is zero). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if exactly quantity elements satisfies the predicate |

##### Remarks

The predicate must return true or false.

##### Example
```

(exactly 4 of {1 2 3 4} satisfies number-p)

.: true

(exactly 1 of {1 a 3 4} is a)

.: true

(exactly 3 of {1 2 3 4} satisfy odd-p within 1)

.: true

```

##### Related

\= equal,

## exchange

Creates a new a sequence with values swapped.

##### Syntax
```

(exchange sequence substitution … )

substitution ::= prior-position later-position

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or a string. |
| substitution | expression | 1+  | A prior and later position pair.  <br>A position may be a number or a list of numbers.. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The modified sequence |

##### Remarks

Returns a copy of the original sequence with substitutions made. For destructive modification of a sequence use the swap function.

##### Example
```

> (exchange {A B C} 1 3)

.:{C B A}

> (exchange "ABCD" 1 3)

.:'CBAD'

> (exchange {{1 2 3}{4 5 6}} {2 1} {1 3})

.: {{1 2 4}{3 5 7}}

```

##### Related

@ element, append, fix, push, pop, swap

## excludes

True if a sequence does not contain an element.

##### Syntax
```

(excludes sequence element option … )

```
##### Module

KB

##### Parameters

None

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| element | variant | 1   | A value |
| option | expression | 0-2 | A key value pair. Any of depth number \- Number or # (for any depth). Default is 1. transform function \- A function to transform the element.. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the element is not in the sequence. |

##### Remarks

If the element and sequence are strings, then a string search is performed.

##### Example
```

> (excludes {a b c d e f g} x)

.: true

> (excludes "cbazyx" "a")

.: false

```

##### Related

includes, excludes, in, occurences, out, pick, position

## exists-p

True if a value is a thing.

##### Syntax
```

(exists-p value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the values is a thing. |

##### Remarks

None.

##### Example
```

> (exists-p yes)

.: true

> (exists-p nil)

.: false

> (exists-p (nothing))

.: false

> (exists-p 3.1415926)

.: true

```

##### Related

null-p

## exit

Explicitly ends a task using a return value.

##### Syntax
```

(exit value)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | A return value. Defaults to nil if not specified. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The argument value |

##### Remarks

Forcibly ends a task. Calling exit from the interpreter shall not exit the interpreter. The bye function must be called to exit the interpreter.

##### Example
```

> (concurrent (step ?x from 1 to 999999999

(if (> ?x 1000000) (exit exited)))) ;

.: {Task-343}

> (await task-343)

.: exited

> (free task-343)

.: freed

> (exit done)

.: done

```

##### Related

wait, abort, await, complete, do, task

## exponential

Returns the base ten exponent of a number.

##### Syntax
```

(exponential number significand)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |
| significand | literal | 0-1 | One of normed, scientific, integer. Default is scientific. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The exponent. |

##### Remarks

The normed significand represents the number as a fraction (0.nnnn). The scientific significand represents the number as a decimal between 1.0 and 10.0 (n.nnnn). The integer significand represents the number as an integer (nnnn). The exponential represents the power of 10 to which the significand must be raised to accurately reflect the number.

##### Example
```

> (exponential 500)

.: 2

> (exponential 0)

.: 1

> (exponential -1000 normed)

.: 4

> (exponential -2302.023900 integer)

.: -4

> (exponential 0.003500 scientific)

.:-3

```

##### Related

digit, digits, fractional, sign, significand,

## expression

Creates an expression.

##### Syntax
```

(expression value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | Any value |

##### Results

| Taxon | Description |
| --- | --- |
| expression | Returns a expression containing the values. |

##### Remarks

Expressions are lists without delimiters. An empty expression has no printed representation.

##### Example
```

> (expression a b c {d})

.: a b c {d}

> (expression "a b c")

.: "a b c"

> (let ?a 1 ?b 2)

.: true

> (bind ?a ?b (expression ?b ?a))

.: true

> ?a ?b

.: 2 1

> (void-p (expression))

.: true

```

##### Related

inside, is, void-p  

## extend

Adds new definitions to a module.

##### Syntax
```

(extend module expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | The module containing the extended definitions |
| expression | expression | 0+  | An expression. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The module literal. |

##### Remarks

Allows new definitions to occur in the target module. The module must be unwrapped.

##### Example
```

> (use User)

.: User

> (extend MyModule (function foo {} 100))

.: MyModule

> (MyModule.foo)

.: 100

```

##### Related

dependencies, discard, forgo, module, modules, require, grok, use

## facility

Creates a private function in a module.

##### Syntax
```

(facility name parameters expression … )

parameters ::=

parameters ::= { }

parameters ::= {required … }

parameters ::= {required … + optional … }

parameters ::= { \+ optional … }

parameters ::= {required … \+ optional … & remaining }

parameters ::= { & remaining }

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing symbols, keywords, sigils, and keyword symbol associations. |
| expression | variant | 0+  | One or more expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Facilities are module level functions which are not accessible outside of the module in which they are created. If the name is supplied then the facility is a named facility, otherwise it is automatically named (auto-named). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following are optional. If an ampersand is provided, then the symbol following is bound to a list of remaining actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted.

##### Example
```

> (module SuperMath

(facility power {?x + ?y = 1} ; private to the module

(\*\* ?x ?y)

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

.: SuperMath

> (use User)

.: User

> (SuperMath.superpower 2 3 4)

.: 4096

> (SuperMath.power 2 3)

.: [Failure :Name UndefinedFunction :Text "The function SuperMath.power is not defined"]

> (facility-p power SuperMath)

.: true

> (function-p power SuperMath)

.: false

```

##### Related

call, extend, functions, macro, module, modules

## fail

Creates and signals a failure.

##### Syntax
```

(fail option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 0+  | Key value pairs :Name name \- The failure name (default is User). :Text text \- The failure text (default "Unexpected failure."). |

##### Results

| Taxon | Description |
| --- | --- |
| Failure | A failure. |

##### Remarks

If no arguments are supplied a generic failure is created and propagated. Use the signal function to propagate a failure further up the call graph for another handler to address.

##### Example
```

> (try

(try

(fail :Name User :Text "A big problem")

learn ?e

(tell user ($ Learned ?e \n))

(tell user ($ Signaling... \n))

(resignal ?e))

learn ?f

(tell user ($ Learned ?f again. \n))

resume

(tell user ($ Resuming \n))

finally

done)

Learned [Failure :Name User :Text "A big problem"]

Signaling...

Resuming [Failure :Name User :Text "A big problem"] again

.: done

```

##### Related

confirm, confute, ensure, escape, signal, try

## few

True if a predicate is true for less than half the elements in a sequence.

##### Syntax
```

(few symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if less than half the elements satisfies the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated.

##### Example
```

> (few ?n in {1 2 3 4} (= (taxon ?n) number))

.: false

> (few ?m ?n per {{2 1} {3 4} {7 9}} (< ?m ?n))

.: false

> (few ?m ?n over {4 2 3 7} (divisible-p ?m ?n))

.: true

```

##### Related

every, nevery, most, none, some

## file

Opens or creates a file.

##### Syntax
```

(file url option … )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url to the file. |
| option | expression | 0+  | A key value pair. Any of mode mode \- append, create, open (default), truncate.  <br>access access \- read, write, or readwrite (default).  <br>sharing share \- none, read (default), write, or readwrite.  <br>seek location - a number from 1 (default) to # (eof).  <br>content type - binary (default) or text.  <br>from place - memory or network (default).  <br>buffer size - minimum buffer size (default is 1). |

##### Results

| Taxon | Description |
| --- | --- |
| file | A file literal. |

##### Remarks

Opens a file for reading or writing and returns a file resource. If the file does not exist then it is created. If from memory is specified, the contents of the file is first cached locally to memory then accessed. If from network is specified, the contents of the file isaccessed over the network.

##### Example
```

> (let ?url (url "file://localhost/C:/temp/quick.txt"))

.: true

> (if (there ?url)

(let ?file (file ?url mode append))

(write ?file "The quick brown fox")

(close ?file)

(free ?file))

.: closed

```

##### Related

close, erase, free, read, seek, there, write

## files

Returns a list of file names.

##### Syntax
```

(files folder )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| folder | folder | 1   | A folder. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list file name strings. |

##### Remarks

If the path is invalid, the function fails. Files or symbolic links to files are returned.

##### Example
```

> (files path (path "c" (separator volume)))

.: {"homework.txt" "temp.txt" "mypath.lnk"}

```

##### Related

folder, folders, links, there, path, separator

## fill

Fills a list with the result of an expression.

##### Syntax
```

(fill symbol from start to end by increment with expression)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A variable iterator |
| from | literal | 0-1 | The literal from. |
| start | number | 0-1 | A number. If from is given this is required. Defaults to 1. |
| to | literal | 1   | The literal to. |
| finish | number | 1   | A number. |
| by | literal | 0-1 | The literal by. |
| increment | number | 0-1 | A number. If by is supplied this is required. |
| with | literal | 1   | the literal with. |
| expression | variant | 1   | a value to populate the list |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of the indicated length containing the value of the expression. |

##### Remarks

The value of the variable iterator is available to the expression when building the list.

##### Example
```

> (fill ?i to 3 with ($ "foo-" ?i))

.: {"foo-1" "foo-2" "foo-3"}

> (fill ?j to 5 with (\* ?j 2))

.: {2 4 6 8 10}

> (fill ?x from -4 to 6 by 2 with {?x})

.: {{-4}{-2}{0}{2}{4}{6}}

```

##### Related

fill, pad, range

## filter

Returns a sequence of elements that satisfy a predicate.

##### Syntax
```

(filter sequence predicate )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| predicate | function | 1   | A truth function. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A new list containing elements satisfying the predicate. |

##### Remarks

For each element in the sequence, if the predicate is true for the element, the element is concatenated into a result list, otherwise the item is excluded from the result list. Finally, the result list is returned.

##### Example
```

> (filter {1 2 3 4} even-p)

.: {2 4}

> (filter {1 2 3 4 5 6} (given {?n} (divisible-p ?n 3))

.: {3 6}

```

##### Related

apply, coalesce, collect, gather, reduce, sort, map, quantity

## find

Returns the best matching candidates.

##### Syntax
```

(find features candidates option ... )

option ::= key value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| features | List | 1   | The features to compare to the candidates |
| candidates | list | 1   | The candidates to be compared |
| option | expression | 0+  | Key value pairs , where a key is one of: limit - The number of matches to return.  <br>(default is 1) minscore - value above which candidates shall be considered. Default is ninfinity maxscore – Value below which candidates are acceptable. Default is 1. transform – The literal name of a value transformation function. comparer - The literal name of a comparison function |

##### Results

| Taxon | Description |
| --- | --- |
| list | A sorted list of lists containing candidate - score pairs. |

##### Remarks

Find compares a set of features to those of candidates and returns the best matching candidate(s) with match score(s). It uses the similarity function (~) as the default comparer. If provided, transforms are applied before comparison. Finally, a comparer can accept two values and returns a score representing the degree of similarity where higher means more similar.

##### Example
```

> (find {" t" " th" "thi" "his" "is " "s "}

{"there" "that" "though" "thin"}

comparer (given {?x} (ngrams ?x 3)))

.: {{"thin" 0.142857}}

```

##### Related

~ similarity, /~ dissimilarity

## finishes-p

True if two intervals finish together.

##### Syntax
```

(finishes-p interval<sub>1</sub> interval<sub>2</sub> tolerance)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if interval1 finishes with interval2. |

##### Remarks

None.

##### Example
```

> (finishes-p 1s~2s 3s~4s)

.: false

> (finishes-p 1s~5s 4s~5s)

.: true

> (finishes-p 1s~9s 4s~6s)

.: false

> (finishes-p 4s~9s 1s~9s)

.: true

> (finishes-p 7s~9s 3s~8s 1s)

.: true

```

##### Related

before-p, during-p, meets-p, overlaps-p, starts-p

## finishing

Returns the instant an interval finishes.

##### Syntax
```

(finishing interval)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval | interval | 1   | An interval |

##### Results

| Taxon | Description |
| --- | --- |
| instant | The finishing value of the interval. |

##### Remarks

None.

##### Example
```

> (finishing 1s~2s)

.: 2s

> (finishing 1s~5s)

.: 5s

> (finishing 4s~6s)

.: 6s

```

##### Related

beginning

## fix

Adds symbols to the current environment.

##### Syntax
```

(fix declaration ... )

declaration ::= taxon symbol value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| declaration | expression | 1+  | A taxon, symbol and value triple. |

##### Results

| Taxon | Description |
| --- | --- |
| Truth | Returns true. |

##### Remarks

Sequentially creates symbols in the current environment. Each symbol shall replace any extant symbol with the same name in the environment. The taxon shall restrict the type of the symbol. If the default does not match the taxon, a failure shall be triggered.

##### Example
```

> (fix literal ?person DrWho)

.: true

> ?person

.: DrWho

> (fix integer ?x 1

float ?y 2.0

long ?z 3n)

.: true

```

##### Related

<-- before tie, --> after tie, constant, dynamic, fix, global, local, set, tie, presume

## float

Converts a value to a floating number.

##### Syntax
```

(float value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number or the literal minimum or maximum. |

##### Results

| Taxon | Description |
| --- | --- |
| float | A float number. |

##### Remarks

If the value cannot be converted to a float, the function fails.

##### Example
```

> (float {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a float"]

> (float "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not a float"]

> (float 500)

.: 500.0f

> 500.0f

.: 500.0f

> (float "23.4")

.: 23.4f

```

##### Related

complex, imaginary, integer, long, rational, real

## floor

Rounds a number towards negative infinity.

##### Syntax
```

(floor number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| number | The next lower integer. |

##### Remarks

Returns the next lower positive integer.

##### Example
```

> (floor 100.5)

.: 100

> (floor -100.5)

.: -101

```

##### Related

ceiling, round, truncate

## fold

Tranforms a sequence into a value.

##### Syntax
```

(fold symbol … in sequence into expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 2+  | Iteration variables |
| in | literal | 1   | The literal in |
| sequence | sequence | 1   | A sequence (string or list) |
| into | literal | 1   | The literal into |
| expression | variant | 1+  | A expression that transforms the iteration variables |

##### Results

| Taxon | Description |
| --- | --- |
| list | A new list after the transformation is applied |

##### Remarks

The first element of the list is stored in the first symbols and the second element is stored in the second symbol (and so forth), then the expressions are evaluated. The result of the last expression is stored in the first symbol while the next element(s) in the sequence is (or are) stored in the second symbol (and so on). This is repeated until all elements are processed

##### Example
```

> (fold ?x ?y in {1 2 3 4 5} into (\* ?x ?y))

.: 120

> (generator OneToFive (yield 1)(yield 2)(yield 3)(yield 4)(yield 5)(done))

.: OneToFive

> (fold ?i ?j ?k in (OneToFive) into (+ ?i ?j ?k))

.: 15

```

##### Related

reduce

## folder

Creates or locates a folder in the file system.

##### Syntax
```

(folder url )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url to the file. |

##### Results

| Taxon | Description |
| --- | --- |
| folder | A folder resource. |

##### Remarks

Returns a folder resource.

##### Example
```

> (let ?path (path "." (separator) "temp"))

.: true

> (there path ?path)

.: false

> (folder path ?path)

.: folder-1

> (there path ?path)

.: true

```

##### Related

file, file-p, folder-p, path, read, separator, write

## folders

Returns a list of sub folders.

##### Syntax
```

(folders option … )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 1+  | A key value pair. One of url url \- full url to the file. host host \- name of the host computer volume volume \- name of the disk volume path path - name of the path to the folder name name \- name of the folder |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of folders strings in the specified path. |

##### Remarks

If the path is invalid, the function fails. Otherwise, a list of sub folders is returned for the path.

##### Example
```

\>(folders path (path "."))

.: {"build" "META-INF" "WebContent"}

```

##### Related

erase, file, files, folder, there, path, separator

## for

Iterates over the elements in a sequence.

##### Syntax
```

(for symbol … binding reversal sequence … expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, over, or across. |
| reversal | literal | 0-1 | The literal reverse. |
| sequence | sequence | 1+  | A list or string |
| expression | variant | 0+  | The expression(s) to evaluate |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last value returned on the last iteration. |

##### Remarks

Symbols and sequences are required for in, per, and over. If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If the binding across is specified, each symbol is bound to elements of the corresponding sequence (i.e, first symbol to the first sequence, second to the second, etc.). If there are insufficient elements to bind to the symbols then the function fails. If the literal reverse is present, the sequence is traversed in reverse. On each iteration, all the expressions are executed. The return value is the result of the last call evaluated on the last iteration.

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
```

(forever expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, over, or across. |
| reversal | literal | 0-1 | The literal reverse. |
| sequence | sequence | 1+  | A list or string |
| expression | variant | 0+  | The expression(s) to evaluate |

##### Results

| Taxon | Description |
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

\>> hello

\*

```

##### Related

count, do, each, loop, repeat, step, until, while

## forgo

Removes a dependent module.

##### Syntax
```

(forgo dependency module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dependency | literal | 1   | A dependent module. |
| module | literal | 0-1 | A module. Default to the module obtained by (use). |

##### Results

| Taxon | Description |
| --- | --- |
| module | Returns the module. |

##### Remarks

Removes a module from the current module’s dependencies list.

##### Example
```

> (dependencies User)

.: {Premise}

> (extend User (require (module Algebra)))

.: Algebra

> (dependencies User)

.: {Premise Algebra}

> (forgo Algebra User)

.: User

> (dependencies User)

.: {Premise }

```

##### Related

dependencies, discard, extend, forgo, module, require, grok, use

## format

Formats a string.

##### Syntax
```

(format template value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| template | string | 1   | A format template. which uses the following directives: ~c - formats a number as currency ~e - formats a number as an exponential ~f - formats a floating point number ~i - formats an integer number ~n - formats a generic number ~s - formats a string. ~v \- formats a generic variant ~~ - formats a single tilde character |
| value | variant | 0+  | A value to be formatted. |

##### Results

| Taxon | Description |
| --- | --- |
| string | A formatted string |

##### Remarks

The formatted result is returned.

##### Example
```

> (format "~v ~v" hello world)

.: "hello world"

```

##### Related

$ concatenate, $$ elide, ask, capitalize, char, lowercase, tell, trim, uppercase

## fractional

Returns the fractional portion of a number.

##### Syntax
```

(fractional number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The fractional portion. |

##### Remarks

The fractional portion is the number minus the floor of the number.

##### Example
```

> (fractional 300)

.: 0.0

> (fractional 0.564)

.: 0.564

> (fractional -2302.023900)

.: -0.0239

> (fractional 0.003500)

.:0.0035

```

##### Related

digit, digits, exponential, sign, significand

## free

Releases resources.

##### Syntax
```

(free resources )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| resources | variant | 1   | A single resource or list of resources. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns the literal freed if successful. |

##### Remarks

None.

##### Example
```

> (free

(tarry (complete

(do (idle 5s) something)

(do (idle 5s) something-else)

(do (idle 5s) one-more-thing))))

.: freed

> (free

(cancel (complete

(do (idle 5s) something)

(do (idle 5s) something-else)

(do (idle 5s) one-more-thing))

mode immediate))

.: freed

```

##### Related

concurrent, cancel, complete, reclaim, tarry, task, wait

## full

True if values are equal or either value is nil.

##### Syntax
```

(full first second )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| first | variant | 1   | A value to be compared. |
| second | variant | 1   | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are the same or if either is nil |

##### Remarks

Returns true if each value is the same or if either value is nil. Both values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equivalent if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical). Return false otherwise.

##### Example
```

> (full a a)

.: true

> (full "johnny" "ralph")

.: false

> (full 3 nil)

.: true

> (full nil 4)

.: true

```

##### Related

< less , <= less or equal, > greater, >= greater or equal, /= unequal, identical, left, right

## function

Creates a public function in a module.

##### Syntax
```

(function scope name parameters returns expression … )

parameters ::=

parameters ::= { }

parameters ::= {required … }

parameters ::= {required … + optional … }

parameters ::= {required … + optional … % keyword }

parameters ::= {required … \+ optional … % keyword … & remaining }

parameters ::= {required … % keyword … & remaining }

parameters ::= {required … & remaining }

parameters ::= { \+ optional … }

parameters ::= { \+ optional … % keyword }

parameters ::= { \+ optional … % keyword … & remaining }

parameters ::= { \+ optional … & remaining }

parameters ::= { % keyword … }

parameters ::= { % keyword … & remaining }

parameters ::= { & remaining }

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied, a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing symbols, keywords, sigils, and keyword symbol associations. |
| returning | expression | 0-1 | The expression “returns taxon”, where taxon is a taxon or meron. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Functions are defined using the function intrinsic function. If the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If a percent sign is supplied the next symbols are keyword symbols where the supplied slot shall have the same name as the symbol parameter excepting the first character of the name which shall be a colon for the slot and a question mark for the symbol. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. The entire parameter list may be omitted.

If the literal returns follows the (non)extant parameter list then the next literal is either a taxon or a meron. which restricts the result of the function. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example
```

> (function {?n} (+ 1 ?n))

.: fn-1

> (function plusN {?n + ?i = 1} (+ ?n ?i))

.: plusN

> (function (scope) addAll {& ?nums} (apply + ?nums))

.: addAll

> (fn-1 100)

.: 101

> (plusN 100)

.: 101

> (function tryParseNum {String ?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

> (tryParseNum "foo")

.: {false nil}

> (tryParseNum "123")

.: {true 123}

> (function dont {{try ?what} + {at ?where = nil}}

(apply (given {?s}(tell user ?s))

($ don't try ?what (unless (any ?where) "" ($ at ?where))))

.: dont

> (dont try "skydiving into a volcano")

don't try skydiving into a volcano

.: told

> (dont try this at home)

don't try this at home

.: told

```

##### Related

arguments, call, extend, functions, junction, macro, module, modules, parameters

## functions

Returns a list of functions defined in a module.

##### Syntax
```

(functions module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module. If not provided defaults to the current module. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of functions defined in the module. |

##### Remarks

The module must be a literal in the list obtained by calling the (modules) function. If the module is not provided this function uses the current module (obtained via the (use) function).

##### Example
```

> (module Mine

(function foo {} bar))

.: Mine

> (functions Mine)

.: {foo}

> (use User)

.: User

> (function hello {} world)

.: hello

> (functions)

.: {hello}

```

##### Related

function, module, modules, symbols

## gather

Returns a sequence of elements that satisfy a predicate.

##### Syntax
```

(gather symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A sequence (string or list) |
| expression | variant | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A sequence containing the elements that satisfy the test. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated. If the last value returned is a true truth value, the item is concatenated into a result list, otherwise the item is excluded from the result list. Finally, the result list is returned.

##### Example
```

> (gather ?n in {-3 -2 -1 0 1 2 3 4} (even-p ?n))

.: {-2 0 2 4}

> (gather ?x ?y per {{4 2}{7 3}{1 2}{15 5}} (divisible-p ?x ?y))

.: {{4 2}{15 5}}

```

##### Related

coalesce, collect, filter

## generator

Creates a series generator.

##### Syntax
```

(generator name parameters expression … )

parameters ::=

parameters ::= { }

parameters ::= {required … }

parameters ::= {required … + optional … }

parameters ::= { \+ optional … }

parameters ::= {required … \+ optional … & remaining }

parameters ::= { & remaining }

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern gn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing symbols, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| generator | A function that returns a series. |

##### Remarks

If the name is not supplied then the generator is automatically named (auto-named). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided in the call to the generator. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following are optional. If an asterisk is provided, then keyword and vaues are expected. Keyword parameters (literal symbol pairts) may be provided as required or optional. If an ampersand is provided, then the symbol following is bound to a list of remaining actual parameter values. The entire parameter list may be omitted.

##### Example
```

> (generator primeNumbers

(let {?primes {}}

(step ?i from 2 to infinity

(if (none ?p in ?primes (divisible-p ?i ?p))

(add ?primes ?i)

(yield ?i)))))

.: primeNumbers

> (collect ?p in (primeNumbers)

(if (> ?p 20) (break ?p) else ?p))

.: {2 3 5 7 11 13 17 19 23}

> (let ?series (series (primeNumbers)))

.: true

> (if (next ?series) (this ?series))

.: 2

> (if (next ?series) (this ?series))

.: 3

> (if (next ?series) (this ?series))

.: 5

> (generator {?interrupt}

(yield 1)

(yield 2)

(if ?interrupt (done))

(yield 3)

(yield 4)

(done))

.: gen-1

> (collect ?x in (gen-1 true) ?x)

.: {1 2}

> (collect ?x in (gen-1 false) ?x)

.: {1 2 3 4}

> (gen-1 true)

.: {...}

```

##### Related

done, is, next, reset, this, yield

## get

Retrieves a value using one or more keys.

##### Syntax
```

(get container key … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | A sequence or assortment. |
| key | variant | 1+  | A key or function. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The value resulting from the retrieval. |

##### Remarks

Consecutively applies the next key to each resultant value. Terminates when all keys are exhausted or when the function fails.

##### Example
```

> (get (new (relation Box :Length 24 :Width 12 :Height 9)) :Width ++ ++)

.: 14

> (relation Person :Name :Friend)

.: Person

> (let {?person nil}  
(for ?name in {Jane John Sally Chuck Martha Shane Todd}

(tie ?person (new Person :Name ?name :Friend ?person))))

.: Person_7

> (get Person_7 :Friend :Name)

.: Shane

> (get Person_7 :Friend :Friend :Name)

.: Martha

```

##### Related

@ element, deq, enq, get, let, the, with

## given

Creates an anonymous function.

##### Syntax
```

(given { parameter … } expression … )

parameter ::= required …

parameters ::= required … + optional …

parameters ::= \+ optional …

parameters ::= required … \+ optional … & remaining

parameters ::= & remaining

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| parameters | list | 1   | A list containing zero or more parameters and sigils |
| expression | variant | 0+  | Expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| anonym | Returns the anonym the expression represents. |

##### Remarks

An anonym is an anonymous function. An anonym is equivalent to lambda in the Lisp programming language, and can be used in most places a function name is required. Anonyms cannot be recursive, since they are unnamed. Continuations may be taken within an anonym. Neither do anonyms use tags that can be reference by a return. If no parameters are specified, then each expression is executed in succession and the value of the last expression is returned. If parameters are specified, then arguments must be provided in the invocation. Anonyms are ephemeral because function definitions are not maintained for them.

##### Example
```

> ((given {?s} (tell user ($ ?s \n))) "Hello, world.")

Hello, world.

.: told

> (map {One Two Three Four Five}

(given {?x} (tell user ($$ ?x "..." \n)))

One...

Two...

Three...

Four...

Five...

.: told

> (filter (range 1 to 40) (given {?n} (and (even-p ?n) (divisible-p ?n 7))))

.: {14 28}

```

##### Related

wait, abort, concurrent, await, complete, done-p, reclaim,task, use

## global

Creates global symbols.

##### Syntax
```

(global assignment … )

assignment ::= symbol value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assignment | expression | 1+  | A symbol value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates global symbols.

##### Example
```

> (global ?START_OF_TASK 1)

.: true

> (global ?FIRST_NAME "Jane"

?LAST_NAME "Smith"

)

.: true

```

##### Related

<-- before tie, --> after tie, constant, dynamic, local, let, modular, put, suppose, swap, undeclare

## globals

Creates a list of global symbols.

##### Syntax
```

(globals )

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| List | Returns of list of symbol value pairs. |

##### Remarks

Creates global symbols.

##### Example
```

> (global ?a foo ?b bar ?c baz)

.: true

> (globals)

.: {{?a foo} {?b bar} {?c baz}}

> (dynamic {?a 1000} (globals))

.: {{?a 1000} {?b bar} {?c baz}}

> (globals)

.: {{?a 1000} {?b bar} {?c baz}}

```

##### Related

<-- before tie, --> after tie, constant, dynamic, local, let, modular, put, suppose, swap, undeclare

## go

Transfers control to a function.

##### Syntax
```

(go function argument … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function. |
| argument | variant | 0+  | An argument to the function. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the result. |

##### Remarks

Transfers control to the specified function by unwinding the current function from the call graph then jumping to the specified function.

##### Example
```

> (relation Queue :Items {} :Capacity 100

!count (given {?me}(# (:Items ?me)))

!full-p (given {?me}(>= (!count ?me) (:Capacity ?me))))

.: Queue

> (function produce {?q}

(while (not (!full-p ?q))

(repeat (random 1 to (- (:Capacity ?q) (!count ?q)))

(enq ?q :Queue (new Item))))

(go consume ?q))

.: produce

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
```

(grok theory)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| theory | variant | 1   | A uniform resource locator or file resource. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last expression evaluated. |

##### Remarks

This function opens the url or file, and evaluates each expression therein.

##### Example
```

> (grok (file name "Module1.th"))

.: Module1

> (grok (url "file://MyCodeSite.com/Module2.theory"))

.: Module2

```

##### Related

eval, file, posit, url

## group

Combines sublists by position or key.

##### Syntax
```

(group list by key … into symbol expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| list | list | 1   | A list containing  sublists or tuples. |
| by | literal | 1   | The literal by. |
| keys | list | 1   | A list containing either slots, integer positions, or transform functions that return a value given an element of the list. |
| into | literal | 1   | The literal into. |
| symbol | symbol | 1   | A symbol storing each grouping. |
| expression | variant | 0+  | An expression to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of the last expression. |

##### Remarks

Each key is either a numeric position, slot or method name, or a transform function which when applied to a list element shall return a value. If as is not provided, then a list of the intermediate groupings is returned. If keyword as is provided, then the subsequent expressions shall have the grouping symbol available for evaluation and the final expression is collected into a list.

##### Example
```

> (group {{1 a b c}{2 b c a}{3 c a b}{4 a b c}{5 b c a}{6 c a b}} by {2 3} into ?g)

.: {{{1 a b c}{4 a b c}}{{2 b c a}{5 b c a}}{{3 c a b}{6 c a b}}}

> (group

{[Fruit :Color red :Name cherry][Fruit :Color red :Name apple]

[Fruit :Color red :Name tomato][Fruit :Color yellow :Name banana]}

by {:Color} into ?g

[R :Color (:Color (@ ?g)) :Count (# ?g)])

.: {[R :Color red :Count 3] [R :Color yellow :Count 1]}

```

##### Related

coalesce, collect, count, gather, given, separate, sort, with

## halt

Terminates a cell or bion.

##### Syntax
```

(halt compute)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| compute | compute | 1   | A cell or bion. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The literal halted. |

##### Remarks

This function starts an asynchronous agent task that processes incomingc messages and performs a default job.

##### Example
```

> (let ?url (url scheme tcp port 5001))

.: true

> (function reply {?sender ?message} (tell ?sender "OK"))

.: reply

> (function job {& ?args} (tell user ($ 1)) (wait 0.5))

.: job

> (agent ?url reply job)

.: Agent-1

> (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1)

111111.: cancelled freed

```

##### Related

bion, cell, free, task

## has

True if a key is present in an assortment.

##### Syntax
```

(has assortment key )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | A sequence or assortment |
| key | variant | 1   | A key. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the key is present. or false if the key is absent. |

##### Remarks

None

##### Example
```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.: Lexicon-1

> (has Lexicon-1 :C)

.: true

> (has Lexicon-1 !m)

.: true

> (has Lexicon-1 !q)

.: false

```

##### Related

beyond, lacks, within

## hash

Computes a hash code.

##### Syntax
```

(hash value option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| option | expression | 0+  | A key value pair size number - a hash table size (default 1000) seed number - a prime number seed. |

##### Results

| Taxon | Description |
| --- | --- |
| integer | The hash value |

##### Remarks

Returns a hash value between zero and the given size, based on the given prime number seed. The size and seed can be omitted.

##### Example
```

> (hash {a b c})

.: 822826764062

> (hash {a b c} size 100)

.: 62

> (hash {a b c} size 1000 prime 3)

.: 186

```

##### Related

array, collection, lexicon

## help

Describes a function.

##### Syntax
```

(help function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | literal | 0-1 | The name of a function. |

##### Results

| Taxon | Description |
| --- | --- |
| nil | Returns nil. |

##### Remarks

Prints the function documentation and returns nil.

##### Example
```

> (help)

Enter your code followed by a blank line. Type (help), (copyright) or (license)

for information. Type (grok (file "file.theory")) to read a file. Type (bye) to exit.

.: nil

> (help help)

(intrinsic KB.help {+ ?function}

Returns documentation about a function. If no function is provided, general help is displayed.

.: nil

```

##### Related

about, bye, copyright, license

## here

Adds symbols in parallel to the current environment.

##### Syntax
```

(here assignment ... )

assignment ::= symbol value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true |

##### Remarks

Concurrently creates symbols in the current environment. Each symbol shall replace any extant symbol with the same name in the current environment. Each symobl assignment occurs either in parallel with, or in isolation to, the other symbol assignments.

##### Example
```

> (assume ?start 1 ?end 100 ?range (range ?start to ?end))

.: true

> (undeclare {?start ?end ?range})

.: undeclared

> (here ?start 1 ?end 100 ?range (range ?start to ?end))

.: [Failure :Name UnboundSymbol :Text "The symbol ?start is unbound"]

> (do (here ?start 1 ?end 100)

(step ?i from ?start to ?end (do nothing)))

.: nothing

```

##### Related

<-- before tie, --> after tie, assume, constant, dynamic, given, global, local, put

## hyperlink

Creates a hyperlink.

##### Syntax
```

(hyperlink option … )

(hyperlink address)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| address | string | 0-1 | The url address. |
| option | expression | 0+  | A key value pair. One of user credentials \-user name and password host host \- host computer name (default is localhost) port number – a port number. (default is 2001) path path – a path query query – a query element fragment fragment – a fragment element |

##### Results

| Taxon | Description |
| --- | --- |
| service | A file resource |

##### Remarks

Returns a hyperlink.

##### Example
```

> (function reply {?target ?request} (tell ?target "goodbye."))

.: reply

> (service (assign ?service (hyperlink "http://localhost:4500/foxxy")) reply)

.: Service-1

> (ask ?service "hello")

.: "goodbye."

> (cancel Service-1) (free ?service) (free Service-1)

.: cancelled freed freed

```

##### Related

close, erase, path, pipe, read, socket, write

## id

Returns a resource number.

##### Syntax
```

(id resource )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| resource | resource | 1   | A resource. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The resource number or nil. |

##### Remarks

None

##### Example
```

> (new (relation Q))

.: Q_1

> (id Q_1)

.: 1

> (id [Q ^ Q_2])

.: 2

> (id file-27)

.: 27

> (id foo)

.: nil

```

##### Related

^ thought, id, uid, unique

## identical-p

True if all values occupies the same memory location.

##### Syntax
```

(identical-p value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | value | 2+  | Values to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are identical |

##### Remarks

Returns true if each value is identical to its successor from left to right, and false otherwise. All values must be of the same type, and must occupy the same address in memory. This function short circuits if false.

##### Example
```

> (identical-p a a a a)

.: true

> (identical-p a (clone a) a a)

.: false

> (identical-p "johnny" "ralph" "sam")

.: false

> (identical-p 3 3)

.: true

> (identical-p 3 (clone 3))

.: false

```

##### Related

< less , <= less or equal, > greater, >= greater or equal, /= unequal, canonify, identity

## identity

Returns the value itself.

##### Syntax
```

(identity value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | Any value |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the value. |

##### Remarks

None.

##### Example
```

> (identity a)

.: a

> (identity {a b c})

.: {a b c}

> (identity (++ 0))

.: 1

```

##### Related

canonify, identical-p

## idle

Pauses for a specified interval.

##### Syntax
```

(idle duration)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| duration | instant | 1   | The quantity of time to pause. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns ready |

##### Remarks

None

##### Example
```

> (idle 10s)

.: ready

```

##### Related

moment, seconds, tick

## if

Branched conditional evaluation.

##### Syntax
```

(if condition expression … or-clause … else-clause)

or-clause ::= or condition expression …

else-clause ::= else expression …

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| expression | expression | 1+  | Any expression |
| or-clause | expression | 0+  | The literal or followed by a condition and zero or more expressions. |
| else-clause | expression | 0-1 | The literal else followed by one or more expressions |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The last value of the executed clause or nil if no conditions were true and no else clause was provided. |

##### Remarks

None

##### Example
```

> (global ?N 100)

.: true

> (if (> ?N 100) over

or (< ?N 100) under

else exactly)

.: exactly

```

##### Related

and, case,either, not, or, unless

## imaginary

Converts a value to an imaginary number.

##### Syntax
```

(imaginary value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number or the literal minimum or maximum. |

##### Results

| Taxon | Description |
| --- | --- |
| integer | An integer number. |

##### Remarks

If the number cannot be converted to an imaginary number, the function fails. If the value is complex, then the imaginary portion is selected.

##### Example
```

> (imaginary {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (imaginary "a b c")

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (imaginary 500)

.: 500i

> (imaginary 500.1)

.: 500.1i

> (imaginary "-23.4")

.: -23.4i

```

##### Related

complex, integer, long, rational, real

## in

True if a value is in a sequence.

##### Syntax
```

(in value sequence option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |
| sequence | sequence | 1   | A sequence. |
| option | expression | 0-2 | A key value pair. Any of depth number \- Number or # (for any depth). Default is 1. transform function \- A function to transform the element.. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the value is in the sequence, false otherwise. |

##### Remarks

None.

##### Example
```

> (in d {a b c d e f g})

.: true

> (in "a" "cbazyx")

.: true

```

##### Related

beyond, includes, excludes, has, out, within

## includes

True if a value is in a sequence.

##### Syntax
```

(includes sequence element option … )

```
##### Module

KB

##### Parameters

None

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| element | variant | 1   | A value. |
| option | expression | 0-2 | A key value pair. Any of depth number \- Number or # (for any depth). Default is 1. transform function \- A function to transform the element. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the item is in the container. |

##### Remarks

If value and sequence are strings, then a string search is performed. If sequence is a list and depth is greater than one, then subsequences shall be checked for the value. A depth of # implies search to any depth.

##### Example
```

> (includes {a b c d e f g} d)

.: true

> (includes "cbazyx" "w")

.: false

> (includes "cbazyx" 25 transform (given {?c} (++ (- (unicode ?c) (unicode "a")))))

.: true

```

##### Related

excludes, in, out

## index

Creates an index on slots of a relation.

##### Syntax
```

(index relation slot … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| relation | literal | 1   | A meron. |
| slot | literal | 1+  | The name of a slot in the relation |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the index |

##### Remarks

Creates an index for the specified slots to expedite value retrieval.

##### Example
```

> (relation X :A :B :C)

.: X

> (index X :B)

.: X_Index_1

> (index X :A :B)

.: X_Index_2

> (new X :A 1 :B 2)

.: X_1

> (which X ^ as ?x :B 1 list ?x)

.: {X_1}

```

##### Related

drop, indices, relation

## indices

Returns a list of indices for a relation.

##### Syntax
```

(indices relation )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| relation | relation | 1   | A relation. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of indices associated with the relation. |

##### Remarks

None.

##### Example
```

> (relation X :A :B :C)

.: X

> (indices X)

.: {}

> (index X :B)

.: X_Index_1

> (index X :A :B)

.: X_Index_2

> (indices X)

.: {X_index_1 X_index_2}

> (drop (indices X))

.: 1

```

##### Related

drop, index, relation

## infix

Creates a new sequence with interposed delimeters.

##### Syntax
```

(infix sequence delimeter)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| delimeter | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list with delimeters between the elements |

##### Remarks

A delimeter is placed between each element. If the sequence is a string, the delimiter shall be converted into a string. If the sequence has less than two elements, no changes are made.

##### Example
```

> (infix {a b c d} \* )

.: {a \* b \* c \* d}

> (infix "abcd" ", ")

.: "a, b, c, d"

> (infix {} ",")

.: {}

> (infix "" ",")

.: ""

```

##### Related

$ concatenate, split

## inside

Creates an expression from a sequence or assortment.

##### Syntax
```

(inside value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A sequence, assortment, or expression. |

##### Results

| Taxon | Description |
| --- | --- |
| expression | returns the contents of the value as an expression. |

##### Remarks

If value is a sequence or assortment then the contents are returned as an expression, otherwise, an empty expression is returned.

##### Example
```

> (inside {the quick brown fox})

.: the quick brown fox

> (inside {})

.:

> (void-p (inside {}))

.: true

> (inside (lexicon 1 a 2 b 3 c 4 d))

.: 1 a 2 b 3 c 4 d

> (inside (collection 1 2 3 a b c))

.: 1 2 3 a b c

```

##### Related

& merge, && abridge, expression, is, list

## insert

Creates a new sequence by inserting values.

##### Syntax
```

(insert sequence position value … )

entry ::= value position

entry ::= alue

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| position | integer | 1   | The position to begin inserting the values. |
| value | variant | 1+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A new sequence. |

##### Remarks

This function creates a new sequence. To modify a sequence use the push function.

##### Example
```

> (insert "abcdef" 1 g)

.: "gabcdef"

> (insert "abcdef" # g)

.: "abcdefg"

> (insert {a b c} 1 d e f)

.: {d e f a b c}

> (insert "abc" 1 d e f)

.: "defabc"

```

##### Related

\# size, add, cut, deq, enq, get, key, keys, push, put, values, zap

## insort

Inserts a value into a sorted sequence.

##### Syntax
```

(insort sequence value option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| value | value | 1   | A value |
| option | expression | 0+  | A key value pair where the key is comparer function - a function returning &lt;, =, &gt; unique yes\|no - Allows duplicate values. Default yes. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The new sequence after insertion. |

##### Remarks

Inserts the item in sorted order in the sequence. If the sequence is a list and first element is a number then the list is kept numerically sorted, otherwise it is alphabetically sorted.

##### Example
```

> (insort {a b c d e x} q)

.: {a b c d e q x}

> (insort "abcde" "z")

.: "abcdez"

> (function desc {?x ?y}

(if (> ?x ?y) &lt; or (= ?x ?y) = else &gt;))

.: desc

> (insort {108 79 33} 84 comparer desc)

.: {108 84 79 33}

```

##### Related

insert

## instantiate

Creates an expression with premises in place of thoughts.

##### Syntax
```

(instantiate expression )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | A thought or a list containing thoughts. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list containing premises |

##### Remarks

Replaces thoughts with corresponding premises within the supplied expression.

##### Example
```

> (relation E :Value)

.: E

> (new E)

.: E_1

> (relation B :Slot)

.: B

> (new B)

.: B_1

> (instantiate {E_1 {:Foo {B_1 x}}})

.: {[E ^ E_1 :Value nil] {:Foo {[B ^ B_1 :Slot nil] x}}}

```

##### Related

^ thought, get, id,premise

## integer

Converts a value to an integer.

##### Syntax
```

(integer value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Taxon | Description |
| --- | --- |
| integer | An integer number. |

##### Remarks

If the value is minimum (or maximum) the minimum (or maximum) integer is returned; otherwise, if the value cannot be converted to an integer, the function fails. The fractional part of the number is truncated. An integer is a signed 64 bits number.

##### Example
```

> (integer {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (integer "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not a number."]

> (integer 500.3)

.: 500

> (integer "23.4")

.: 23

```

##### Related

ceiling, complex, floor, is, long, radix, rational, real, round, truncate, unsigned

## interleave

Interleaves arguments into a new sequence.

##### Syntax
```

(intersection sequence sequence … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | A sequence |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The interleaved sequence. |

##### Remarks

Returns a single sequence interleaving all sequences. if there are insufficient elements, NOTHING is supplied as the element. If the first element is not a sequence, then a list is treturned. The sequence type shall be that of the first element.

##### Example
```

> (interleave {1 2 3} {4 5 6} {7 8 9} {10})

.: {1 4 7 10 2 5 8 3 6 9}

> (interleave [1 2 3] [4 5 6] [7 8 9] [10])

.: [1 4 7 10 2 5 8 3 6 9]

> (interleave |1 2 3| |4 5| |6| |7 8 9| |10|)

.: |1 4 7 10 2 5 8 3 6 9|

> (interleave "abc" "def" "ghi" "j")

.: "adgjbehcfi"

```

##### Related

&& abridge, mid, insert, pop, push, swap, transfer

## intersection

Creates a sequence of common elements.

##### Syntax
```

(intersection sequence sequence … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | A list or string |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A list of common items |

##### Remarks

Returns the intersection of the provided sequences, i.e., the elements common to all sequences.

##### Example
```

> (intersection {1 2 3 4} {2 3 4 5)

.: {2 3 4}

> (intersection {2 3 4 5} {4 5 6 7})

.: {4 5}

> (intersection {1 2 3 4} {2 3 4 5} {3 4 5 6} {4 5 6 7})

.: {4}

> (intersection "abc" "bcd" "cde")

.: "c"

```

##### Related

common, difference, union

## intersects-p

True if any elements intersect.

##### Syntax
```

(intersects-p set1 set2 )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| set1 | sequence | 1   | A sequence. |
| set2 | sequence | 1   | A sequence |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the sets have any elements in common. |

##### Remarks

None.

##### Example
```

> (intersects-p {a b c d e f g} {a b x})

.: true

> (intersects-p {a b c d e f g} {a b d})

.: true

> (intersects-p "the quick brown" "ick bro")

.: true

> (intersects-p {a b c} {d e f})

.: false

> (intersects-p {1 2 3} {4 5 6})

.: false

```

##### Related

disjoint-p, subset-p

## interval

Creates a time interval.

##### Syntax
```

(interval start finish)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| start | time | 0-1 | A time value. (Default is neternity) |
| finish | time | 0-1 | A time value. (Default is eternity) |

##### Results

| Taxon | Description |
| --- | --- |
| interval | An interval. |

##### Remarks

If no parameters are provided, start shall default to negative eternity (neternity), and finish wil default to positive eternity. If only start is provided, finish shall default to positive eternity If finish is less than start, the positions shall be swapped so that start is always less than or equal to finish.

##### Example
```

> (interval 2014-01-01 2015-12-31)

.: 2014-01-01T00:00:00.000~2015-12-319T00:00:00.000

> (interval 2015000000000000m)

.: 2015000000000000m~eternity

> (interval 63573798191026000t neternity)

.: neternity~63573798191026000t

> (interval)

.: neternity~eternity

> (interval 600p 300p)

.: 300p~600p

```

##### Related

date, epoch, moment, seconds, tick

## into

Creates new thoughts based on existing thoughts.

##### Syntax
```

(into relation thoughts)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| relation | relation | 1   | A relation . |
| thoughts | list | 1   | A list of records. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the relation or structure. |

##### Remarks

If the thoughts contain slots that are in the relation, the slot values are copied to new thoughts.

##### Example
```

> (relation X :A :B :C)

.: X

> (repeat 10

(new X :A (random 1 to 100) :B (random 50 to 500) :C (random 0 to 1)))

.: X_10

> (into (relation Y uses {X}) (with X))

.: Y

> (which Y)

.: {Y_1 Y_2 Y_3 Y_4 Y_5 Y_6 Y_7 Y_8 Y_9 Y_10}

```

##### Related

knew, new

## invoke

Invokes a call.

##### Syntax
```

(invoke call environment)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| call | call | 1   | A call. |
| environment | environment | 0-1 | An environment (defaults to (scope)) |

##### Results

| Taxon | Description |
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

.: A

> (new A)

.: A_1

> (invoke (call !incr A_1) (scope))

.: 1

> (invoke (call !incr A_1) (scope))

.: 2

> (invoke (call @ "hello"))

.: "h"

```

##### Related

apply, call, closure, eval, function, macro, scope, supply

## is

Applies the predicate to the value returning true or false..

##### Syntax
```

(is value predicate)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| predicate | literal | 0-1 | a unary function returning true or fase. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is true, or if the applied unary predicate returns true. |

##### Remarks

None.

##### Example
```

> (is true)

.: true

> (is false)

.: false

> (is 41 even-p)

.: false

> (is 9 (given {?n} (divisible-p ?n 3)))

.: true

> (is foo null-p)

.: false

> (is nil null-p)

.: true

```

##### Related

convert, datatype, known, the, type

## junction

Creates a public function in a module with arguments evaluated in parallel.

##### Syntax
```

(junction scope name parameters expression … )

parameters ::=

parameters ::= { }

parameters ::= {required … }

parameters ::= {required … + optional … }

parameters ::= { \+ optional … }

parameters ::= {required … \+ optional … & remaining }

parameters ::= { & remaining }

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied then a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing symbols, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Junctions are defined using the junction intrinsic function. A junction is merely a function that evaluates all it’s arguments in parallel. A parallel argument evaluation the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example
```

> (junction {?n} (+ 1 ?n))

.: fn-1

> (junction plusN {?n + ?i = 1} (+ ?n ?i))

.: plusN

> (junction (scope) . addAll {& ?nums} (apply + ?nums))

.: addAll

> (fn-1 100)

.: 101

> (plusN 100)

.: 101

> (junction tryParseNum {String ?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

> (tryParseNum "foo")

.: {false nil}

> (tryParseNum "123")

.: {true 123}

> (junction dont {{try ?what} + {at ?where = nil}}

(apply (given {?s}(tell user ?s))

($ don't try ?what (unless (any ?where) "" ($ at ?where))))

.: dont

> (dont try "skydiving into a volcano")

don't try skydiving into a volcano

.: told

> (dont try this at home)

don't try this at home

.: told

```

##### Related

arguments, call, extend, functions, macro, module, modules, parameters

## key

Finds the key for a value in an assortment.

##### Syntax
```

(key assortment value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| value | variant | 1   | A value |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The key for the value. |

##### Remarks

If a key does not exist for the value, the function fails. It is advised to test whether the value exists in the assortment by first using the values function.

##### Example
```

> (assign ?s (lexicon a 1 b 2 c 3 d 4))

.: Lexicon-1

> (values ?s)

.: {1 2 3 4}

> (keys ?s)

.: {a b c d}

> (key ?s 4)

.: d

> (key ?s 5)

.: [Failure :Name NotFound "The value 5 was not found in the assortment."]

```

##### Related

@ element, position, values

## keys

Returns a list of keys for an assortment.

##### Syntax
```

(keys assortment )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of values |

##### Remarks

All keys from the assortment are returned in a list.

##### Example
```

> (assign ?s (lexicon a 1 b 2 c 3 d 4))

.: Lexicon-1

> (values ?s)

.: {1 2 3 4}

> (keys ?s)

.: {a b c d}

> (key ?s 4)

.: d

> (key ?s 5)

.: [Failure :Name NotFound :Text "The value 5 was not in the assortment."]

```

##### Related

key, values

## keywords

Returns the list of Premise keywords.

##### Syntax
```

(keywords)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is a keyword. |

##### Remarks

None.

##### Example
```

> (keywords)

.: {eternity infinity neternity ninfinity unknown}

```

##### Related

is

## knew

Finds or creates a thought.

##### Syntax
```

(knew relation criterion … )

criterion ::= slot referent

criterion ::= method function

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| relation | relation | 1   | The name of the relation to find |
| criterion | expression | 0+  | A slot referent pair or method function pair. |

##### Results

| Taxon | Description |
| --- | --- |
| thought | A known or new thought. |

##### Remarks

Looks for an existing thought that matches the criteria and returns the first match. If no thought matches the criteria, a new thought is created using the criteria.

##### Example
```

> (relation Pairs :A :B)

.: Idea

> (knew Pairs :A 1 :B 2)

.: Pairs_1

> (knew Pairs :A 1)

.: Pairs_1

> (knew Pairs :B 3)

.: Pairs_2

```

##### Related

new, relation

## knowledge

Finds or creates a knowledge base.

##### Syntax
```

(knowledge option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 0+  | Key value pair. Any of the following name name \- A literal to identify the knowlebge base. Options for constructing a local knowledge base path string \- the local path (required if constructing). unit literal \- either TB, GB, MB (default) size real \- the initial knowledge base (default is 5). max real \- maximum kb size (default is nil) log real \- initial log size. (default is 2). growth real \- Resize percentage (default is 10). Options for connecting to an existing knowledge base connect string - use the specified connection string. poolsize integer \- maximum # of connections provider literal - either mssql, odbc, maria, pgsql Options for building the connection string from elements. driver string - the driver server string \- server address version number - server version class class - class name of driver host address \- host address port port \- server port for database service instance instance \- server instance name integratedSecurity truth \- true or false database name - database name user username - user name password password - user password trusted yesorno - trusted connection yes or no. source name - data source name protocol protocol - database protocol subprotocol subprotocol - database sub protocol subname subname - sub name |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the new knowledge base. |

##### Remarks

If path is provided, then name is required. If data is provided then a knowledge base must already exist at the specified data url.

##### Example
```

> (knowledge provider mssql connect "Data Source=MYHOST\\SERVER; Initial Catalog=MyKB; Integrated Security=SSPI;")

.: Knowledge-1

> (knowledge name Mathematics path "c:/premise/kb/" units MB size 2 max 10

log 1 growth 10)

.: Mathematics

```

##### Related

attach, conceive, detach, each, eradicate, knew, knowing, new, relation, which, with

## known

True if a thought pattern matches.

##### Syntax
```

(known pattern … option … )

pattern ::= [relation clause …]

clause ::= slot referent

clause ::= slot is unary-predicate

clause ::= slot not referent

clause ::= slot binary-predicate referent

clause ::= slot n-ary-predicate referent-list

clause ::= method function

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| pattern | expression | 0+  | A relation clause pattern enclosed in square brackets. |
| option | expression | 0-2 | Key value pairs: limit number - maximum number of thoughts to match. scan number - maximum number of thoughts to search. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns whether any thoughts matched. |

##### Remarks

Looks for existing thoughts matching the criteria.

##### Example
```

> (relation Pairs :A :B)

.: Pairs

> (new Pairs :A 1 :B 2)(new Pairs :A 3 :B 4)(new Pairs :A 5 :B 2)

.: Pairs_1 Pairs_2 Pairs_3

> (known [Pairs :B 2] limit 1)

.: true

```

##### Related

knew, new, relation, the, with

## lacks

True if a key is absent from an assortment.

##### Syntax
```

(lacks assortment key )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| key | variant | 1   | A key. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the key is absent or false if the key is present. |

##### Remarks

None

##### Example
```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.: Lexicon-1

> (lacks Lexicon-1 :C)

.: false

> (lacks Lexicon-1 !m)

.: false

> (lacks Lexicon-1 !q)

.: true

```

##### Related

beyond, has, within

## last

Creates a subsequence of the last elements.

##### Syntax
```

(last sequence count)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |
| count | number | 0-1 | The number of elements to return. Default is 1. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The selected sub sequence |

##### Remarks

None

##### Example
```

> (last {a b c})

.: {c}

> (last {a b c d e f} 3)

.: {d e f}

> (last "abcde" 2)

.: "de"

```

##### Related

but, rest, top

## left

True if values are equal or the second value is nil.

##### Syntax
```

(left first second )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| first | variant | 1   | A value to be compared. |
| second | variant | 1   | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are the same or if second is nil |

##### Remarks

Returns true if each value is the same or if the second value is nil, and false otherwise. Both values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equal if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical). Returns false if both values are false.

##### Example
```

> (left a a)

.: true

> (left "johnny" "ralph")

.: false

> (left 3 nil)

.: true

> (left nil 4)

.: false

```

##### Related

< less , <= less or equal, > greater, >= greater or equal, /= unequal, full, identical, right

## let

Adds symbols to the current environment.

##### Syntax
```

(let manner assignment ... )

assignment ::= symbol value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| Truth | Returns true. |

##### Remarks

Sequentially creates symbols in the current environment. Each symbol shall replace any extant symbol with the same name in the environment. . If parallel is specified as the manner, the symbols are defined in parallel, otherwise the symbols are assigned in tandem (by default).

##### Example
```

> (let ?person DrWho)

.: true

> ?person

.: DrWho

> (let parallel ?x 1 ?y 2 ?z 3)

.: true

```

##### Related

<-- before tie, --> after tie, constant, dynamic, fix, global, local, set, tie, presume

## lexemes

Creates an uppercase string with spaces between words.

##### Syntax
```

(lexemes string)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A string to be converted |

##### Results

| Taxon | Description |
| --- | --- |
| string | A converted string. |

##### Remarks

Converts a string to uppercase with a single space between alphanumeric words. Removes punctuation.

##### Example
```

> (lexemes "The quick brown fox!! ")

.: "THE QUICK BROWN FOX"

```

##### Related

char, format, lexemes, like, lowercase, ngrams, split, trim, unlike, unicode, uppercase

## lexicon

Creates a lexicon.

##### Syntax
```

(lexicon association … )

association ::= key value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| association | expression | 0+  | A key and a value. |

##### Results

| Taxon | Description |
| --- | --- |
| lexicon | The newly created lexicon. |

##### Remarks

None.

##### Example
```

> (lexicon {a b c} "foo 123" bar "bar 456" baz (lexicon))

.: Lexicon-2

> (keys Lexicon-2)

.: {{a b c} bar baz}

> (values Lexicon-2)

.: {"foo 123" "bar 456" Lexicon-1}

> (@ Lexicon-2 {a b c})

.: "foo 123"

> (key Lexicon-2 Lexicon-1)

.: baz

```

##### Related

lexicon

## lexicons

Creates a list of all lexicons.

##### Syntax
```

(lexicons)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list of lexicons. |

##### Remarks

None.

##### Example
```

> (lexicons)

.: {}

> (lexicon k1 v1 k2 v2)

.: Lexicon-1

> (lexicons)

.: {Lexicon-1}

```

##### Related

lexicon

## license

Prints the software license.

##### Syntax
```

(license)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| nil | nil |

##### Remarks

None.

##### Example
```

> (license)

Premise Community Edition

Copyright (c) 2013-2020 Michael S. P. Miller. All Rights Reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of the Community edition of the software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

.: nil

```

##### Related

about, bye, copyright

## like

Compares a pattern to a sequence.

##### Syntax
```

(like sequence pattern )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A string or list of strings to be compared. |
| pattern | string | 1   | A regex pattern. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | If sequence is a string, then a truth is returned. If sequence is a list, then a list of matches is returned |

##### Remarks

If the sequence is a list, then this function Creates a new list containing only those elements matching the pattern. If the sequence is a string, then this function returns true if the pattern matches the candidate, and false otherwise. Standard regular expression matching is used.

##### Example
```

> (like "abc" "bc")

.: true

> (like "abc" "[xy]")

.: false

> (like {"abc" "def" "xyz" "wxy"} "xy")

.: {"xyz" "wxy"}

```

##### Related

unlike

## list

Creates a list.

##### Syntax
```

(list value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | Any value |

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list containing the values. |

##### Remarks

A list can also be created by simply enclosing the elements with curly braces, {}.

##### Example
```

> (list a b c {d})

.: {a b c {d}}

> (list "a b c")

.: {"a b c"}

> (list 500)

.: {500}

> (list foo)

.: {foo}

> {a b c {d}}

.: {a b c {d}}

> {"a b c"}

.: {"a b c"}

```

##### Related

& merge, && abridge, inside, vector

## literal

Creates a literal.

##### Syntax
```

(literal value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A string or literal to be converted. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | A literal. |

##### Remarks

Only strings or literals can be converted to a literal. sequences, numbers and symbols cannot be converted to literals. This function fails if the value cannot be converted.

##### Example
```

> (literal abc)

.: abc

> (literal 500)

.: [Failure :Name ArgumentValue :Text "Cannot convert '500' to a literal."]

> (literal "500")

.: [Failure :Name ArgumentValue :Text "Cannot convert '500' to a literal."]

> (literal "foo")

.: foo

> (literal (symbol bar))

.: [Failure :Name ArgumentValue :Text "Cannot convert '?bar' to a literal."]

```

##### Related

is

## local

Creates a task level scope.

##### Syntax
```

(local assignments expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assignments | list | 1   | A list of symbol value pairs |
| expression | variant | 0+  | An expression |

##### Results

| Taxon | Description |
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

.: appendToFile

```

##### Related

<-- before tie, --> after tie, constant, dynamic, given, global, only, set

## location

Sets a symbol to the current location.

##### Syntax
```

(location symbol )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol to contain the location. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result value. |

##### Remarks

This function saves the present program location in a symbol. A subsequent resume call shall reset the location to the one in the symbol for the program control to resume at the location.

##### Example
```

> (function makeSandwich {?where}

(tell user "Made a sandwich.\n")

(proceed ?where set ?sandwich made))

.: makeSandwich

> (function eatSandwich

(tell user "Ate the sandwich.\n"))

.: eatSandwich

> (do

(let ?sandwich none)

(location ?kitchen)

(if (= ?sandwich made)

(eatSandwich)

else

(makeSandwich ?kitchen)))

Made a sandwich.

Ate the sandwich.

.: told

```

##### Related

resume, go

## log

Logarithm.

##### Syntax
```

(log number base)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| base | number | 1   | The base. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The logarithm |

##### Remarks

Returns the logarithm of the number for a base.

##### Example
```

> (log 100 10)

.: 2

> (log 27 3)

.: 3

> (log 22026.31763368418 (e))

.: 10

```

##### Related

\*\* exponentiation

## long

Converts a value to a long number.

##### Syntax
```

(long value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Taxon | Description |
| --- | --- |
| long | An long number. |

##### Remarks

A long is a signed 128 bit number. If the value is minimum (or maximum) the minimum (or maximum) monadic is returned; otherwise, if the value cannot be converted to a monadic, the function fails. The fractional part of the number is truncated. The suffix n denotes a long number.

##### Example
```

> (long {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (long "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not a number."]

> (long 500)

.: 500n

> (long 500.0)

.: 500n

> (long "23.4")

.: 23n

```

##### Related

big, integer

## loop

Repeatedly evaluates expressions.

##### Syntax
```

(loop expression … gate )

gate ::= repeat integer

gate ::= until truth

gate ::= while truth

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 0+  | Expressions to be evaluated. |
| gate | expression | 1   | the literal while or until followed by a truth expression, or the literal repeat followed by an integer. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the value of the last executed expression before the gate. |

##### Remarks

Each expression is executed in succession and the value of the last expression before te gate is returned. This function repeats the expression(s) according to the gate. If until is specified, the iteration fails when the condition becomes true. If while is specified, the iteration fails when the condition becomes false. If repeat and an integer value is specified as the gate, then the iteration repeats for the number of times in the integer value. The gate may be omitted to iterate only once.

##### Example
```

> (loop (--> ++ ?i) while (< ?i 10))

.: 10

> (loop (--> -- ?i) until (< ?i 1))

.: 0

> (loop (--> ++ ?i) repeat 10)

.: 10

```

##### Related

wait, abort,, await, complete, done-p, reclaim, use, for, iterate, loop, step, task, until, while

## lowercase

Converts a string to lower case.

##### Syntax
```

(lowercase string)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A string |

##### Results

| Taxon | Description |
| --- | --- |
| string | The lower cased string |

##### Remarks

None

##### Example
```

> (lowercase "The Quick BROWN fox")

.: "the quick brown fox"

```

##### Related

capitalize, uppercase

## lowercase-p

Returns true if a string's first position is lower case.

##### Syntax
```

(lowercase-p value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the first position is lowercase. |

##### Remarks

None

##### Example
```

> (lowercase-p "the quick brown fox")

.: true

> (lowercase-p "This and that")

.: false

```

##### Related

letter-p, lowercase-p, uppercase-p, whitespace-p

## macro

Creates a macro.

##### Syntax
```

(macro name parameters expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | A macro name |
| parameters | list | 1   | A parameter list |
| expression | variant | 1+  | Forms to be evaluated |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last value in the list of frames |

##### Remarks

A macro is a function whose parameters are unevaluated. To evaluate any of the parameters, the eval function must explicity be called on that parameter.

##### Example
```

> (macro set2 {?value ?var1 ?var2}

"puts value into two variables in parallel"

(eval (\` (set , ?var1 , ?value , ?var2 , ?value))))

.: set2

> (let ?x1 nil ?x2 nil) ?x1 ?x2

.: true nil nil

(set2 (+ 2 2) ?x1 ?x2)

> ?x1 ?x2

.: 4 4

```

##### Related

evaluate, function, ' quote, \` expand

## macros

Creates a list of macros defined in a module.

##### Syntax
```

(macros module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A valid module name. Defaults to the current module. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of macros defined in the module. |

##### Remarks

##### None.

##### Example
```

> (macro set2 {?s1 ?s2 ?value}

(eval (\` (set , ?s1 , ?value , ?s2 , ?value))))

.: set2

> (macros)

.: {set2}

```

##### Related

\` expand, ' quote, eval, functions, is, macro

## make

Creates a record by creating a relationship if it does not already exist.

##### Syntax
```

(make prototype term … )

term ::= slot referent

term ::= method function

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| prototype | prototype | 1   | A relation or structure. |
| term | expression | 0+  | A slot and a referent, or method and function. |

##### Results

| Taxon | Description |
| --- | --- |
| identifier | The identifier of the premise |

##### Remarks

If the prototype is a relation which has has an !onNew method defined, the method shall be invoked once during thought creation, before the thought identifier is returned to the calling function. If the relationship is new, the referents and functions shall serve as defaults for the relationship.

##### Example
```

> (make Employee :Name "John Smith" :Salary 225000

!onNew (function Employee_new {?me}

(tell user ($ Emp - ($$ (:Name ?me),)

Pay - (:Salary ?me) \n \n)))))

Emp - John Smith, Pay – 225000

.: Employee_1

```

##### Related

nix, old, relation, seal, unseal

## map

Applies a function to elements across sequences.

##### Syntax
```

(map sequence ... function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1+  | A sequence of values |
| function | variant | 1   | The name of the function to invoke |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The sequence resulting from applying the function to all sequences. |

##### Remarks

Applies the argument to a list containing values and returns the results.

##### Example
```

> (map {1 2 3} {4 5 6} {7 8 9} +)

.: {12 15 18}

> (map {1 2 3} even-p)

.: {false true false}

> (map {10 20 30} {3 4 5} \*)

.: {30 80 150}

```

##### Related

apply, collect, count, each, filter, fold, gather, group, merge, reduce , scale , separate, sort

## max

Finds the maximum element.

##### Syntax
```

(max value … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A sequence, or an atomic value. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The largest element in the sequence. |

##### Remarks

Returns the maximum element in a list or expression. If the list or expression is empty, it returns nil. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example
```

> (max {1 2 3 4 5})

.: 5

> (max {a b c d e})

.: e

> (max {})

.: nil

  
> (max 1 2 3 4 5)

.: 5

> (max {1 2 3} 4 {6 3 2})

.: {6 4 4}

```

##### Related

choose, min

## maximum

Finds the maximum element.

##### Syntax
```

(maximum symbol … binding sequence expression … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result of applying the max function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the symbols then the function fails. The last expression shall be evaluated and the maximum function shall be applied to both that expression and any prior result. The final value is returned.

##### Example
```

> (maximum ?x in (range 1 to 10) ?x)

.: 10

> (maximum ?x in {1 2 3 4} (\*\* ?x 2))

.: 16

> (maximum ?x ?y per {{a 1}{b 2}{c 3}} ?x)

.: c

```

##### Related

fold, minimum, product, summation

## may

Evaluates an expression while surpressing failures.

##### Syntax
```

(may expression )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 1   | An expression to evaluate. |

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list containing a truth success value, the result, and possible failure. |

##### Remarks

If the expression fails, the result shall be nil.

##### Example
```

> (may (string x))

.: {true "x" nil}

> (may (integer x))

.: {false nil [Failure :Name TypeConversion :Text "Cannot convert x to Integer"]}

> (let {?success ?result ?error} (may ($ hello world)))

.: true

> ?success ?result ?error

.: true "hello world" nil

```

##### Related

assert, can, did, ensure, fail, finally, try

## median

Finds the middle value of a sequence.

##### Syntax
```

(median value …)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The median value of all elements. |

##### Remarks

Returns the median. If the list or expression is empty, it returns nil. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example
```

> (median {1 2 3 4 5})

.: 3

> (median {})

.: nil

> (median 1 2 3 4 5)

.: 3

> (median {1 2 3} 4 {6 3 2})

.: {4 3 3}

```

##### Related

avg, max, median, min, statistics, sigma, sum

## meets-p

True if an interval finishes when a second interval starts.

##### Syntax
```

(meets-p interval<sub>1</sub> interval<sub>2</sub> tolerance)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if interval1 finishes when interval2 starts. |

##### Remarks

None.

##### Example
```

> (meets-p 1s~2s 3s~4s)

.: false

> (meets-p 1s~5s 5s~8s)

.: true

> (meets-p 1s~9s 4s~6s)

.: false

> (meets-p 4s~6s 6s~9s)

.: true

> (meets-p 5s~6s 8s~9s 2s)

.: true

```

##### Related

before-p, during-p, finishes-p, overlaps-p, starts-p

## meron

Returns the meronomic (i.e., proto) type of a value.

##### Syntax
```

(meron value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A structure, relation, or premise |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The meronomic prototype of the relation |

##### Remarks

None

##### Example
```

> (meron (relation A))

.: A

> (meron (new (structure B :Slot1 :Slot2)))

.: B

> (meron 100)

.: nil

> (meron foo)

.: nil

> (meron (new (relation C uses {A B})))

> C

> (meron [D :Foo 1 :Bar 2])

> D

```

##### Related

id, is, meronomy,, taxon, taxonomy

## meron-p

True if the value isa meron or is of a specific meronomic type.

##### Syntax
```

(meron-p value meron)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |
| meron | literal | 0-1 | The name of a meronomic type. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is a meron or is of a specific meronomic type.. |

##### Remarks

If the meron parameter is omitted, the functon returns true if the value is a meron. Otherwise, the function returns true if the value is of the specified meronomic type. .

##### Example
```

> (meron-p 500)

.: false

> (relation A :S1 :S2 0) (relation B uses {A} :S3 100)

.: A B

> (meron-p (new A))

.: true

> (meron-p (new B) A)

.: true

```

##### Related

meron, meronomy, taxon, taxon-p, taxonomy

## meronomy

Returns a list of meronomic (i.e., proto) types for a value.

##### Syntax
```

(meronomy value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |

##### Results

| Taxon | Description |
| --- | --- |
| list | The meronomic types used |

##### Remarks

The value must be a premise, prototype, or record , otherwise an empty list is returned

##### Example
```

> (meronomy 100)

.: {}

> (meronomy donut)

.: {}

> (relation C uses {(relation A) (relation B)})

.: C

> (meronomy (new C))

.: {C A B}

> (meronomy A)

.: {A}

```

##### Related

taxon,taxonomy, id, is, meron, relation, structure

## method

Creates a function within a prototype.

##### Syntax
```

(method scope name parameters expression … )

parameters ::=

parameters ::= { }

parameters ::= {required … }

parameters ::= {required … + optional … }

parameters ::= { \+ optional … }

parameters ::= {required … \+ optional … & remaining }

parameters ::= { & remaining }

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| scope | environment | 0-1 | An environment. If not supplied, a new one is made. |
| name | literal | 0-1 | The name of the function. If not supplied then the name shall follow the pattern fn-&lt;number&gt;. |
| parameters | list | 0-1 | A list containing symbols, keywords, sigils, and keyword symbol associations. |
| expression | variant | 1+  | One or more expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the function |

##### Remarks

Methods are defined using the method intrinsic function. If the name is supplied then the method is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined. A hidden variant parameter ?me is supplied as the first parameter to the method function and is available within the method for reading. It may not be upadted or changed in the scope of the method.

##### Example
```

> (relation Context_Items

:Lexicon

:Item )

.: Context_Item

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

.: MyLexicon

> (structure IMonsterTask

:Name

!setInfo

!setRoomTask

:RoomTask

!kill )

.: IMonstertask

> (structure MonsterTask

uses {IMonsterTask}

:MonsterInfo (new MonsterInfo)

!onActivate (method {truth ?cancelled}

(put ?me :Id (!getPrimaryKey ?me))

(registerTimer move nil (interval 150s 9000s))

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

(return (tell User ($ (!name (:MonsterInfo ?me)) is already dead. \n

You were too slow and someone else got to

him.)))))

.: MonsterTask

```

##### Related

arguments, call, extend, functions, junction, macro, module, modules, parameters

## mid

Copies a subsequence of a sequence.

##### Syntax
```

(mid sequence start distance )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | sequence |
| start | number | 1   | Starting position |
| distance | expression | 1   | One of to finish or go count |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The sub-sequence |

##### Remarks

The end value must be greater than the start value.

##### Example
```

> (mid {a b c d} 2 to 3)

.: {b c}

> (mid "abcdefg" 4 go 4)

.: "defg"

> (mid "abcdefg" 2 to 4)

.: "bcd"

> (mid "abcdefg" 2 go 3)

.: "bcd"

```

##### Related

but, last, rest, top

## min

Finds the minimum element.

##### Syntax
```

(min value … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | An atom or list of atoms. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The smallest element in the sequence. |

##### Remarks

Returns the minimum element in a list or expression. If the list or expression is empty, it returns nil. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example
```

> (min {1 2 3 4 5})

.: 1

> (min {a b c d e})

.: a

> (min {})

.: nil

  
> (min 1 2 3 4 5)

.: 1

> (min {1 2 3} 4 {6 3 2})

.: {1 2 2}

```

##### Related

choose, max

## minimum

Finds the minimum element.

##### Syntax
```

(minimum symbol … binding sequence expression … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result of applying the plus function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the symbols then the function fails. The last expression shall be evaluated and the minimum function shall be applied to both that expression and any prior result. The final value is returned.

##### Example
```

> (minimum ?x in (range 1 to 10) ?x)

.: 1

> (minimum ?x in {1 2 3 4} (\*\* ?x 2))

.: 1

> (maximum ?x ?y per {{a 1}{b 2}{c 3}} ?x)

.: a

```

##### Related

fold, maximum, minimum, product

## missing

True if a value is absent from an assortment.

##### Syntax
```

(missing assortment key )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| vaue | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the value is absent or false if the value is present. |

##### Remarks

None

##### Example
```

> (lexicon :A 1 :B 2 !m X_foo :C 3)

.: Lexicon-1

> (missing Lexicon-1 3)

.: false

> (missing Lexicon-1 X_foo)

.: false

> (missing Lexicon-1 elephant)

.: true

```

##### Related

beyond, has, within

## mod

Finds the remainder after division.

##### Syntax
```

(mod dividend modulus)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| dividend | variant | 1   | A number or list of numbers. |
| modulus | variant | 1   | A number or list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | the remainder after dividing dividend by divisor as a number or list of remainders. |

##### Remarks

Returns the remainder of the dividend divided by the modulus. Both values must be numbers or lists. If each argument is a list, they must be the same length.

##### Example
```

> (mod 28 3)

.: 1

> (mod {6 8 9 2} 2)

.: {0 0 1 0}

> (mod 17 {5 6 3 4})

.: {2 5 2 1}

> (mod {12 45 8 17} {5 5 3 7})

.: {2 0 2 3}

```

##### Related

/ division, \* multiplication

## modular

Evaluates expressions within a module's scope.

##### Syntax
```

(modular module expression … )

assignment ::= symbol value expression

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | Literal | 1   | A module name |
| expression | variant | 1+  | An expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns the value true. |

##### Remarks

Creates module level symbols.

##### Example
```

> (modular User (let ?START_OF_TASK 1))

.: true

> (modular Business

(let ?FIRST_NAME Jane

?LAST_NAME Smith))

.: true

```

##### Related

<-- before tie, --> after tie, constant, dynamic, local, put, suppose, swap, undefine, use

## module

Creates a module.

##### Syntax
```

(module name definition … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | A module name |
| definition | expression | 0+  | A function, macro, or relation definition call |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the module. |

##### Remarks

Shall create a new module or redefine an existing module. To add definitions to an existing module use the extend function. To prohibit new definitions in a module use the wrap function. Each module is global, this means that nested module definitions do not concatenate.

##### Example
```

> (module Algebra

(function sum ?args (apply + ?args)))

.: Algebra

> (module Outer

(module Inner

(function Which {} One) ; the function shall be Inner.Which

)

)

.: Outer

> (Inner.Which)

.: One

```

##### Related

dependencies, discard, extend, forgo, modules, require, grok, unwrap, use, wrap

## modules

Creates a list of known modules.

##### Syntax
```

(modules)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of all modules |

##### Remarks

Returns the list of known modules.

##### Example
```

> (modules)

.: {DB IO KB Math Meta Tasks User}

```

##### Related

dependencies, discard, extend, forgo, module, require, grok, unwrap, use, wrap

## moment

Creates a moment or returns the current moment.

##### Syntax
```

(moment units secs mins hours days year )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| units | number | 0-1 | Units. Up to three digits for milliseconds. |
| secs | number | 0-1 | Two digits: e.g., (seconds / 60) \* 100 |
| min | number | 0-1 | Two digits: e.g., (minutes / 60) \* 100 |
| hour | number | 0-1 | Two digits: e.g., (hour / 24) \* 100 |
| days | number | 0-1 | Three digits e.g. (day of year / 365.25) x 1000 |
| year | variant | 0-1 | Four digits for year (e.g. 2015, 2017, 2018, 2025) |

##### Results

| Taxon | Description |
| --- | --- |
| moment | The current moment in nano years |

##### Remarks

If no arguments are supplied, moment returns the current time as a moment, otherwise it attempts to construct a moment from the supplied arguments.

##### Example
```

> (moment)

.: 2018270038501744m

> (moment 3000)

.: 3000m

> (moment 0 0 0 0 0 2020)

.: 2020000000000000m

> (moment 0 0 0 (time hour part 18) (time days part 182) 2027)

.: 2027499030000000m

```

##### Related

date, epoch, tick

## more-p

True if a container contains more than zero elements.

##### Syntax
```

(more-p sequence)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the container contains more than zero elements. |

##### Remarks

None.

##### Example
```

> (more-p "not empty")

.: true

> (more-p (call pi))

.: true

> (more-p "")

.: false

> (more-p {})

.: false

> (more-p [A])

.: true

> (more-p (expression foo))

.: true

```

##### Related

void-p

## morph

Applies functions in succession using the arguments.

##### Syntax
```

(morph arguments functions)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| arguments | list | 1   | The intial arguments to the last function in the functions list. |
| functions | list | 1   | An ordered list of functions to be applied. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The result of the application of the last function. |

##### Remarks

If the arguments parameter is an empty list, the leftmost function is assumed to be niladic (requiring no arguments). The leftmost function is applied to the arguments parameter list, then the second from leftmost is applied to the result, and so on, until all functions are applied. The final result is returned. The opposite function is compose. The scatter function applies functions in parallel.

##### Example
```

> (morph {0} {++ ++ ++ (given {?n} (\* ?n 2))})

.: 6

> (morph {{the quick brown fox jumped over the lazy dogs}}

{but rest but rest})

.: {brown fox jumped over the}

> (morph {2 3 4} {+ ++ ++ (given {?n} (\* ?n 2))})

.: 22

```

##### Related

apply, compose, map, scatter

## most

True if the predicate is true for more than half of the elements in a sequence.

##### Syntax
```

(most symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if more than half the elements satisfies the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated.

##### Example
```

> (most ?n in {1 2 3 4} (= (taxon ?n) number))

.: true

> (most ?m ?n per {{2 1} {3 4} {7 9}} (< ?m ?n))

.: true

> (most ?m ?n over {4 3 2 7} (divisible-p ?m ?n))

.: false

```

##### Related

every, few, nevery, none, some

## move

Moves or renames one or more files.

##### Syntax
```

(move source destination)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| source | url | 1   | The source url |
| destination | url | 1   | The destination url |

##### Results

| Taxon | Description |
| --- | --- |
| list | A possibly empty list of file path strings for each file moved. |

##### Remarks

If the path is invalid, the function fails.

##### Example
```

> (move (url path "foo.txt") (url path "bar.txt"))

.: {"bar.txt"}

```

##### Related

close, mkdir, file, path, write

## my

Returns the current cell resource.

##### Syntax
```

(my)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| cell | The cell resource for the performing functions. |

##### Remarks

None.

##### Example
```

> (my)

.: Cell-0

> (get (my) :Self)

.: Task-0

```

##### Related

premise, self

## nall

True if not all relevant knwledege satisfies all the premises.

##### Syntax
```

(nall premise … )

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot is unary-predicate

condition ::= slot not value

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| premise | variant | 1+  | A pattern, call, or truth value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if not all values return true. |

##### Remarks

True if any value is nil. Terminates on the first nil value. If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.

##### Example
```

> (nall grapefruit nil apple)

.: true

> (nall nil nil)

.: true

> (nall nil)

.: true

> (nall foo)

.: false

```

##### Related

all, any, no

## nand

Negated logical conjunction.

##### Syntax
```

(nand truth truth … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | truth | 2+  | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if any argument value is false |

##### Remarks

Equivalent to (not (and truth …)).

##### Example
```

> (nand true true true false)

.: true

> (nand true true true true)

.: false

```

##### Related

and, is, nor, not, or, xor

## negative-p

True if a number is negative.

##### Syntax
```

(negative-p number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the number is less than zero. |

##### Remarks

None.

##### Example
```

> (negative-p 500)

.: false

> (negative-p 0)

.: false

> (negative-p -25)

.: true

```

##### Related

even-p, odd-p, positive-p, zero-p

## nevery

True if the predicate is false for any element in the sequence.

##### Syntax
```

(nevery symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if any element does not satisfy the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example
```

> (nevery ?n in {1 a 3 4} (= (taxon ?n) number))

.: true

> (nevery ?m ?n per {{1 2} {3 4}} (> ?m ?n))

.: true

> (nevery ?m ?n over {4 2 1} (divisible-p ?m ?n))

.: false

```

##### Related

every, few, most, none, some

## new

Creates a record.

##### Syntax
```

(new prototype term … )

term ::= slot referent

term ::= method function

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| prototype | prototype | 1   | A relation or structure. |
| term | expression | 0+  | A slot and a referent, or method and function. |

##### Results

| Taxon | Description |
| --- | --- |
| identifier | The identifier of the premise |

##### Remarks

If the prototype is a relation which has has an !onNew method defined, the method shall be invoked once during thought creation, before the thought identifier is returned to the calling function.

##### Example
```

> (relation Employee :Name :Salary

!onNew (function Employee_new {?me}

(tell user ($ Emp - ($$ (:Name ?me),)

Pay - (:Salary ?me) \n \n)))))

.: Employee

> (new Employee :Name "John Smith" :Salary 225000)

Emp - John Smith, Pay – 225000

.: Employee_1

```

##### Related

nix, old, relation, seal, unseal

## next

Advances a series to the next element.

##### Syntax
```

(next series)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| series | series | 1   | A series. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the next item in the iteration can be accessed. |

##### Remarks

None.

##### Example
```

> (function walk {?iterable}

(let ?series (series ?iterable))

(while (next ?series)

(tell user ($ Found ($$ (this ?series) .) \n)))

walked)

.: walk

> (walk {a b c})

Found a.

Found b.

Found c.

.: walked

> (walk (lexicon a 1 b 2 c 3))

Found {a 1}.

Found {b 2}.

Found {c 3}.

.: walked

```

##### Related

reset, series, this

## ngrams

Creates a list of substrings.

##### Syntax
```

(ngrams string length)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A target string |
| length | integer | 0-1 | The length of substrings to find. (Default is 3.) |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of strings of the specified length |

##### Remarks

Affixes spaces before and after the string, then divides the string into substrings of the specified length.

##### Example
```

> (ngrams "fox" 3)

.: {" f" " fo" "fox" "ox " "x "}

> (ngrams "fox")

.: {" f" " fo" "fox" "ox " "x "}

> (ngrams "fox" 5)

.: {" f" " fo" " fox" " fox " "fox " "ox " "x "}

```

##### Related

lexemes, split, trim

## nix

Deletes a prototype.

##### Syntax
```

(nix prototype … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| prototype | prototype | 1+  | A prototype or list of prototypes. |

##### Results

| Taxon | Description |
| --- | --- |
| expression | Returns the literal nixed and the quantity deleted. |

##### Remarks

Undeclares a prototype. All thoughts of the relation must be reclaimed with the old function first, otherwise the function fails.

##### Example
```

> (new (relation Q))

.: Q_1

> (nix Q)

.: [Failure :Name InvalidOperation :Text "Cannot nix relations having thoughts."]

> (do (with Q ^ as ?q do (old ?q)) (nix Q))

.: nixed 1

> (is Q (given {?r} (more-p (meronomy ?r)))

.: false

> (new (relation P))

.: P_1

> (do (old (with P)) (nix P))

.: nixed 1

```

##### Related

structure, structures, old, relation, relations, seal, unseal

## no

True if no relevant knowledge satisfies all of the premises.

##### Syntax
```

(no premise … )

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot is unary-predicate

condition ::= slot not value

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A pattern, call, or ruth value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all the values are nil. |

##### Remarks

Equivalent to (not (any premise …)). If the value is a pattern or a relationship, then a cursor is created over which the remaining values are tested until truth or falsity is determined. If the value is an iterator, then a cursor is created over which the remaining values are tested until truth or falsity is determined.

##### Example
```

> (relation Is :)

.: false

> (no nil nil)

.: true

```

##### Related

all, any, default, nall

## none

True if the predicate is false for all sequence elements.

##### Syntax
```

(none symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | variant | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if every element does not satisfy the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example
```

> (none ?n in {1 2 3 4} (alphabetic-p ?n))

.: true

> (none ?m ?n per {{1 2} {3 4}} (< ?m ?n))

.: true

> (none ?m ?n over {4 2 1} (divisible-p ?m ?n))

.: false

```

##### Related

every, few, most, nevery, some

## nor

Negated logical disjunction.

##### Syntax
```

(nor truth truth … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 1+  | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all argument values are false |

##### Remarks

Equivalent to (not (or value value …)).

##### Example
```

> (nor true true true false)

.: false

> (nor true true true true)

.: false

> (nor false false false false)

.: true

```

##### Related

and, nand, not, or, xnor, xor

## not

True if the value is false, or if the applied unary predicate returns false.

##### Syntax
```

(not value predicate)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| predicate | literal | 0-1 | A unary predicate |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if value is false, or if the applied unary predicate returns false. |

##### Remarks

None.

##### Example
```

> (not false)

.: true

> (not true)

.: false

> (not 3 even-p)

.: true

> (not 7 (given {?n} (divisible-p ?n 3)))

.: true

> (not foo null-p)

.: true

> (not nil null-p)

.: false

```

##### Related

convert, datatype, is, known, the, type

## nothing

Returns nothing.

##### Syntax
```

(nothing)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| nothing | A nothing value. |

##### Remarks

None.

##### Example
```

> (nothing)

.:

> {a (nothing) b (nothing) c}

.: {a b c}

```

##### Related

ceiling, complex, floor, is, long, radix, rational, real, round, truncate, unsigned

## null-p

True if a value is nothing or nil.

##### Syntax
```

(null-p value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | A value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the values is nothing or nil. |

##### Remarks

None.

##### Example
```

> (null-p yes)

.: false

> (null-p nil)

.: true

> (null-p (nothing))

.: true

```

##### Related

exists-p

## odd-p

True if a number is odd.

##### Syntax
```

(odd-p number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the number is odd. |

##### Remarks

Returns true if the number is not evenly divisible by two.

##### Example
```

> (odd-p 500)

.: false

> (odd-p 1)

.: true

> (odd-p -33)

.: true

```

##### Related

even-p, negative-p, positive-p, zero-p

## old

Deletes a thought.

##### Syntax
```

(old thought)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| thought | variant | 1   | A premise, thought, relation, or list of thoughts. |

##### Results

| Taxon | Description |
| --- | --- |
| expression | Returns  the number of thoughts deleted. |

##### Remarks

Returns the number of thought identifiers deleted. If the relation has an !onOld method defined, then the method is invoked prior to the thought being deleted.

##### Example
```

> (relation Q)

.: Q

> (new Q)

.: Q_1

> (new Q)

.: Q_2

> (old Q_1)

.: 1

> (old Q)

.: 1

> (nix Q)

.: nixed

```

##### Related

structure, new, nix, relation

## omit

Creates a new sequence with values omitted.

##### Syntax
```

(omit sequence value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| value | variant | 0+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The modified assortment |

##### Remarks

A new sequence is constructed. To modify the sequence use the rip function.

##### Example
```

> (omit {a b c d e f g} a b)

.: {c d e f g}

> (omit {a 1 nil b 2 c 3 nil nil d nil 4} nil)

.: {a 1 b 2 c 3 d 4}

```

##### Related

Insert, pop, push

## on

Branched conditional evaluation.

##### Syntax
```

(on condition true-case false-case )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| true-case | variant | 1   | An expression to evaluate |
| false-case | variant | 1   | An expression to evaluate |

##### Results

| Taxon | Description |
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
```

(only symbols expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbols | list | 1   | A list of symbols from the enclosing scope |
| expression | variant | 1+  | An expression to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| value | Returns the last value. |

##### Remarks

Creates a new environment shadowing the designated symbols in the encompassing environment and executes each of the expressions, one at a time, returning the result of the last expression. No free variables (i.e., variables not defined inside the scope or not in the variable list) are permitted within the scope. only is equivalent to an in-line anonymous function. Changes to the symbols shall not affect the enclosing scope.

##### Example
```

> (function sample {?b ?c}

(let ?a 5)

(tell user ($ given a+b= (+ ?a ?b) \n))

(tell user ($ given a+b+c= (+ ?a ?b ?c) \n))

(only {?a ?b}

(tell user ($ only a+b= (+ ?a ?b) \n))

(try (tell user ($ only a+b+c= (+ ?a ?b ?c) \n))

learn ?f (tell user ($ "?c" is not in scope \n)))))

.: sample

> (sample 15 30)

given a+b= 20

given a+b+c= 50

only a+b= 20

?c is not in scope

.: told

```

##### Related

given, dynamic, local

## open

Opens a file or data url.

##### Syntax
```

(open url)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A file or data url. |

##### Results

| Taxon | Description |
| --- | --- |
| url | The opened url. |

##### Remarks

Opens an file.

##### Example
```

> (assign ?file (file name "kwikfox.txt"))

.: File-1

> (open ?file)

.: File-1

> (let ?contents (read ?file #))

.: true

> ?contents

.: "The quick brown fox jumped over the lazy dogs."

> (close ?file)

.: closed

```

##### Related

close, data, file

## or

Logical disjunction.

##### Syntax
```

(or truth truth … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 1+  | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if any argument value is true |

##### Remarks

Short circuits evaluation upon reaching the first true argument.

##### Example
```

(or false true false false)

.: true

(or true true true true)

: true

(or false false false false)

.: false

```

##### Related

and, is, nand, nor, not, xnor, xor

## out

True if a value is absent from a sequence.

##### Syntax
```

(out value sequence option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |
| sequence | sequence | 1   | A sequence. |
| option | expression | 0-2 | A key value pair. Any of depth number \- Number or # (for any depth). Default is 1. transform function \- A function to transform the element.. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is not in the sequence. |

##### Remarks

If value and sequence are strings, then a string search is performed.

##### Example
```

> (out x {a b c d e f g})

.: true

> (out "a" "cbazyx")

.: false

```

##### Related

includes, excludes, in, occurrences, pick, position

## overlaps-p

True if an interval finishes after a second interval starts.

##### Syntax
```

(overlaps-p interval<sub>1</sub> interval<sub>2</sub> tolerance)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if interval1 finishes after interval2 starts. |

##### Remarks

None.

##### Example
```

> (overlaps-p 1s~2s 3s~4s)

.: false

> (overlaps-p 1s~5s 4s~8s)

.: true

> (overlaps-p 1s~9s 4s~6s)

.: false

> (overlaps-p 4s~6s 5s~9s)

.: true

> (overlaps-p 3s~4s 5s~9s 2s)

.: true

```

##### Related

before-p, during-p, finishes-p, meets-p, starts-p

## pad

Creates a new padded sequence.

##### Syntax
```

(pad sequence length value side )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A string or list |
| length | number | 1   | The length of the final sequence |
| value | variant | 1   | A value to insert into the sequence |
| side | literal | 0-1 | the literal left or right (default). |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | Creates a new sequence |

##### Remarks

If the sequence is a string, the value must also be a one position string. If the sequence is a list, the value may be any value. To modify a string destructively, use resize.

##### Example
```

> (pad {1 2 3} 10 0)

.: {1 2 3 0 0 0 0 0 0 0}

> (pad "123" 10 "0")

.: "1230000000"

> (pad "123" 10 "0" left)

.: "0000000123"

> (pad {1 2 3} 10 0 left)

.: {0 0 0 0 0 0 0 1 2 3}

```

##### Related

fill , resize

## parameters

Returns a list of parameters for a function, call, or task.

##### Syntax
```

(parameters what )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| what | variant | 1   | A function, task or call. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of parameters to the function, task or call. |

##### Remarks

Functions are defined using the function intrinsic function. If the name is supplied then the function is a user named function (also called an exonym), otherwise it is an automatically named function (called an esonym). If a parameter list is supplied then it shall bind the formal parameter symbols to any actual parameter expressions provided. The first symbols in the parameter list are required. If a plus sign is provided, then those symbols following the plus sign are optional. Each optional parameter may have a default value (specified with an equal sign and the value). If no default value is specified, the default value shall be nil. If an ampersand is provided, then the symbol following it is bound to a list of remaining (variadic) actual parameter values. Keyword parameters (literal symbol pairts) may be provided as required or optional. The entire parameter list may be omitted. The function shall be accessible from other modules by prefixing it with the module name in which it was defined.

##### Example
```

> (function {?n} (+ 1 ?n))

.: fn-1

> (function plusN {?n + ?i = 1} (+ ?n ?i))

.: plusN

> (function addAll {& ?nums} (apply + ?nums))

.: addAll

> (fn-1 100)

.: 101

> (plusN 100)

.: 101

> (function tryParseNum {?s}

(let ?convertible (convertible-p ?s number))

{?convertible (if ?convertible (@ (take ?s)))})

> (tryParseNum "foo")

.: {false nil}

> (tryParseNum "123")

.: {true 123}

> (function dont {{try ?what} + {at ?where = nil}}

(apply (given {?s}(tell user ?s))

($ don't try ?what (unless (any ?where) "" ($ at ?where))))

.: dont

> (dont try "skydiving into a volcano")

don't try skydiving into a volcano

.: told

> (dont try this at home)

don't try this at home

.: told

```

##### Related

arguments, call, function, task, parameters

## partition

Creates a list of equivalence sets for a pivot element.

##### Syntax
```

(partition sequence pivot comparer)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| pivot | variant | 1   | An element in the list. |
| comparer | function | 0-1 | A comparison function.( Defaults to compare.) |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of sublists each containing elements partitioned by a predicate.. |

##### Remarks

If no comparer is provided, the function compare is used. The element argument is compared to each item in the sequence and three lists are returned, elements that are less, elements that are the same, and elements that are greater. If a comparer function is provided, it must return the literals <, \=, > for elements that are less than, equal to, or greater than the pivot element.

##### Example
```

> (partition (3 5 2 0 5 8 9} 5)

.: {{3 2 0}{5 5}{8 9}}

> (partition "abcdefg" "e")

.: {{"a" "b" "c" "d"}{"e"}{"f" "g"}}

> ((function qksort {?list}

(if (void-p ?list) {}

else (let {?less ?same ?more} (partition ?list (pick ?list)))

(& (qksort ?less) ?same (qksort ?more))))

(3 5 2 7 5 6 0 8 9})

.: {0 2 3 5 5 6 7 8 9}

```

##### Related

categorize

## path

Concatenates a folder and file name.

##### Syntax
```

(path component …)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| component | string | 1   | A folder, separator, or file name. |

##### Results

| Taxon | Description |
| --- | --- |
| string | Returns the concatenated folder and file as a string. |

##### Remarks

Returns a properly formatted path combining the folder and file name.The folder may or may not contain a terminating directory separator. The file may or may not contain a leading directory separator.

##### Example
```

> (path "C:/projects/project1/" (separator) "plan.pdf")

.: "C:/projects/project1/plan.pdf"

> (path "C:/projects/project1/" (file name "plan.pdf"))

.: "C:/projects/project1/plan.pdf"

> (path "C:/projects/project1/" (separator) "plan" (separator file) "pdf")

.: "C:/projects/project1/plan.pdf"

```

##### Related

file, folder, separator, url

## pattern

Creates a pattern containing the supplied expressions.

##### Syntax
```

(pattern expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1+  | An expression. |

##### Results

| Taxon | Description |
| --- | --- |
| premise | A premise |

##### Remarks

Returns an unevaluated pattern.

##### Example
```

> (pattern Prediction ^ as ?p :Hypothesis as ?h)

.: [Prediction ^ as ?p :Hypothesis as ?h]

> (pattern Hypothesis as ?h :Before as ?b :After as ?a (< ?b ?a))

.: [Hypothesis as ?h :Before as ?b :After as ?a (< ?b ?a)]

> (pattern {Solution_1 Solution_2} as ?s :Timeframe >= ?t)

.: [{Solution_1 Solution_2} as ?s :Timeframe >= ?t]

```

##### Related

^ thought, id, premise

## pause

Pauses an agent.

##### Syntax
```

(pause agent)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| agent | agent | 1   | An agent |

##### Results

| Taxon | Description |
| --- | --- |
| agent | The agent task. |

##### Remarks

This function pauses an asynchronous agent task that processes incomingc messages and performs a default job.

##### Example
```

> (let ?url (url scheme tcp port 5001))

.: true

> (function reply {?sender ?message} (tell ?sender "OK"))

.: reply

> (function job {& ?args} (tell user ($ 1)) (wait 0.5))

.: job

> (agent ?url reply job) (start Agent-1)

.: Agent-1 Agent-1

> (pause Agent-1) (wait 3) (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1)

111111.: cancelled freed

```

##### Related

ask, cancel, listen, pause, perform, start, tell

## perform

Invokes a call.

##### Syntax
```

(perform environment method instance expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| environment | environment | 0-1 | An environment (defaults to (scope)) |
| method | method | 1   | The method to be invoked |
| instance | instance | 1   | A prototype instance |
| expression | variant | 0+  | Additional arguements |

##### Results

| Taxon | Description |
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

.: A

> (new A)

.: A_1

> (perform (scope) !incr A_1)

.: 1

> (perform !incr A_1)

.: 2

```

##### Related

apply, call, closure, eval, function, macro, method, scope, supply

## pi

Returns 3.141592653589793.

##### Syntax
```

(pi)

```
##### Module

Math

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| real | The value of pi, 3.141592653589793 |

##### Remarks

Returns the constant 3.141592653589793

##### Example
```

> (pi)

.: 3.141592653589793

```

##### Related

e

## pick

Creates a list of randomly selected elements.

##### Syntax
```

(pick sequence quantity)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence of elements |
| quantity | integer | 0-1 | The number of items to select. Default is 1. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A sequence containing the selected elements. |

##### Remarks

Returns the specified quantity of randomly-chosen elements from the sequence. The quantity must be a number between 1 and the sequence size.

##### Example
```

> (function chunk (+ 7 (random -2 to +2)))

.: chunk

> (pick {a b c d e f g h i j k l m n o p q r s t u v w x y z} (chunk))

.: {k j z h q f}

> (pick "abcdefghijklmnopqrstuvwxyz" (chunk))

.: "cfilnsw"

```

##### Related

random, shuffle

## pipe

Creates a pipe.

##### Syntax
```

(pipe option … )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 1+  | A key value pair. One of host host \- name of the host computer port number – a port number. path name \- name of the pipe mode mode \- either read, write, or readwrite (default). content type - either binary or text (default). address url\- url string.. |

##### Results

| Taxon | Description |
| --- | --- |
| io resource | A file resource |

##### Remarks

Creates a pipe for reading or writing.

##### Example
```

> (let ?pipe (pipe address "pipe://localhost:4500/MyPipe"))

.: true

> (function reply {?target ?message} (tell ?target "goodbye."))

.: reply

> (service ?pipe reply)

.: Service-1

> (ask ?pipe "hello")

.: "goodbye."

> (cancel Service-1) (free ?pipe) (free Service-1)

.: cancelled freed freed

```

##### Related

close, erase, path, read, service, socket, write

## pop

Returns the element removed from a sequence.

##### Syntax
```

(pop sequence position )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | An assortment or sequence. |
| position | integer | 0-1 | A position. (defaults to 1) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The removed element |

##### Remarks

If position is omitted the first element of the sequence shall be deleted. The sequences is modified.

##### Example
```

> (pop {a b c d})

.: a

> (pop {a b c d} 2)

.: b

> (pop {a b c d e f g} 7)

.: g

```

##### Related

@ element, add,bind, cut, deq, enq, get, key, keys, put, #, values, zap

## posit

Writes module expressions to a url.

##### Syntax
```

(posit module url)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | module | 1   | A module. |
| url | url | 0-1 | A url. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns the literal posited if successful. |

##### Remarks

This function writes all expression in the module to a file named "MySubject.theory".

##### Example
```

> (posit Geometry (folder path "c:/projects/premise/"))

.: posited

> (posit MyModule (url path "//MyServer/Misc/"))

.: posited

```

##### Related

dependencies, discard, file, folder, forgo, module, modules, require, grok, use, url

## position

Finds the position of an element or subsequence within a sequence.

##### Syntax
```

(position sequence element option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The sequence to search |
| element | value | 1   | The item to be located |
| option | expression | 0+  | Key value pairs containing any of the following keys: from integer – the beginning position, (default is 1). to integer – a stop position, or # (default) for end of list go direction – forward (default) or backward. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The position of the item, or nil if not found. |

##### Remarks

None

##### Example
```

> (position {a b c d e f g h} f)

.: 6

> (position {a b c d e f g h} {f g h})

.: 6

> (position {a b a} a go backward)

.: 3

> (position {a b a} a go backward from 2)

.: 1

> (position "abcdefg" "cde" from 4)

.: nil

```

##### Related

@ element, gather, in, occurs, pick

## positions

Returns positions of an element in a sequence or position value pairs.

##### Syntax
```

(positions sequence element option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The sequence to search |
| element | value | 0   | The item to be located |
| option | expression | 0+  | Key value pairs containing any of the following keys: from integer – the beginning position, (default is 1). to integer – a stop position, or # (default) for end of list go direction – forward (default) or backward. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A possibly empty list containing the positions of the element. |

##### Remarks

If element is omitted, the function returns a list containing position value pairs for the sequence.

##### Example
```

> (positions {a b c d} b)

.: {2}

> (positions {a b c d} x)

.: {}

> (positions {a b c b d b} x)

.: {2 4 6}

> (positions (tuple :X nil :Y nil :Z apple))

.: {{1 :X}{2 nil}{3 :Y}{4 nil} {5 :Z}{6 apple}}

> (positions "abcd")

.: {{1 "a"}{2 "b"}{3 "c"}{4 "d"}}

```

##### Related

bindings, definitions, entries, position

## positive-p

True if a number is greater than zero.

##### Syntax
```

(positive-p number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the number is greater than zero |

##### Remarks

None.

##### Example
```

> (positive-p 500)

.: true

> (positive-p 0)

.: false

> (positive-p -25)

.: false

```

##### Related

even-p, negative-p, odd-p, zero-p

## premise

Creates a premise representation of a value.

##### Syntax
```

(premise value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A variant. |

##### Results

| Taxon | Description |
| --- | --- |
| premise | A premise |

##### Remarks

None.

##### Example
```

> (premise 1)

.: [Integer :Value 1]

> (premise "The quick brown fox")

.: [String :Value "The quick brown fox" :Size 19]

> (relation Foo :Item)

.: Foo

> (premise (new Foo :Item bar))

.: [Foo ^ Foo_1 :Item bar]

```

##### Related

id, position, known, new, old, relation, structure, the, with

## probability

Calculates the probability over a series.

##### Syntax
```

(probability events A operation B)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| events | list | 1   | A list of elements representing events |
| A   | expression | 1   | A key value pair. One of of event - a list element that predicate - a unary truth function. |
| operation | literal | 0-1 | An operation. One of {and, or, given} |
| B   | expression | 0-1 | A key value pair. One of of event - a list element that predicate - a unary truth function. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The probability of the supplied expression. |

##### Remarks

Calculates the probability of A in a list, or a conditional probability if B is also provided. The operator may be one of {and, or, given}.

##### Example
```

> (probability {head tail head tail} of tail)

.: 0.5

> (probability {1 2 3 4 5 6} that even-p and that (given {?n} (< ?n 4)))

.: 0.16666666667

> (probability {1 2 3 4 5 6} that even-p given that (given {?n} (< ?n 4)))

.: 0.08333333333

```

##### Related

statistics

## proceed

Evaluates expressions and recovers from an escape.

##### Syntax
```

(proceed expression … resumption … finally … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1+   | An expression to evaluate |
| resumption | expression | 1+ | the literal resume followed optionally by a literal tag and one or more expressions |
| finally | literal | 0-1  | Symbol value pairs for extant symbols at the location. |
| expression | expression | 1+   | An expression to evaluate |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true. |

##### Remarks

Transfers control to the specified location; then sets the indicated symbols to new values. If the symbols are not defined at the location, an unbound symbol failure occurs.

##### Example
```

> (function main {& list ?args}
    (tell user ($ \n Attempting dangerous operation... \n))
    (proceed
      (escape there)
      (tell user ($ \n Hello \n))
     resume here
          (tell user ($ Escaped here \n))
     rusimu there
          (tell user ($ Escaped there \n))
     finally
       (tell user ($ Whew, we dodged a bullet.)))
   )

.: main

> (main)

Attempting dangerous operation...

Escapted there 

Whew, we dodged a bullet.

Goodbye

.: told

```

##### Related

location, go

## product

Multiplies an expression over a range of values.

##### Syntax
```

(product symbol … binding sequence expression …)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | variant | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result of applying multiplication to the last expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the symbols then the function fails. The last expression shall be evaluated and the plus function shall be applied to both that expression and any prior result. The final value is returned.

##### Example
```

> (product ?x in (range 1 to 10) ?x)

.: 55

> (generator OneToTen {}

(step ?i from 1 to 10 (yield ?i))

(done))

.: OneToTen

> (product ?x in (OneToTen) ?x)

.: 55

```

##### Related

fold, summation

## punctuation-p

True if the first position of a string is punctuation.

##### Syntax
```

(punctuation-p string)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A value.. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the first position is punctuation. |

##### Remarks

None

##### Example
```

> (punctuation-p " the quick brown fox ")

.: false

> (punctuation-p "This and that")

.: false

> (punctuation-p "400 years")

.: false

> (punctuation-p "...")

.: true

```

##### Related

alphabetic-p, lowercase-p, uppercase-p, whitespace-p

## push

Modifies a sequence by inserting a value.

##### Syntax
```

(push sequence value position )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| value | variant | 1   | The value to be inserted. |
| position | integer | 0-1 | The position to insert the value. (Default is 1.) |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The modified sequence. |

##### Remarks

If position is omitted the value is prepended to the sequence. If # is used for the position, the value is appended to the sequence. Otherwise, the value is inserted at the indicated position. The sequence itself is modified.

##### Example
```

> (push {a b c} d)

.: {d a b c}

> (push {a b c} d 2)

.: {a d b c}

> (push "abcdef" g #)

.: "abcdefg"

```

##### Related

\# size, add, cut, deq, enq, get, insert, key, keys, put, values, zap

## put

Modifies an assortment or sequence by updating values.

##### Syntax
```

(put container entry … )

entry ::= key value

entry ::= position value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |
| entry | expression | 1+  | A key and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| thing | Returns the modified assortment or sequence. |

##### Remarks

For assortments, the key(s) to be updated must be present, for sequences, the positions to update must be within the sequence, otherwise the function fails. Keys and positions are added via the add function. Positions may be also added using append. Use copy or clone to return a new container. A coordinate is a position list. A list of keys may be provided for an entry as well, in which case the keys are traversed and the value is placed at the last key. To create a new container use replace.

##### Example
```

> (let ?a (lexicon x 1 y 2 z 3) ?s {a b c d e})

.: true

> (entries (put ?a y 12 z 13))

.: {{x 1}{y 12}{z 13}}

> (put ?s 2 hello 3 goodbye)

.: {a hello goodbye d e}

```

##### Related

add, cut, get, has, key, keys, lacks, let, values

## qualified

Prepends a module to a function name.

##### Syntax
```

(qualified module function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module literal. |
| function | literal | 1   | A function or macro literal. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The fully qualified literal with the module prepended to the function. |

##### Remarks

Returns a fully qualified function literal. If omitted, the first function matching the literal is returned.

##### Example
```

> (module Math

(function sum {& ?args} (apply + ?args)))

.: Math

> (qualified sum)

.: User.sum

> (qualified Math sum)

.: Math.sum

> (require Math)

.: Math

> (qualified sum)

.: Math.sum

```

##### Related

functions, modules, qualifier, unqualified

## qualifiers

Creates a list of modules associated with an identifier.

##### Syntax
```

(qualifiers identifier)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| identifier | identifier | 1   | An identifier |

##### Results

| Taxon | Description |
| --- | --- |
| list | The modules associated with the literal. |

##### Remarks

Checks the function against known modules and returns the modules in which the function is defined.

##### Example
```

> (qualifiers sum)

.: {}

> (module Math

(function sum ?args (apply + ?args)))

.: Math

> (use User)

.: User

> (require Math)

.: Math

> (qualifiers sum)

.: {Math}

```

##### Related

functions, modules, qualified, unqualified

## quantify

Returns a quantifier for elements satisfying a test.

##### Syntax
```

(quantify sequence predicate option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| predicate | function | 1   | A truth expression |
| option | expression | 0+  | A key value pair. One of as format - either the literal word (default) or percent. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns a percentage or the words none, few, half, most, all. |

##### Remarks

None.

##### Example
```

> (quantify {1 2 3 -4 5 6 7 8 9 10} (given {?n} (< ?n 0)))

.: few

> (quantify {1 2 3 4 5 6 7 8 9 10} number-p as percent)

.: 1.0

> (quantify {1 2 3 4 5 6 7 8 9 10} odd-p)

.: half

> (quantify {1 2 3 4 5 6 7 8 9 10} negative-p)

.: none

> (quantify {1 2 3 5 6 7 8 9} odd-p)

.: most

```

##### Related

coalesce, collect, exactly, filter, gather, quantity

## quantity

Returns the number of elements satisfying a test.

##### Syntax
```

(quantity symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per. |
| sequence | sequence | 1   | A sequence (string or list) |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| number | Returns the number of elements satisfying the test. |

##### Remarks

None.

##### Example
```

> (quantity ?n in {1 2 3 4 5 6 7 8 9 10}

(is ?n (given {?x} (= (taxon ?x) number))))

.: 10

> (summation ?n in {1 2 3 4 5 6 7 8 9 10} (bracket (odd-p ?n)))

.: 5

> (quantity ?n in {1 2 3 4 5 6 7 8 9 10} (odd-p ?n))

.: 5

> (quantity ?n in {1 2 3 4 5 6 7 8 9 10} (negative-p ?n))

.: 0

```

##### Related

coalesce, collect, exactly, filter, gather, quantify

## radians

Converts degrees to radians.

##### Syntax
```

(radians degrees)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| degrees | number | 1   | a number in degrees. |

##### Results

| Taxon | Description |
| --- | --- |
| number | Number of radians. |

##### Remarks

For the conversion the degrees are multiplied by π / 180, or roughly 0.0174532922222222.

##### Example
```

> (radians 200)

.: 3.490658444444444

> (radians 120)

.: 2.094395066666667

> (radians 45)

.: 0.7864815

```

##### Related

cosine, degrees, sine, tangent

## radix

Converts a number to a base.

##### Syntax
```

(radix number base )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | An integer or unsigned number to convert |
| base | integer | 0-1 | A number between 2 and 36. (default is 10) |

##### Results

| Taxon | Description |
| --- | --- |
| number | The number converted to the base as as an integer or long. |

##### Remarks

None.

##### Example
```

> (radix 15 8)

.: #08r17

> (radix (unsigned 89975) 16)

.: #16r15F77

> (radix #x15F77)

.: #10r89975

> (radix #d10 10)

.: #10r10

> (radix (integer 2.003) 2)

.: #02r10

```

##### Related

complex, float, imaginary, integer, long, real, unsigned

## random

Creates a random number.

##### Syntax
```

(random lower to upper precision)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| lower | number | 1   | A lower bound |
| to | literal | 1   | The literal to |
| upper | number | 1   | An upper bound |
| precision | literal | 0-1 | Either integer (default), real or float |

##### Results

| Taxon | Description |
| --- | --- |
| number | A random number. |

##### Remarks

If the precision is omitted the default precision is integer. If precision is omitted and the bounds are zero and one, then the default precision is real. If the precision is supplied, then it is used.

##### Example
```

> (random 0 to 1)

.: 0.325377881526947

> (random 0 to 1 float)

.: 0.8128264546394348216582

> (random 0 to 100)

.: 63

> (random 1000 to 2000 real)

.: 1194.230922829

```

##### Related

pick, shuffle

## range

Creates a list of numbers.

##### Syntax
```

(range first to last by increment)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| first | number | 1   | The initial value of the variable |
| limit | literal | 1   | The literal to, above, below or go. (default is to). |
| last | number | 1   | The final value of the variable |
| by | literal | 0-1 | by  |
| increment | number | 0-1 | The positive or negative increment for the variable |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list containing the numbers in the range. |

##### Remarks

If to is specified, the last number is included in the iteration. If below is specified the last value is excluded from the iteration. If above is specified the next number above the last value is included in the iteration. If go is specified, then the last value specifies the number of iterations.

##### Example
```

> (range 1 to 5)

.: {1 2 3 4 5}

> (range 1 to 10 by 2)

.: {1 3 5 7 9}

> > (range 100 go 5)

.: {100 101 102 103 104 105}

```

##### Related

for, step

## rational

Converts values to a rational number.

##### Syntax
```

(rational numerator denominator)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| numerator | variant | 1   | An integer or the literal minimum or maximum. |
| denominator | variant | 0-1 | A non-zero integer.( Default is 1.) |

##### Results

| Taxon | Description |
| --- | --- |
| number | A rational number. |

##### Remarks

All integers are rational numbers with a denominator of 1. If a non-zero denominator is supplied, it must be an integer. If a denominator is not supplied, then an attempt is made to convert the value to a rational number.

##### Example
```

> (rational {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not number"]

> (rational "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not number"]

> (rational 500)

.: 500/1

> (rational 500.0)

.: 500/1

> (rational "23.4")

.: 234/10

```

##### Related

complex, float, imaginary, integer, is, real

## read

Creates a string or stream.

##### Syntax
```

(read file count bits)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| file | resource | 1   | An file, or pipe. |
| count | variant | 0-1 | The number of bytes to read, the literal all, or the literal line. (Default is all.) |
| bits | integer | 0-1 | If count is provided, then this represents the size of the character in bits. Either 7, 8, 16,o,r 32. (Default is 8.) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | A string, stream, or the value nothing (if at end of file). |

##### Remarks

If the literal all is provided for count, the entire file (or stream) is read. If line is provided, one line is read (up to the newline character). If count is omitted, then the entire file read.

##### Example
```

> (global ?File (file name "test.txt" seek 1 erase yes)) ; open at BOF

.: true

> (seek ?File 1)

.: File-1

> (read ?File all)

.: "Hello, world.'

> (close ?File)

.: closed

```

##### Related

bytes, close, take, peek, peep, file, seek, write

## ready-p

True if a task has completed.

##### Syntax
```

(ready-p task)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| task | task | 1   | A task resource. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the task has completed |

##### Remarks

Returns true if the task has completed, false otherwise.

##### Example
```

> (let ?task (concurrent (@ (concurrent (idle 100s)))))

.: true

> (do (idle 20s)

(if (ready-p ?task)

(free ?task)

else

running))

.: running

```

##### Related

wait, abort, await, busy-p, cancel, cancelled-p, complete, reclaim, tarry, task

## real

Converts a value to a real number.

##### Syntax
```

(real value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number or the literal minimum or maximum. |

##### Results

| Taxon | Description |
| --- | --- |
| number | A real number. |

##### Remarks

If the value cannot be converted to a real number, the function fails.

##### Example
```

> (real {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not number"]

> (real "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not number"]

> (real 500)

.: 500.0

> (real 500.0)

.: 500.0

> (real "23.4")

.: 23.4

```

##### Related

complex, float, imaginary, integer, long, rational

## reasoning

Resumes or pauses asynchronous rule execution.

##### Syntax
```

(reasoning toggle)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| toggle | literal | 0-1 | The value on or off. Default is on if not supplied. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if rule execution is on. |

##### Remarks

If toggle is provided, rule execution is resumed (for on) or paused (for off).

##### Example
```

> (relation Car :Age :Condition)

.: Car

> (rule

when [Car :Age /= old :Condition = good]

do (tell user ($ ($$ \n that) is possible. \n)))

.: Rule-1

> (new Car :Age new :Condition good)

.: Car_1

> (reasoning)

.: true

that is possible.

> (reasoning off)

.: false

```

##### Related

is, rule, rules

## reclaim

Performs garbage collection.

##### Syntax
```

(reclaim)

```
##### Module

KB

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns the literal reclaimed when completed. |

##### Remarks

None.

##### Example
```

> (reclaim)

.: reclaimed

```

##### Related

free

## reduce

Converts a sequence into a value.

##### Syntax
```

(reduce sequence function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence |
| function | function | 1   | A function. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The return value of the function applied to all the items in succession. |

##### Remarks

Applies the binary function to each item of a list and returns the final value.

##### Example
```

(reduce {1 2 3 4 5} \*)

.: 120

(reduce {1 2 3 4 5} +)

.: 15

(reduce {3 2 1} \*\*)

.: 9

```

##### Related

fold

## relation

Creates a relation.

##### Syntax
```

(relation name inclusion … definition … )

inclusion ::= uses { prototype … }

definition ::= slot

definition ::= slot default-value

definition ::= method function

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of the relation |
| inclusion | expression | 0+  | A inclusion expression |
| definition | expression | 0+  | A slot definition expression |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The name of the defined relation |

##### Remarks

Relations are assortment prototypes that represent persistent relationships among one or more values. A relation is comprised of a name, attributes (collectively called slots) with optional default values, and methods. Relations are defined using the relation function. A thought is a relation record created using the new function. A relation must be defined before a thought can be formed. Any number of slots or methods can be specified, and default values may also be defined. A sealed relation cannot create new thoughts.

##### Example
```

> (relation Employee

:Salary

:Name

:Supervisor

:Reclaim false

!SalaryYTD Employee_salaryYTD

)

.: Employee

> (new Employee :Name "Jane Dough" :Salary 2000000.00)

.: Employee_1

> (premise Employee_1)

.: [Employee ^ Employee_1 :Salary 2000000.0 :Name "Jane Dough" :Supervisor nil

:Recalim false !SalaryYTD Employee_salaryYTD]

```

##### Related

new, nix, old, relation-p, relations, seal, structure, structures, unseal

## relations

Returns a list of defined relations.

##### Syntax
```

(relations)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list of all defined relations. |

##### Remarks

None

##### Example
```

> (relation Animal

:Phylum :Class :Order :Family :Genus :Species :Color :Weight :Height

)

.: Animal

  
> (relations)

.: {Animal}

> (nix Animal)

.: nixed

> (relations)

.: {}

```

##### Related

structures, structure, new, nix, old, relation,

## release

Releases locks on critical sections.

##### Syntax
```

(release locks)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| locks | list | 1   | A list of literals denoting critical section locks. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns the literal released if successful. |

##### Remarks

Forces the release of critical section locks.

##### Example
```

> (function pp {+ ?a ?b ?c ?d}

(critical {A B} (tell user ($ ?a ?b)))

(critical {C D} (tell user ($ \\s ?c ?d \n))))

.: pp

> (free (complete (critical {A B C D} (idle 30s)))

(do (idle 5)

(release {A B C D})

(tarry (complete

(pp the quick brown fox)

(pp jumped over lazy dogs)

(pp four score and seven)))))

the quick jumped over brown fox

four score lazy dogs

and seven

.: freed

```

##### Related

critical

## remove

Creates a new assortment by removing values.

##### Syntax
```

(remove assortment value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| value | variant | 1+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The new assortment. |

##### Remarks

To remove elements destructively use the rip function.

##### Example
```

> (entries (collection a b c d))

.: {{a a} {b b} {c c} {d d}}

> (entries (remove (lexicon a 1 b 2 c 3 d 4) 2 4))

.: {{a 1}{c 3}}

```

##### Related

add, combine, cut, rip

## repeat

Loops a specified number of times.

##### Syntax
```

(repeat count expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| count | variant | 1   | The number of iterations. |
| expression | expression | 0+  | A call to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | returns the last expression on the last iteration. |

##### Remarks

Repeats the expression(s) the specified number of times. An implicit counter from 0 to the designated count. Count may be an integer or long value.

##### Example
```

> (global ?i 0)

.: true

> (repeat 10 (--> ++ ?i))

.: 10

> (repeat 10 (--> -- ?i))

.: 0

> (repeat 1000 (--> ++ ?i))

.: 1000

> ?i

.: 1000

```

##### Related

do, for, loop, step, until, while

## replace

Creates a new assortment or sequence by updating values.

##### Syntax
```

(replace container entry … )

entry ::= key value

entry ::= position value

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | thing | 1   | An assortment or sequence. |
| entry | expression | 1+  | A key and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| thing | Returns the modified assortment or sequence. |

##### Remarks

For assortments, the key(s) to be updated must be present, for sequences, the positions to update must be within the sequence, otherwise the function fails. Keys and positions are added via the add function. Positions may be also added using append. Use copy or clone to return a new container. A coordinate is a position list. A list of keys may be provided for an entry as well, in which case the keys are traversed and the value is placed at the last key.

##### Example
```

> (let ?a (lexicon x 1 y 2 z 3) ?s {a b c d e})

.: true

> (entries (replace ?a y 12 z 13))

.: {{x 1}{y 12}{z 13}}

> (replace ?s 2 hello 3 goodbye)

.: {a hello goodbye d e}

```

##### Related

add, cut, get, has, key, keys, lacks, let, values

## require

Retrieves an absent module.

##### Syntax
```

(require module as moniker from url … options … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | The name of the required module |
| as | literal | 0-1 | The literal as. |
| moniker | literal | 0-1 | A literal. |
| from | literal | 0-1 | The literal from. |
| url | url | 0+  | URLs from which to retrieve the module. |
| options | expression | 0+  | Any of the following  <br>update choice where choice Is yes or no. |

#####
Results

| Taxon | Description |
| --- | --- |
| literal | The module |

##### Remarks

Allows the current module to access functions in the specified module using a moniker. The from URLs shall be evaluated if the module is either not present or if the update option is yes. Grok is applied to the urls in succession until one url is available to be read. s

##### Example
```

> (mySum 1 2 3)

.: [Failure :Name NotFound :Text "The function mySum isn't found"]

> (require MyMath as m from (file "lib/mymath.th"))

.: MyMath

> (mySum 1 2 3) (m.mySum 1 2 3)

.: 6 6

```

##### Related

dependencies, discard, extend, forgo, module, modules, run, use

## reset

Resets a series for reuse.

##### Syntax
```

(reset series)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| series | series | 1   | A series. |

##### Results

| Taxon | Description |
| --- | --- |
| series | Returns the series. |

##### Remarks

After the series is reset, the next function must be used to move the series to the first element.

##### Example
```

> (global ?Series (series {a b c}))

.: true

> (while (next ?Series) (tell user ($$ (this ?Series) ,) ($)))

a, b, c, .: told

> (reset ?Series)

.: Series-1

> (this ?Series)

.: [Failure :Name OutOfRange :Text "Must advance series to the first element."]

> (next ?Series)

.: true

> (this ?Series)

.: a

```

##### Related

next, series, this


## resignal

Resignals a tuple.

##### Syntax
```

(resignal tuple)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| tuple | tuple | 1   | Propagates an existing tuple. |

##### Results

| Taxon | Description |
| --- | --- |
| Tuple | A tuple. |

##### Remarks

This function resignals an existing tuple. To create the original tuple use the signal function.

##### Example
```

> (on (void-p {}) (signal Failure :Name BadArg :Text "Argument was empty")  success)

.: [Failure :Name BadArg :Text "Argument was empty"]

> (try

(try

(signal Misconception :Name User :Text "A big problem")

learn ?e

(tell user ($ Caught ?e \n))

(tell user ($ Rethrowing... \n))

(resignal ?e))

learn ?f

(tell user ($ Caught ?f again. \n))

done)

Caught [Misconception :Name User :Text "A big problem"]

Rethrowing...

Caught [Misconception :Name User :Text "A big problem"] again

.: done

```

##### Related

assert, ensure, fail, try

## resize

Modifies the length of a sequence.

##### Syntax
```

(resize sequence length default)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| length | integer | 1   | The length of the final sequence |
| default | variant | 0-1 | A value to fill the sequence (default is nil or space). |

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a the modified list. |

##### Remarks

If the sequence is a string, the default value must be a single position string (space if unspecified). If the sequence is a list, the default value may be any value (nil if unspecified).

##### Example
```

> (let ?s (array 3 of 0))

.: true

> (fix ?s 1 1 2 2 3 3)

.: {1 2 3}

> (resize ?s 10 0)

.: {1 2 3 0 0 0 0 0 0 0}

> (resize ?s 2 0)

.: {1 2}

```

##### Related

array, fill , pad

## rest

Creates a subsequence of all except the first elements.

##### Syntax
```

(rest sequence skip)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |
| skip | number | 0-1 | The number of elements to skip. Default is 1 |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The sequence without the skipped elements. |

##### Remarks

None

##### Example
```

> (rest {a b c d e})

.: {b c d e}

> (rest "abcdefg")

.: "bcdefg"

> (rest "abcdefg" 2)

.: "cdefg"

> (rest {a b c d e} 3)

.: {d e}

> (rest {a b c d e} 5)

.: {}

```

##### Related

but, last, top

## retract

Eliminates rules.

##### Syntax
```

(retract rules)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| rules | variant | 1   | A single rule resource or a list of rule resources. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The literal retracted |

##### Remarks

None.

##### Example
```

> (relation Fact :Number)

.: Fact

> (rule

when [Fact :Number as ?n]

(no [Fact ^ as ?f (= (:Number ?f) (++ ?n)])

do (knew Fact :Number (++ ?n)))

.: Rule-1

> (rule CleanUp when [Fact ^ as ?fact] do (old ?fact))

.: CleanUp

> (rules)

.: {CleanUp Rule-1}

> (retract (rules))

.:retracted

> (rules)

.: {}

```

##### Related

wait, abort, await, task, complete, busy-p, ready,-p, reclaim

## return

Terminates a function call.

##### Syntax
```

(return value option …)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | Any value to be returned. (Default is nil.) |
| option | expression | 0-1 | A key value pair. One of: from function \- returrns from a function on the call graph. unwind count \- unwinds the call graph a number of times.. |

##### Results

| Taxon | Description |
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

.: foo

> (foo)

.: found-it

> (function f1 {}

(do (tell user ($ inside do. \n))

(return 0))

(tell user ($ within f1. \n)))

.: f1

> (function main

(fn1)

(tell user ($ within main. \n)))

.: main

> (main)

inside do.

within f1.

within main.

.: nil

> (function f1 {}

(do (tell user ($ inside do. \n))

(break 0))

(tell user ($ within f1. \n)))

.: f1

> (main)

inside do.

within f1.

within main.

.: told

> (function f1 {}

(do (tell user ($ inside do. \n))

(break 0))

(tell user ($ within f1. \n)))

.: f1

> (main)

inside do.

within f1.

within main.

.: told

> (function f1 {}

(do (tell user ($ inside do. \n))

(return 0 from f1))

(tell user ($ within f1. \n)))

.: f1

> (main)

inside do.

within main.

.: told

> (function f1 {}

(do (tell user ($ inside do. \n))

(return 0 from f1))

(tell user ($ within f1. \n)))

.: f1

> (main)

inside do.

within main.

.: told

> (function f1 {}

(do (tell user ($ inside do. \n))

(return 0 from f1))

(tell user ($ within f1. \n)))

.: f1

> (main)

inside do.

within main.

.: told

> (function f1 {}

(do (tell user ($ inside do. \n))

(return 0 from main))

(tell user ($ within f1. \n)))

.: f1

> (main)

inside do.

.: 0

> (let ?a (let {?y "hello"}

(if (< (@ ?name) "M") (return ($ Goodbye ?name) unwind 2)

else (tell user ($ Hello ?name)))

(ask user ($ What is your favorite color?))

($ You’re nice))

.: true

> ?a

.: "You’re nice"

```

##### Related

continue, do, break, fail, function, go, location, resume, try

## reverse

Creates a reversed sequence.

##### Syntax
```

(reverse sequence)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The reversed sequence |

##### Remarks

None.

##### Example
```

> (reverse "abcde")

.: "edcba'

> (reverse {a b c d e})

.: {e d c b a}

> (reverse [A :B C :D E])

.: [E :D C :B A]

> (reverse (' (a b c d e)))

.: (e d c b a)

```

##### Related

but, first, last, pick, rest, mid, top

## right

True if values are equal or the first value is nil.

##### Syntax
```

(right first second )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| first | variant | 1   | A value to be compared. |
| second | variant | 1   | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are the same or if second is nil |

##### Remarks

Returns true if each value is the same or if the first value is nil, and false otherwise. Both values must be of the same type, and must be numbers, literals, or strings. Short circuits if false. Two items are equal if their representation is the same regardless of whether or not they occupy the same location in memory (viz. identical). Returns false if both values are false.

##### Example
```

> (right a a)

.: true

> (right "johnny" "ralph")

.: false

> (right nil 3)

.: true

> (right nil nil)

.: false

```

##### Related

< less , <= less or equal, > greater, >= greater or equal, /= unequal, full, identical, left

## rip

Removes elements from assortments by value.

##### Syntax
```

(rip assortment value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| value | variant | 1+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The modified assortment. |

##### Remarks

Assortments are modified destructively. To delete nondestructively use the omit function.

##### Example
```

> (entries (collection a b c d))

.: {{a a} {b b} {c c} {d d}}

> (entries (rip (lexicon a 1 b 2 c 3 d 4) 2 4))

.: {{a 1}{c 3}}

```

##### Related

cut, omit

## round

Rounds a number to the nearest integer.

##### Syntax
```

(round number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A real number. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The rounded integer |

##### Remarks

If the number is zero, zero is returned. If the number is negative then if the tenths digit is five or less, it shall be rounded down towards negative infinity, otherwise it shall be rounded towards positive infinity. If the number is positive, then if the tenths digit is five or greater, it shall be rounded towards positive infinity, otherwise it shall be rounded towards negative infinity.

##### Example
```

> (round 0.5)

.: 1

> (round 0.4)

.: 0

> (round 0.49)

.: 0

> (round -0.5)

.: -1

> (round -0.4)

.: 0

```

##### Related

% modulus, ceiling, floor,truncate,

## rule

Creates a rule.

##### Syntax

```
(rule name properties when premises option … action … )

properties ::= { property … }

property ::= :Stage literal

property ::= :Salience integer

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot is unary-predicate

condition ::= slot not value

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

option ::= scan number

option ::= limit number

option ::= group slot … by slot … into symbol

option ::= merge value …

option ::= sort ordering …

action ::= deem value1 else value2

action ::= do expression …

action ::= give expression

action ::= list value …

action ::= tally

action ::= yield expression

ordering ::= term comparator

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 0-1 | The name of the rule. If omitted, the rule is auto-named. |
| properties | list | 0-1 | A list containing any of the following properties: :Salience integer – indicates the rule priority :Stage literal – indicase the rule stage |
| with | literal | 1   | The literal with. |
| clauses / premises | expression | 1+  | Either one or more clauses, or, one or more premises |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |
| action | literal | 0-1 | Either deem, do, give, list, tally, yield. |
| expression | expression | 0+  | An expression |

##### Results

| Taxon | Description |
| --- | --- |
| rule | Returns a rule. |

##### Remarks

The rule macro creates a rule to monitor premises. The rule is run spontaneously when premises match the preconditions. There is no guarantee as to when or whether or not the rule shall execute. The rule may be cancelled and deleted using the reclaim command.

Note that a predicate is a truth function, scan tells the number of matches to attempt (default is infinity), and limit tells how many results to return (default is infinity). If the action is deem, then the subsequent value is returned if the final descriptor is matched, otherwise the else value is returned. If the action is do, then for each match the expressions are run, and for the last match, the last value of the last expression is returned, or nil is returned if all descriptors were false or had no matches. If the action is give, then the expression is immediately returned from the with call on the first match, akin to return from with. If the action is yield, then the expression is immediately returned from the with call, but may be resumed with a next function call. When all matches are completed, the done function is implicitly called to terminate the generator. If the action is group, followed by a list of slots and values from which the group is picked, then the literal by and a set of slots and values that determines the grouping inclusion , and finally the literal into followed by a symbol to which the group shall be bound on each iteration. If the action is either list (or merge), then a (merged) list is returned or an empty list if nothing matched. If the action is sort then the list of slots and comparators should follow. (Note that list is required if the sort action is selected.) If the action is tally, then the number of matched premises is returned, or zero if no matches.

##### Example
```

> (reasoning off)

.: false

> (relation Fact :All :Are)

.: Fact

> (rule ExcludedMiddle

when [Fact :All as ?S :Are as ?M]

[Fact :All = ?M :Are as ?P]

do

(knew Fact :All ?S :Are ?P))

.: ExcludedMiddle

> (new Fact :All people :Are mortal)

.: Fact_1

> (with Fact)

.: {Fact_1}

> (new Fact :All philosophers :Are people)

.: Fact_2

> (with Fact list @^)

.: {Fact_1 Fact_2}

> (reasoning on)

.: true

> (with Fact list @^)

.: {Fact_1 Fact_2 Fact_3}

> (get Fact_3)

.: [Fact ^ Fact_3 :All philosphers :Are mortal]

> (rules)

.: {ExcludedMiddle}

> (retract ExcludedMiddle)

.: retracted

> (rule {:Salience 100 :Stage 0}

when [Fact :All as ?S :Are as ?M]

[Fact :All = ?M :Are as ?P]

do

(knew Fact :All ?S :Are ?P))

.: Rule-1

> (rules)

.: {Rule-1}

> (retract (rules))

.: retracted

> (which Fact ^ as ?a :Are mortal list ?a)

.: {Fact_1 Fact_3}

> (which Fact :Are mortal)

.: {[Fact ^ Fact_1 :All people :Are mortal]

[Fact ^ Fact_3 :All philosophers :Are mortal]}

```

##### Related

reasoning, reclaim, rules, using, with

## rules

Returns a list of rules defined in a module.

##### Syntax
```

(rules module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 0-1 | A module. If not provided defaults to the current module. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of rules defined in the module. |

##### Remarks

The module must be a literal in the list obtained by calling the (modules) function. If the module is not provided this function uses the current module (obtained via the (use) function).

##### Example
```

> (module Mine

(rule foo {:Stage One :Salience 0} when [A ^ as ?a] list ?a))

.: Mine

> (rules Mine)

.: {foo}

> (use User)

.: User

> (rule hello when [A ^ as ?a] list ?a)

.: hello

> (rules)

.: {hello}

```

##### Related

function, module, modules, symbols

## same

True if all values are equal or contain equal elements.

##### Syntax
```

(same value value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 2+  | A value to be compared. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all values are identical |

##### Remarks

Returns true if each value is the equal to the next value from left to right, sequences are the same if the are equal length and contain the same elements regardless of order.

##### Example
```

> (same a a a)

.: true

> (same "johnny" "ralph" "sam")

.: false

> (same 3 3 3)

.: true

> (same {a b c} {c b a} {c a b})

.: true

> (same "abc" "cba" "cab")

.: true

> (same {"abc"}{"cba"}{"cab"})

.: false

```

##### Related

\= equal, < less , <= less or equal, > greater, >= greater or equal, /= unequal, identical

## scale

Applies a function to a list of numbers and scalar values.

##### Syntax
```

(scale list scalar … function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| list | list | 1   | A list of numbers. |
| scalar | number | 1+  | A number. |
| function | function | 1   | The name of the function to invoke |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The resulting sequence. |

##### Remarks

None.

##### Example
```

> (scale {1 2 3} 5 +)

.: {6 7 8}

> (scale {1 2 3} 5 10 \*)

.: {50 100 150}

```

##### Related

apply, collect, count, filter, gather, group, map, merge, reduce , separate, sort

## scatter

Applies functions in parallel returning a list of results.

##### Syntax
```

(scatter arguments functions)

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| arguments | list | 0-1 | The intial arguments to each function. |
| functions | list | 1   | An unordered list of functions to be applied. |

##### Results

| Taxon | Description |
| --- | --- |
| list | Non nil results |

##### Remarks

This function supplies the arguments to each function and returns a list of results from all the functions evaluated in parallel. Sequential forms of this function are compose and morph.

##### Example
```

> (scatter {5} {++ -- (given {?x} (\* ?x 2))})

.: {6 4 10}

> (scatter {{the quick brown fox jumped over the lazy dogs}}

{but rest top last})

.: {{the quick brown fox jumped over the lazy }

{quick brown fox jumped over the lazy dogs}

{the} {dogs}}

> (scatter {2 3 4} {+ \* -})

.: {9 24 -5}

```

##### Related

apply, concurrent, complete, compose,map, morph

## scope

Finds an environment or gets the current environment.

##### Syntax
```

(scope keyval … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| keyval | expression | 0-2 | A key value pair where key is either: at name where name of an environment or module, of what where what is a symbol or function,  <br>to offset search until negative integer ancestors back,  <br>go offset jumps to negative integer ancestors back. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The environment or nil if not found. |

##### Remarks

If no argument are provided, scope returns the current environment. If offset is provided, it indicates the number of ancestors to search backward. Kewords of and to are used together to locate a function or symbol, while go is used to pick a specific environment relative to a starting environment.

##### Example
```

> (function foo {}

(let ?func (scope) ?symbol (symbol func))

(let {?inner (scope)}

(tell user ($ function scope ?func \n))

(tell user ($ inner scope ?inner \n)))

(tell user ($ parent of inner scope (scope at ?inner go -1) \n)))

(tell user ($ location of ?symbol (scope of ?symbol to -10) \n))))

.: foo

> (foo)

function scope Environment-2

inner scope Environment-3

parent of inner scope Environment-2

location of ?func scope Environment-1

.: told

```

##### Related

do, function, given, global, invoke, local, modular

## seal

Prohibits new records.

##### Syntax
```

(seal prototype)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| prototype | literal | 1   | The name of a relation. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns sealed |

##### Remarks

Calling the new function on a sealed relation shall fail. Sealed relations must be unsealed before the new function shall work again.

##### Example
```

> (relation Q)

.: Q

> (new Q)

.: Q_1

> (seal Q)

.: sealed

> (new Q)

.: [Failure :Name Permission :Text "Attempt to modify sealed relation Q"]

> (unseal Q)

.: unsealed

> (new Q)

.: Q_2

```

##### Related

relation,structure, unseal

## secant

Calculates the secant of the number.

##### Syntax
```

(secant number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The secant of the number. |

##### Remarks

None.

##### Example
```

> (secant 0.785398)

.: 1.41421333

> (secant cir 0.785398 radians)

.: 1.41421333

> (secant cir 75 degrees)

.: 3.863703305

> (secant hyp 10 degrees)

.: 0.98496007966

> (secant hyp 0.0872665 radians)

.: 0.9962043239686199

```

##### Related

acosecant, asecant, cosecant

## seconds

Creates a seconds value or returns seconds since year zero.

##### Syntax
```

(seconds seconds)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| seconds | variant | 0-1 | The number of seconds as an integer or time. |

##### Results

| Taxon | Description |
| --- | --- |
| second | The argument converted to seconds, or seconds since the year zero. |

##### Remarks

If no argument is supplied, this function returns the current date and time since the year zero in seconds, otherwise it attempts to construct a second atom from the supplied argument.

##### Example
```

> (seconds)

.: 63698773193s

> (seconds 546)

.: 546s

> (if (< (seconds) eternity)

(tell user ($ Now is less than the infinite future. \n)))

Now is less than the infinite future.

.: told

> (if (> (seconds) neternity)

(tell user ($ Now is greater than the infinite past. \n))

Now is greater than the infinite past.

.: told

```

##### Related

date, moment, paused, tick

## securelink

Creates a secure link.

##### Syntax
```

(securelink option … )

(securelink address)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| address | string | 0-1 | The url address. |
| option | expression | 0+  | A key value pair. One of user credentials \-user name and password host host \- host computer name (default is localhost) port number – a port number. (default is 2001) path path – a path query query – a query element fragment fragment – a fragment element |

##### Results

| Taxon | Description |
| --- | --- |
| service | A file resource |

##### Remarks

Returns a secure link.

##### Example
```

> (function reply {?target ?request} (tell ?target "goodbye."))

.: reply

> (service (assign ?service (securelink "https://localhost:4500/foxxy")) reply)

.: Service-1

> (ask ?service "hello")

.: "goodbye."

> (cancel Service-1) (free ?service) (free Service-1)

.: cancelled freed freed

```

##### Related

close, erase, path, pipe, read, socket, write

## seek

Repositions a file resource to a new read/write location.

##### Syntax
```

(seek file position)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| file | file | 1   | An file resource. |
| position | variant | 1   | A byte position in the file, or 1 (beginning), or \# (end). |

##### Results

| Taxon | Description |
| --- | --- |
| file | Returns the file resource. |

##### Remarks

None.

##### Example
```

> (set ?file (file name "test.txt"))

.: File-1

> (read ?file #)

.: "Hello"

> (seek ?file 1)

.: File-1

> (write ?file "Goodbye")

.: File-1

> (close ?file)

.: closed

```

##### Related

bytes, close, file, read, write

## self

Returns the currently executing task resource.

##### Syntax
```

(self)

```
##### Module

Tasks

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| task | The task resource for the executing task. |

##### Remarks

None.

##### Example
```

> (self)

.: task-0

> (concurrent (tell user ($ My task is (self) \n)))

My task is task-4

.: {task-4}

```

##### Related

wait, abort, concurrent, await, complete, reclaim, task, tasks

## separator

Creates a separator string.

##### Syntax
```

(separator kind)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| kind | literal | 0-1 | One of scheme, volume, folder (default), file, path, port, unchost, uncpath. |

##### Results

| Taxon | Description |
| --- | --- |
| string | A folder or volume separator character. |

##### Remarks

None.

##### Example
```

> (separator)

.: "/"

> (separator path)

.: "/"

> (separator scheme)

.: "//"

> (separator volume)

.: ":/"

> (separator port)

.: ":"

> (separator file)

.: "."

```

##### Related

file, folder, path, url

## series

Creates a serial iterator.

##### Syntax
```

(series iterable)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| iterable | variant | 1   | A sequence, assortment, or stream,. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | returns the last expression. |

##### Remarks

The iterable must be either a sequence, assortment, or stream..

##### Example
```

> (function walk {?iterable}

(ensure {sequence assortment stream} ?iterable)

(let ?series (series ?iterable))

(map (infix (let {?e nil ?result {}}

(reset ?series)

(while (next ?series)

(set ?e (this ?series))

(add ?result (do ($ ?e))))

?result)

",")

(given {?x} (tell user ?x)))

walked)

.: walk

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
```

(service url handler)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A Universal Resource Locator.. |
| handler | function | 1   | An message handler function. |

##### Results

| Taxon | Description |
| --- | --- |
| Service | The Service task. |

##### Remarks

This function creates an asynchronous service task that processes messages. The handler function shall receive the sender’s url, and an optional message string so that it may return a response.

##### Example
```

> (let ?url (url scheme tcp port 5001))

.: true

> (function reply {?sender ?message}  
(tell ?sender "OK"))

.: reply

> (start (service ?url reply))

.: Service-3

> (ask ?url "How are you?")

.: "OK"

> (free (cancel Service-3))

.: freed

```

##### Related

agent, ask, cancel, free, tell, start

## set

Assigns symbols to values. .

##### Syntax
```

(set manner assignment ... )

assignment ::= symbol value

assignment ::= {symbol ... } list

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| Truth | Returns true. |

##### Remarks

If a list of symbols is provided for an assignment, then the value must be a list with the corresponding number of elements. The symbol must have previously been defined otherwise a symbol not found failure shall occur. If parallel is specified as the manner, the symbols are defined in parallel, otherwise the symbols are assigned in tandem (by default).

##### Example
```

> (set ?person DrWho)

.: true

> ?person

.: DrWho

> (set parallel {?x ?y ?z} {1 2 3})

.: true

```

##### Related

<-- before tie , --> after tie, dynamic, global, let, local, modular, only, scope, tie

## sever

Creates a new assortments by removing keys.

##### Syntax
```

(sever assortment key … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | An assortment. |
| key | variant | 1+  | A key. |

##### Results

| Taxon | Description |
| --- | --- |
| assortment | The new assortment. |

##### Remarks

Assortments are modified destructively. To delete nondestructively use the remove function.

##### Example
```

> (entries (collection a b c d))

.: {{a a} {b b} {c c} {d d}}

> (entries (sever (lexicon a 1 b 2 c 3 d 4) b d))

.: {{a 1}{c 3}}

```

##### Related

cut, rip, remove

## shuffle

Creates a reordered sequence.

##### Syntax
```

(shuffle sequence seed)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or string. |
| seed | number | 0-1 | A randomization seed. |

##### Results

| Taxon | Description |
| --- | --- |
| list | The list reordered. |

##### Remarks

None..

##### Example
```

> (global ?Alphabet {a b c d e f g h i j k l m n o p q r s t u v w x y z})

.: true

> (shuffle ?Alphabet)

.: {v z e g s y c b t h x o p I q a d r k l n u m j f w}

> (shuffle ?Alphabet 123)

.: {y g l r x b k u t a j q f c d i s h e m v p n z o w}

> (shuffle ?Alphabet 123)

.: {y g l r x b k u t a j q f c d i s h e m v p n z o w}

> (shuffle "abcdefghijklmnopqrstuvwxyz" (tick))

.: "pnitdvjbqyuxkfazorecmwgslh"

```

##### Related

pick, random

## sigma

Calculates the sigma of a sequence.

##### Syntax
```

(sigma list )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| list | list | 1   | A list. |
| of | literal | 0-1 | The literal of. |
| kind | literal | 0-1 | Either population or sample. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The standard deviation |

##### Remarks

Returns the amount of variation or dispersion of the list. Low deviation indicates the values are close to the mean while high deviation indicates values are more spread out.

##### Example
```

> (sigma {1 2 3 4} of population)

.: 1.118033988749895

> (sigma (map {{apple 1}{pear 2}{banana 3}{coconut 4}} (given {?e} (@ ?e 2)))

of population)

.: 1.118033988749895

> (sigma (range 1000 to 3000000 by 10000) of sample)

.: 866020.5925188307

> (sigma (range 100 to 3000 by 100) of sample)

.: 865.544144839919

```

##### Related

probability, range, statistics

## sign

Returns the sign of a number as a number, sigil, or word.

##### Syntax
```

(sign number option … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A real number. |
| option | expression | 0+  | One of part which - where which is real (default)or imaginary format output - either number (default) , glyph or word. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the literal + if the number is positive or zero, or the literal - otherwise. |

##### Remarks

By default , this function returns the number 1 if positive, the number 0 if zero, or -1 if negative. If the format is glyph, then If the number is positive this function returns the literal +, if zero it returns nothing, otherwise it returns the literal \-. When the format s word then it returns positive or negative, and nothing if zero.

##### Example
```

> (sign 500)

.: 1

> (sign 0 format number)

.: 0

> (sign -1000+32i part real format word)

.: negative

> (sign 500 format glyph)

.: +

```

##### Related

digit, digits, exponential, fractional, significand

## signal

Signals a failure.

##### Syntax
```

(signal type term ...)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| type | literal | 1   | the type of the tuple. |
| term | expression | 0+   | a slot and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| tuple | A tuple. |

##### Remarks

This function creates a tuple and unwinds the stack to the overarching try block. To resignal a tuple use the resignal function.

##### Example
```

> (if (void-p {}) (signal Failure :Name BadArg :Text "Argument was empty") else success)

.: [Failure :Name BadArg :Text "Argument was empty"]

> (try

(try

(signal Failure :Name User :Text "A big problem")

learn ?e

(tell user ($ Caught ?e \n))

(tell user ($ Rethrowing... \n))

(resignal ?e))

learn ?f

(tell user ($ Caught ?f again. \n))

done)

Caught [Failure :Name User :Text "A big problem"]

Rethrowing...

Caught [Failure :Name User :Text "A big problem"] again

.: done

```

##### Related

assert, ensure, fail, try

## significand

Calculates the modified significand as a number between 1 and 10, or zero.

##### Syntax
```

(significand number kind)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |
| kind | literal | 0-1 | One of normed, scientific (default), or integer. |

##### Results

| Taxon | Description |
| --- | --- |
| number | A number between 1 and 10, or 0.0. |

##### Remarks

The normed significand represents the number as a fraction (0.nnnn). The scientific significand represents the number as a decimal between 1.0 and 10.0 (n.nnnn). The integer significand represents the number as an integer (nnnn).

##### Example
```

> (significand 500.645 integer)

.: 500645

> (significand 0)

.: 0.0

> (significand -12345 normed)

.: 0.12345

> (significand -2302.023900 scientific)

.: 2.3020239

```

##### Related

digit, digits, exponential, fractional

## sine

Calculates the sine of a number.

##### Syntax
```

(sine number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The sine of the number. |

##### Remarks

None.

##### Example
```

> (sine 0.785398)

.: 0.7071066656

> (sine cir 0.785398 radians)

.: 0.7071066656

> (sine cir 45 degrees)

.: 0.7071067811

> (sine hyp 1.5708 radians)

.: 2.30130811905

> (sine hyp 90 degrees)

.: 2.30129890230

```

##### Related

asine, cosine

## so

Creates a task level scope.

##### Syntax
```

(so expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 0+  | An expression. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last expression. |

##### Remarks

Any new variables declared shall shadow any prior variables with the same name.

##### Example
```

> (so (let ?file (file name "myfile.out"))

(seek ?file #)

(for ?s in ?message (write ?file ($ ?s)))

(close ?file))

.: closed

```

##### Related

do, assume, scope

## socket

Creates a TCP socket.

##### Syntax
```

(socket option … )

##### odule

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| option | expression | 0+  | A key value pair. One of scheme scheme \- either tcp (default) or udp user username \-user name password password \- password host host \- host computer name (default is localhost) port number – a port number. (default is 2001)  <br>address url \- the uniform resource locatior as string |

##### Results

| Taxon | Description |
| --- | --- |
| io resource | A file resource |

##### Remarks

Opens a port for reading or writing and returns a socket.

##### Example
```

> (function reply {?target ?request} (tell ?target "goodbye."))

.: reply

> (service (assign ?socket (socket "http://localhost:4500/foxxy")) reply)

.: Service-1

> (ask ?socket "hello")

.: "goodbye."

> (cancel Service-1) (free ?socket) (free Service-1)

.: cancelled freed freed

```

##### Related

close, erase, path, pipe, read, service, write

## some

True if the test is true for any element in the sequence.

##### Syntax

(some symbol … binding sequence expression … test)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | An iteration variable |
| binding | literal | 1   | The literal in, per, or over. |
| sequence | sequence | 1   | A list or string |
| expression | expression | 0+  | An expression. |
| test | truth | 1   | A truth expression |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if any element satisfies the predicate |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to sub-elements of each subsequence. If the binding over is specified, each symbol is bound to overlapping elements of the sequence. If there are insufficient elements to bind to the symbols then the function fails. The expressions and test are evaluated. If the sequence is empty the function fails.

##### Example
```

> (some ?x in {a b c d} (= ?x c))

.: true

> (some ?m ?n per {{2 1} {3 4}} (< ?m ?n))

.: true

> (some ?m ?n over {4 3 2 7} (divisible-p ?m ?n))

.: false

```

##### Related

every, few, nevery, none, most

## sort

Creates a sorted sequence.

##### Syntax
```

(sort sequence ordering option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The string or list to sort |
| ordering | variant | 1   | an ordering is either: a direction, i.e. < (ascending) or > (descending) for a sequence of atoms, or an ordered list of slot direction pairs (e.g. , { slot dir slot dir ...} ) if the elements are premises or tuples, or an ordered list of position direction pars (e.g., {position dir position dir ...} ) if the elements are sequences. an ordered list of key direction pairs (e.g., {key dir key dir ...} ) if the elements are assortments. |
| option | expression | 0+  | A key value pair containing any of the following keys: comparer - a comparison function (uses the compare function if this key value pair is not supplied). transform - function to retrieve a value given an item key – a alist key (if sequence is a alist) index – a list index (if sequence is a list of lists) minval – a minimum value to consider in card sort maxval – a maximum value to consider in card sort limit - a number of items to return after sorting algorithm - value one of { tree, card } default is tree |

##### Results

| Taxon | Description |
| --- | --- |
| list | The sorted list |

##### Remarks

The typical ordering is < for ascending and > for descending.

##### Example
```

> (sort {1 2 8 9 3 6 2} <)

.: {1 2 2 3 6 8 9}

> (sort {1 2 8 9 3 6 2} >)

.: {9 8 6 3 2 2 1}

> (Relation N :Value 0)

.: N

> (for ?value in (range 1 to 10) (new N :Value (random 1 to 100))

.: 55

> (sort (with N :Value as ?v list ?v) <)

.: {4 27 38 41 55 68 83 94 97}

> (sort {{A 1}{C 3}{F 6}{B 2}{D 4}{E 5}} {2 >})

.: {{F 6}{E 5}{D 4}{C 3}{B 2}{A 1}}

> (sort {{Letter A Number 1}{Letter C Number 3}{Letter B Number 2}}

{Letter >})

.: {{Letter C Number 3}{Letter B Number 2}{Letter A Number 1}}

```

##### Related

align, apply, best, count, gather, map

## split

Creates a list of subsequences divided at a delimiter.

##### Syntax
```

(split sequence delimiter)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or a string. |
| delimiters | sequence | 0-1 | A sequence of delimiters.(Default is space character) |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of subsequences. |

##### Remarks

Returns a list of sequences split at a delimiter. The delimiter is not included in the result.

##### Example
```

(split "the quick brown fox")

.: {"the" "quick" "brown" "fox"}

(split {the quick brown fox jumped over the lazy dogs} {the})

.: {{quick brown fox jumped over} {lazy dogs}}

```

##### Related

$ concatenate , capitalize, char, infix, lexemes, lowercase, ngrams, take, trim, unicode, uppercase

## start

Starts an agent, cell, or task.

##### Syntax
```

(start compute arugment …)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| compute | compute | 1   | An agent, cell, or task. |
| argument | variant | 0+  | An argument to the compute |

##### Results

| Taxon | Description |
| --- | --- |
| compute | Returns the argument. |

##### Remarks

This function starts an asynchronous agent task that processes incomingc messages and performs a default job.

##### Example
```

> (let ?url (url scheme tcp port 5001))

.: true

> (function reply {?sender ?message} (tell ?sender "OK"))

.: reply

> (function job {& ?args} (tell user ($ 1)) (wait 0.5))

.: job

> (agent ?url reply job)

.: Agent-1

> (start Agent-1) (wait 3) (cancel Agent-1) (free Agent-1)

111111.: cancelled freed

```

##### Related

ask, cancel, listen, pause, perform, start, tell

## starts-p

True if two intervals start together.

##### Syntax
```

(starts-p interval<sub>1</sub> interval<sub>2</sub> tolerance)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| interval<sub>1</sub> | interval | 1   | An interval |
| interval<sub>2</sub> | interval | 1   | An interval |
| tolerance | instant | 0-1 | Amount of variation. (Defaults to zero ticks). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if interval1 starts with interval2. |

##### Remarks

None.

##### Example
```

> (starts-p 1s~2s 3s~4s)

.: false

> (starts-p 1s~5s 1s~8s)

.: true

> (starts-p 1s~9s 4s~6s)

.: false

> (starts-p 4s~6s 4s~9s)

.: true

> (starts-p 5s~9s 3s~9s 2s)

.: true

```

##### Related

before-p, during-p, finishes-p, meets-p, overlaps-p

## statistics

Finds the mean, median, sigma, and count of a list of numbers.

##### Syntax
```

(statistics numbers )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| numbers | list | 1   | A list of numbers. |

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns an association list containing the mean, median, sigma, min, max. and count. |

##### Remarks

None.

##### Example
```

> (statistics (array (random 0 to 1000) each (random 0 to 10000)))

.: {mean 5601.26666 median 5701 sigma 3692.856193 min 43 max 9444 count 368}

> (statistics {6 3 1 1 5 1 0 5 5 0 2})

.: {mean 2.636363 median 2 sigma 2.1436047 min 0 max 6 count 11}

```

##### Related

probability, survey

## step

Loops a symbol over a numeric range to evaluate expressions.

##### Syntax
```

(step symbol from i limit j by k expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | An index variable to be incremented |
| from | literal | 1   | from |
| i   | number | 1   | The initial value of the variable |
| limit | literal | 1   | The literal to, above, below or go. (default is to). |
| j   | number | 1   | The final value of the variable |
| by | literal | 0-1 | by  |
| k   | number | 0-1 | The positive or negative increment for the variable |
| expression | expression | 0+  | The expression(s) to be evaluated |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last expression on the last iteration of the loop |

##### Remarks

If to is specified, the j value is included in the iteration. If below is specified the j value is excluded from the iteration. If above is specified the next number above the j value is included in the iteration. If go is specified, then the j value specifies the number of iterations.

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
```

(stream streamable )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| streamable | variant | 0+  | A file, pipe, string, or url.. |

##### Results

| Taxon | Description |
| --- | --- |
| stream | A stream resource. |

##### Remarks

A stream is a potentially infinite byte array containing serialized expressions. Serializations can be prepended to, appended to, or taken from the stream.

##### Example
```

> (function unstream {?s}

(decode (trim (string ?s) cut "|") base16))

.: unstream

> (assign ?s (stream "The quick brown fox jumped over the lazy dogs."))

.: |540068006500200071007500690063006b002000620072006f0077006e00200066006f00780020006a0075006d0070006500640020006f00760065007200200074006800650020006c0061007a007900200064006f00670073002e00|

> (unstream ?s)

.: "The quick brown fox jumped over the lazy dogs."

\>

```

##### Related

append, takeable, take, peek, peep, prepend, stream-p

## string

Converts a value to a string.

##### Syntax
```

(string value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| string | The converted value. |

##### Remarks

None.

##### Example
```

> (string {a b c})

.: "{a b c}"

> (string "a b c" (\\s) "d e f")

.: "\\"a b c\\" \\"d e f\\""

> (string 500 50 5)

.: "500 50 5"

> (string [A :B :C])

.: "[A :B :C]"

> (string the quick "brown" fox)

.: "the quick \\"brown\\" fox"

> (string)

.: ""

```

##### Related

$ concatenate, $$ elide, is

## structure

Creates a structure.

##### Syntax
```

(structure name inclusion … definition … )

inclusion ::= uses { structure … }

definition ::= slot

definition ::= slot default

definition ::= method function

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | literal | 1   | The name of the structure. |
| inclusion | expression | 0+  | The literal uses followed by a list of structure names. |
| definition | expression | 0+  | A slot definition or method definition expression |

##### Results

| Taxon | Description |
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

.: Fault

> (new Fault :What "An error" :When (moment) :Where "Over Here")

.: [Fault :What "An error" :When 20180561212150036m :Where "Over Here"]

> (structure Error

uses {Fault}

:Who )

.: Error

> (new Error :Who MyFunction :What "Punted." :When (moment) :Where "Here")

.: [Error :Who MyFunction :What "Punted." :When 20180561212489526m :Where "Here"]

```

##### Related

is, new, nix, relation, seal, structures, unseal

## structures

Creates a list of all structures.

##### Syntax
```

(structures)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of all structures. |

##### Remarks

None

##### Example
```

> (structure Foo :Bar :Baz)

.: Foo

> (structures)

.: {Failure Foo}

```

##### Related

new, nix, old, relation, relations,seal, structure, unseal

## sub

Replaces a subsequence within a sequence.

##### Syntax
```

(sub sequence entry … )

entry ::= start to end replacement

entry ::= start go length replacement

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | An assortment or sequence. |
| entry | expression | 1+  | A 4-tuple of the start position, either to position or  go length, and the replacement sequence |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | Returns the modified sequence. |

##### Remarks

Each replacement is inserted into the sequence at the indicated positions. .

##### Example
```

> (sub {the quick red fox jumped} 2 to 4 {cute pink rabbit} )

.: {the cute pink rabbit jumped}

> (sub "abcdefghij" 4 go 3 "456")

.: "abc456ghij"

> (sub "the quick brown fox jumped" 11 go 5 "green" 17 to 19 "dog")

> "the quick green dog jumped"

.: (sub {the quick brown fox jumped} 2 to 4 {cute rabbit})

.: {the cute rabbit jumped}

```

##### Related

fix, put, replace, sub

## subset

True if all elements in each subset are in the superset.

##### Syntax
```

(subset-p subset superset )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| subset | sequence | 1   | A sequence |
| superset | sequence | 1+  | A sequence |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if all elements of the subset are in the superset. |

##### Remarks

If superset and subset are strings and ordered is true, then a string search is performed.

##### Example
```

> (subset-p {a b x} {a b c d e f g})

.: false

> (subset-p {a b d} {a b c d e f g})

.: true  


> (subset-p "ick bro" "the quick brown")

.: true

> (subset-p {g h i} {a b c d e f g})

.: false

> (subset-p {e f d} {a b c d e f g})

.: true

```

##### Related

disjoint-p, intersects-p, position, in, pick

## substitute

Copies a sequence and replaces subsequences.

##### Syntax
```

(substitute sequence entry … )

entry ::= start to end replacement

entry ::= start go length replacement

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | An assortment or sequence. |
| entry | expression | 1+  | A 4-tuple of the start position, either to position or  go length, and the replacement sequence |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | Returns the modified sequence. |

##### Remarks

Each replacement is inserted into the sequence at the indicated positions. .

##### Example
```

> (substitute {the quick red fox jumped} 2 to 4 {cute pink rabbit} )

.: {the cute pink rabbit jumped}

> (substitute "abcdefghij" 4 go 3 "456")

.: "abc456ghij"

> (substitute "the quick brown fox jumped" 11 go 5 "green" 17 to 19 "dog")

> "the quick green dog jumped"

.: (substitute {the quick brown fox jumped} 2 to 4 {cute rabbit})

.: {the cute rabbit jumped}

```

##### Related

fix, put, replace, sub

## subsumes-p

True if all elements in each subset are in the superset.

##### Syntax
```

(subsumes-p superset subset … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| superset | sequence | 1   | A list or string |
| subset | sequence | 1+  | A list or string |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if superset contains all elements of each subset. |

##### Remarks

None

##### Example
```

> (subsumes-p {a b c d e f g} {a b x})

.: false

> (subsumes-p {a b c d e f g} {a b x} {a b d})

.: true  


> (subsumes-p "the quick brown" "ick bro")

.: true

> (subsumes-p {a b c d e f g} {d e f} {g h i})

.: false

> (subsumes-p {a b c d e f g} {e f d})

.: false

```

##### Related

disjoint-p, intersects-p, position, in, pick, subset-p

## such

Returns a list of thoughts.

##### Syntax
```

(such ?symbol that premises option)

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot /= value

condition ::= slot is unary-predicate

condition ::= slot not unary-predicate

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

option ::= scan number

option ::= limit number

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol| symbol | 1  | A symbol bound to a thought identifier |
| that| literal | 1  | The literal "that" |
| premises | expression | 1+  | One or more premises |
| option | expression | 0-1 | the literal "limit" followed by a number. |


##### Results

| Taxon | Description |
| --- | --- |
| list | A list of thought identifiers bound within a premise. |

##### Remarks

The limit tells how many results to return (default is infinity). 

##### Example
```

> (relation Fact :All :Are)

.: Fact

> (new Fact :All people :Are mortal) (new Fact :All philosophers :Are people)

.: Fact_1 Fact_2

> (function ExcludedMiddle {}

(with [Fact :All as ?s :Are as ?m]

[Fact :All = ?m :Are as ?p]

(no [Fact :All = ?s :Are = ?p])

list (premise (knew A :All ?s :Are ?p))))

.: ExcludedMiddle

> (ExcludedMiddle)

.: {[Fact ^ Fact_3 :All philosophers :Are mortal]}

> (such ?a that [Fact ^ as ?a :Are = mortal])

.: {Fact_1 Fact_3}

> (which Fact :Are mortal)

.: {[Fact ^ Fact_1 :All people :Are mortal]

[Fact ^ Fact_3 :All philosophers :Are mortal]}

```

##### Related

assert, assume, each, retract, such, which

## sum

Calculates the arithmetic sum.

##### Syntax
```

(sum value …)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1+  | An atom or list of atoms. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The arithmetic sum of all elements. |

##### Remarks

Returns the arithmetic sum. If the list or expression is empty, it returns zero. If the only value is a list then all elements within the list are compared, otherwise, all subsequent values are compared.

##### Example
```

> (sum {1 2 3 4 5})

.: 15

> (sum {})

.: 0

> (sum 1 2 3 4 5)

.: 15

> (sum {1 2 3} 4 {6 3 2})

.: {11 9 9}

```

##### Related

avg, max, median, min, statistics, sigma

## summation

Adds an expression over a range of values.

##### Syntax
```

(summation symbol … binding sequence expression … )

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1+  | A symbol. |
| binding | literal | 0-1 | The literal in or per. |
| sequence | sequence | 0-1 | A sequence. |
| expression | expression | 1+  | any expression involving variables from the pattern(s) |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result of applying the plus function to the expression for the indicated range. |

##### Remarks

If the binding in is specified, each symbol is bound to successive elements of the sequence. If the binding per is specified, each element is expected to be a sequence, so that each symbol is bound to subelements of each subsequence. If there are insufficient elements to bind to the symbols then the function fails. The last expression shall be evaluated and the plus function shall be applied to both that expression and any prior result. The final value is returned.

##### Example
```

> (summation ?x in (range 1 to 10) ?x)

.: 55

> (summation ?x in {1 2 3 4} (\*\* ?x 2))

.: 25

> (summation ?n in {1 2 3} (+ ?n 5))

.: 21

```

##### Related

fold, maximum, minimum, product

## supply

Applies a function to an argument list.

##### Syntax
```

(supply arguments function environment)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| arguments | list | 1   | A list containing actual parameters. |
| function | function | 1   | The name of a function to invoke |
| environment | environment | 0-1 | An environment. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | The result from applying the function. |

##### Remarks

Applies the function to the list using the supplied environment, or the current scope if no environment is provided. The function is applied to the entire list and the result is returned.

##### Example
```

> (supply {1 2 3} +)

.: 6

> (consdier {?x 9} (let ?env (scope))(let {?x 3}(supply {1 2 ?x} + ?env)))

.: 12

```

##### Related

apply, call, count, gather, map, reduce

## suppose

Performs hypothetico-deductive reasoning.

##### Syntax
```

(suppose facts action goals binding by strategies 
  via operators limit quantity gate condition 
  within timeframe before timepoint options options)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| facts | list | 1   | a list of premises |
| action | literal | 1   | one of prove, refute, solve, infer, speculate, explain |
| expression | expression | 0+  | An expression  |
| goals | list | 1   | a list of premises |
| by  | literal | 1   | the literal “by” |
| strategies | list | 1   | a list of user defined search functions. |
| via | literal | 0-1 | the literal “via” |
| operators | list | 0-1 | a list of operators |
| limit | literal | 0-1 | the literal “limit” |
| quantity | number | 0-1 | the number of solutions/proofs to generate (default is 1) |
| gate | literal | 0-1 | one of while or until |
| condition | truth | 0-1 | an expression which follows while or until (default is true) |
| within | literal | 0-1 | the literal “within” |
| timeframe | number | 0-1 | a time duration (default is eternity) |
| before | literal | 0-1 | the literal “within” |
| timepoint | number | 0-1 | an exact time (default is now + 60 seconds) |
| options | literal | 0-1 | the literal “options” |
| options | lexicon | 0-1 | a lexicon or list. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last expression. |

##### Remarks

Returns solutions (i.e. lists of operators) which transform the facts into the goals, 
or proofs (lists of operators as inference steps) showing the goals follow from the facts, 
or a truth indicating the goals are provable from the facts, by creating a monitor task and 
worker tasks which search for operator chains from facts to goals. The using function invokes 
all the supplied strategies (i.e. search functions) concurrently, canceling them if a condition 
dictates or a timeframe is passed. One or more result lists (up to the limit) is returned.

1.  If the action is solve, each solution is a list of operators.
2.  If the action is prove, each proof is a list of conclusion-operator pairs.
3.  If the action is refute, each proof is a list of conclusion-operator pairs.
4.  If the action is infer, a truth result determines if the goals are inferable from the facts.
5.  If the action is speculate, each proof is a list of conclusion-operator-probability triples.
6.  If the action is explain, each explanation lists the inferences linking goals to facts.

Each strategy (search function) needs to define keyword parameters which accept arguments from the 
using call. All the following keyword parameters are optional: solve, prove, infer, via, within, options.
 The strategy shall need to periodically check its own task identifier (by calling (cancelled-p (self)) 
 to determine if the search task has been interrupted by the monitor task.

##### Example
```

> (structure Pegs

:Left

:Temp

:Right

)

.: Pegs

> (function LeftToTemp {?state} ; a state is a list containing one Pegs structure.

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?left)(or (void-p ?temp) (< (@ ?left) (@ ?temp))))

{(new Pegs :Left (rest ?left) :Temp (& (@ ?left) ?temp) :Right ?right)}))

.: LeftToTemp

> (function LeftToRight {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?left) (or (void-p ?right) (< (@ ?left) (@ ?right))))

{(new Pegs :Left (rest ?left) :Temp ?temp :Right (& (@ ?left) ?right))}))

.: LeftToRight

> (function TempToRight {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?temp) (or (void-p ?right) (< (@ ?temp) (@ ?right))))

{(new Pegs :Left ?left :Temp (rest ?temp) :Right (& (@ ?left) ?right))}))

.: TempToRight

> (function TempToLeft {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?temp) (or (void-p ?left) (< (@ ?temp) (@ ?left))))

{(new Pegs :Left(& (@ ?temp) ?left) :Temp (rest ?temp) :Right ?right)}))

.: TempToLeft

> (function RightToTemp {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?right) (or (void-p ?temp) (< (@ ?right) (@ ?temp))))

{(new Pegs :Left ?left :Temp (& (@ ?right) ?temp) :Right (rest ?right))}))

.: RightToTemp

> (function RightToLeft {?state}

(let (@ ?state) :Left ?left :Temp ?temp :Right ?right)

(if (and (more-p ?right) (or (void-p ?left) (< (@ ?right) (@ ?left))))

{(new Pegs :Left (& (@ ?right) ?left) :Temp ?temp :Right (rest ?right))}))

.: RightToLeft

> (relation Node

:Parent

:Operator

:State

:Children {}  
:Tried {}

:Task)

.: Node

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

(let {?state ((:Operator ?child) (:State ?current))}

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

(with [Node ^ ?n] (= (:Task ?n) (self)) do (old ?p)))

?solution

)

.: depthFirstSearch

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

(let {?state ((:Operator ?child) (:State ?current))}

(put ?child :State ?state)

(if (null-p ?state)

(push ?useless ?child)

or (= ?goal ?state)

(set ?solution (only {?child}

(let {?result {}}

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

.: breadthFirstSearch

> (function TowersOfHanoi {% ?facts ?goals}

(do (let (new Pegs :Left (@ ?facts) :Temp (@ ?facts 2) :Right (@ ?facts 3))}

solve {(new Pegs :Left (@ ?goals) :Temp (@ ?goals 2) :Right (@ ?goals 3))}

by {depthFirstSearch breathFirstSearch}

via {LeftToTemp LeftToRight TempToLeft TempToRight RightToTemp

RightToLeft})

)

.: TowersOfHanoi

> (TowersOfHanoi facts {{1 2 3} {} {}} goals {{}{}{1 2 3}})

.: {{LeftToRight LeftToTemp RightToTemp LeftToRight TempToLeft TempToRight LeftToRight}}

> (TowersOfHanoi facts {{3}{1 2}{}} goals {{}{}{1 2 3}})

.: {{LeftToRight TempToLeft TempToRight LeftToRight}}

> (TowersOfHanoi facts {{1 2} {} {}} goals {{}{}{1 2}})

.: {{LeftToTemp LeftToRight TempToRight}}

```

##### Related

assume, old, use

## survey

Creates a list of referents or referent-count pairs.

##### Syntax
```

(survey format relation slot)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| format | literal | 1   | One of values, counts. |
| relation | relation | 1   | A relation |
| slot | slot | 1   | The slot of interest |

##### Results

| Taxon | Description |
| --- | --- |
| list | An association list or list of all values contained in the slot. |

##### Remarks

Returns a list values or an association list of counts (i.e., observations) for a relation slot

##### Example
```

> (relation Fruit :Color :Type)

.: Fruit

> (new Fruit :Color red :Type apple) (new Fruit :Color red :Type cherry)

.: Fruit_1 Fruit_2

> (new Fruit :Color red :Type strawberry)

.: Fruit_3

> (survey values Fruit :Color)

.: {red red red}

> (survey counts Fruit :Type)

.: {{apple 1}{cherry 1}{strawberry 1}}

```

##### Related

probability, statistics

## swap

Modifies a sequence by interchanging values.

##### Syntax
```

(swap sequence substitution …)

 substitution ::= prior-position later-position

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A list or a string. |
| substitution | expression | 1+  | A prior and later position pair.  <br>A position may be a number o a list of numbers.. |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The modified sequence |

##### Remarks

Destructively modifies the sequence. No changes occur if prior and later are the same. To create a new sequence use the exchange function.

##### Example
```

> (swap {A B C} 1 3)

.:{C B A}

> (swap "ABCD" 1 3)

.:'CBAD'

> (swap {{1 2 3}{4 5 6}} {2 1} {1 3})

.: {{1 2 4}{3 5 7}}

```

##### Related

@ element, append, exchange, fix, push, pop

## symbol

Creates a symbol.

##### Syntax
```

(symbol name )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| name | variant | 0-1 | A string, literal or integer. |
| environment | environment | 0-1 | An environment (defaults to the current scope). |

##### Results

| Taxon | Description |
| --- | --- |
| symbol | A symbol |

##### Remarks

The current environment is available via scope. If no arguments are suppled, then a new symbol is returned for the current context based on the value "s".

##### Example
```

> (symbol)

.: ?s-1

> (use User)

.: User

> (modular (symbol 500) nil (symbol) 350)

.: true

> (entries (scope (use)))

.: {{?500 nil} {?s-2 350}}

```

##### Related

<-- before tie, --> after tie, add, assign, assume, is, presume, scope, set, tie

## symbols

Lists the symbols in an environment.

##### Syntax
```

(symbols scope option )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| scope | variant | 1   | A environment. or module. |
| opetion | expression | 0-1 | A key value pair, one of:  <br>ancestors truth - Search ancestors. (Default is false.) |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of symbols defined in the environment, and parent environments. |

##### Remarks

If ancestors is true, then the symbols from parent environments are gathered recursively.

##### Example
```

> (let ?x 1 ?y 2 ?z 3) (scope)

.: true {?x ?y ?z}

> (module Mine

(modular ?foo bar))

.: Mine

> (symbols (scope at Mine))

.: {?foo}

> (let {?g 7 ?h 8 ?i 9}

(let {?d 4 ?e 5 ?f 6}

(let {?a 1 ?b 2 ?c 3}

(symbols (scope) ancestors true))))

.: {?a ?b ?c ?d ?e ?f ?g ?h ?i}

```

##### Related

environment, functions, module, modules, scope, symbol

## take

Creates an expression from a readable sequence.

##### Syntax
```

(take readable options …)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| readable | variant | 1   | An file, stream, or string. |
| options | expression | 0-2 | A key value pair, one of:  <br>start position - Place to setart parrsing. (Default is 1). limit quantity - Number of parses to make (Default is 1.) |

##### Results

| Taxon | Description |
| --- | --- |
| expression | The parsed expression and the next position to parse in the readable. |

##### Remarks

Returns an expression containing a list of the extracted expression(s) according to SubSubThought Premise Language syntax, and the last parsed position in the readable. If limit is not supplied, the limit becomes one, the next expression is returned. If limit is greater than one then as many expressions are returned as can be extracted up to the limit. If # is provided as the limit, then all remaining expressions are returned. This function returns an empty expression if no expression could be extracted. It's recommended to test the argument prior to parsing using the takeable function.

##### Example
```

> (take (stream ""))

.: 0

> (take "hello world")

.: hello 7

> (take (stream "hello world" #) start 7)

.: world 12

> (take "{the quick brown fox} jumped over the lazy dogs" start 23 limit 3)

.: jumped over the 39

```

##### Related

append, peek, prepend, skip, stream, stream-p, takeable, whitespace-p

## takeable

Calculates the number of expressions that can be read.

##### Syntax
```

(takeable readable options …)

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| readable | variant | 1   | A stream, or file resource or a string containing zero or more expressions. |
| options | expression | 0-2 | A key value pair, one of:  <br>start position - Place to setart parrsing. (Default is 1). want quantity - Number of parses to make (Default is #.) |

##### Results

| Taxon | Description |
| --- | --- |
| number | Calculates the number of actual expression that can be taken. . |

##### Remarks

If want is greater than one then as many expressions are tested for completeness as can be extracted up to the count. If # is provided, then all remaining expressions are tested for completeness. After testing, the resource shall be unchanged. Returns a number up to the number of desired expressions that can be successfully taken (because they are complete).

##### Example
```

> (global ?Stream (stream "The quick brown fox {jumped} "))

.: true

> (takeable ?Stream)

.: 4

> (takeable ?Stream #)

.: 4

> (takeable ?Stream 2)

.: 2

```

##### Related

skip, append, take, peek, prepend, stream, stream-p

## tally

Returns the number of matches in the knowledge base.

##### Syntax
```

(tally pattern option )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| pattern | pattern | 1   | A grounded premise |
| option | expression | 0+  | An option for retrieving the bindings. limit n - the number of results to return. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of all symbol value pairs |

##### Remarks

Returns an anonymous list generator containing lists of symbol value lists.

##### Example
```

> (relation Poll :Response)

.: Poll

> (step ?i from 1 to 1000

(new Poll :Response (on (> (radom 0 to 1) 0) Yes No)))

.: Poll_1000

> (tally [Poll :Respones Yes])

.: 672

```

##### Related

tally, using, with

## tangent

Calculates the tangent.

##### Syntax
```

(tangent number geometry metrum)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |
| geometry | literal | 0-1 | One of: cir(cle), hyp(erbola). Default is circle. |
| metrum | literal | 0-1 | One of: degrees, radians. Default is radians. |

##### Results

| Taxon | Description |
| --- | --- |
| number | The tangent of the number. |

##### Remarks

None.

##### Example
```

> (tangent 5)

.: -3.38051500625

> (tangent 5 cir radians)

.: -3.38051500625

> (tangent 120 degrees)

.: 1.7320508075

> (tangent 45 hyp degrees)

.: 0.655794202632

> (tangent (pi) hyp radians)

.: 0

```

##### Related

acotangent, atangent, cotangent

## tarry

Allows tasks to complete on their own.

##### Syntax
```

(tarry tasks expression …) )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| tasks | variant | 1   | A task or list of task resources. |
| expression | variant | 0+  | An expression to evaluate after the tasks are completed. |

##### Results

| Taxon | Description |
| --- | --- |
| list | The task resources. |

##### Remarks

This function allows tasks to complete in a non-blocking manner. It is equivalent to

(given {?tasks}

(& ?tasks

(concurrent (do (until (every ?t in ?tasks (ready-p ?t))(idle 1m)) ready))))

##### Example
```

> (assign ?tasks (tarry (concurrent (repeat 1000000 foo)

(repeat 2000000 bar)

(repeat 3000000 baz))))

.: {task-1 task-2 task-3 task-4}

> (map ?tasks ({?t}(await ?t 0s)))

.: {­foo bar baz done}

> (free (tarry (complete

(repeat 1000 foo)

(repeat 2000 bar)

(repeat 3000 baz))))

.: freed

```

##### Related

wait, abort, concurrent, await, complete, do, done-p, free, task

## task

Creates a list of tasks for deferred evaluation.

##### Syntax
```

(task cell scope expression … )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| cell | cell | 0-1 | A cell. |
| scope | environment | 0-1 | An environment. A child scope is created if not provided. |
| expression | expression | 1+  | Any expression to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of task resources, one resource for each expression. |

##### Remarks

The tasks need to be initiated with the concurrent or complete function.

##### Example
```

> (task (/ 1000 57) (\*\* 4 20) (\*\* 4 20))

.: {Task-1 Task-2 Task-3}

> (concurrent task-1)

.: {Task-1}

> (await task-1)

.: 17.54385964912281

> (concurrent task-2 task-3)

> (await task-2)

.: 1099511627776

> (await task-3)

.: 1099511627776

> (free {task-1 task-2 task-3})

.: nil

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

.: main

> (main)

Hello World

.: freed

```

##### Related

wait, abort, concurrent, await, busy-p, cancel, cancelled-p, complete, critical, do, is, ready-p, reclaim , task

## tasks

Creates a list of all tasks.

##### Syntax
```

(tasks)

```
##### Module

Tasks

##### Parameters

None.

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list of task handles |

##### Remarks

This list does not include the interpreter task. To obtain the interpreter task, use the self function.

##### Example
```

> (task (apply + {1 2 3}))

.: {Task-1}

> (complete (apply \* {1 2 3}))

.: {Task-2}

> (tasks)

.: {Task-2 Task-1}

> (free (tasks))

.: freed

```

##### Related

wait, abort, concurrent, await, task, await, complete, reclaim, self, task

## taxon

Returns the taxonomic (i.e., data) type of a value.

##### Syntax
```

(taxon value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | A taxonomic type name |

##### Remarks

None

##### Example
```

> (taxon true)

.: truth

> (taxon nil)

.: nothing

> (taxon 12345)

.: number

> (taxon #)

.: literal

```

##### Related

convert, convertible, taxonomy, identity, is, meron, meronomy, relation, structure

## taxon-p

True if the value is of the specific taxonomic type.

##### Syntax
```

(taxon-p value taxon )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |
| taxon | literal | 1   | The name of a taxon. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is the taxon. |

##### Remarks

None.

##### Example
```

> (taxon-p 500 literal)

.: false

> (taxon-p 300t time)

.: true

> (taxon-p "the quick brown fox" string)

.: true

```

##### Related

meron, meron-p, meronomy, taxon, taxonomy

## taxonomy

Returns a list of taxonomic types for a value.

##### Syntax
```

(taxonomy value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value |

##### Results

| Taxon | Description |
| --- | --- |
| list | The taxonomic types used |

##### Remarks

None

##### Example
```

> (taxonomy A)

.: {literal atom thing}

> (taxonomy 100)

.: {number atom thing}

> (taxonomy {a b c})

.: {list sequence thing}

> (taxonomy [A :B 1 :C 2])

.: {premise tuple sequence thing}

> (taxonomy 522t)

.: {tick time atom thing}

```

##### Related

taxon, is, id, meron, meronomy, relation, structure

## tell

Sends a message to a recipient.

##### Syntax
```

(tell who message option … )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| who | literal | 1   | A URL web resource or the literal user. |
| message | string | 1   | A message or command.. |
| option | expression | 0+  | Key value pairs timeout instant – delay before terminating request,  <br>default value – value to return upon timeout, |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns told if successful. If a default is provided then the default is returned in case of a timeout. |

##### Remarks

If user is specified for who, then the output is displayed to the console.

##### Example
```

> (tell user "Hello World!\n")

Hello World

.: told

> (function reply {?url ?message}

(tell ?url ($ received ?message)))

.: reply

> (service (url scheme tcp port 5950) reply)

.: Service-1

> (ask (url scheme tcp port 5950) "secret")

.: "received secret"

> (free Service-1)

.: freed

> (global ?Data (data source (get Settings-1 "/db/dsn")))

.: true

> ?Data

.: Data-1

> (open ?Data)

.: Data-1

> (tell ?Data "update product set price = price \* 1.1025;")

.: told

> (close ?Data)

.: closed

```

##### Related

ask, listen,free


## that

Returns true if premises are true.

##### Syntax
```

(that premise … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| premise | premise | 1+ | an ephemeron or thought premises |


##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the premises are true, otherwise false. |

##### Remarks

Each thought premise is added to the knowledge base.


##### Example
```

> (use (conceive)  
	(relation Sibling :Who :Sibling)
	
	(assert
	   [Sibling :Who Jane :Sibling Mary])

    (knew ?sibling :Who Mary :Sibling Jane)


	(tell user ($ Jane and Mary are (on (that [Sibling :Who Jane :Sibling Mary]) (nothing) not) siblings.))
  )	

Jane and Mary are siblings.
.: told

```

##### Related

assume, assert, which, with

## there

True if a file, folder, or url actually exists.

##### Syntax
```

(there url )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| url | url | 1   | A url. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the url exists.. |

##### Remarks

This function checks whether or not the url exists.

##### Example
```

> (let ?url (ul path "quick.txt"))

.: true

> (if (there ?url)

(let ?file (file url ?url seek 1 mode write erase yes))

(write ?file "The quick brown fox")

(close ?file))

.: closed

```

##### Related

absent, file, folder, url

## this

The current element of a series.

##### Syntax
```

(this series)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| series | series | 1   | A series. |

##### Results

| Taxon | Description |
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

.: walk

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
```

(thought relation id )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| relation | literal | 1   | A relation |
| id  | number | 1   | An instance number |

##### Results

| Taxon | Description |
| --- | --- |
| thought | A thought. |

##### Remarks

Returns an existing thought, otherwise signals a failure If the thought does not exist.

##### Example
```

> (relation E :Value)

.: E

> (new E :Value 100)

.: E_1

> (new E :Value 200)

.: E_2

> (thought E 1)

.: E_1

> (thought E 2)

.: E_2

> (thought E 3)

.: [Failure :Name NotFound :Text "Thought E_3 was referenced but not found."]

```

##### Related

^ thought id, id, is, premise

## thunk

Creates a thunk in a module.

##### Syntax
```

(thunk expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | variant | 0+  | Expressions to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| thunk | Returns the thunk containing the expressions. |

##### Remarks

A thunk is a parameterless anonymous function. A thunk is equivalent to lambda expression without parameters in the Lisp programming language, and can be used in most places a function name is required. Anonyms cannot be recursive, since they are unnamed. Continuations may be taken within an anonym. Neither do anonyms use tags that can be reference by a return. Since no parameters are specified, each expression is executed in succession and the value of the last expression is returned. The thunk is ephemeral because function definitions are not maintained for them.

##### Example
```

> (thunk (tell user "Hello, world."))

.: (thunk (tell user "Hello, world."))

> (invoke (thunk (tell user "Hello, world.")))

Hello, world.

.: told

```

##### Related

wait, abort, concurrent, await, complete, done-p, reclaim,task, use

## thunks

Returns a list of thunks defined in a module.

##### Syntax
```

(thunks module)

```
##### Module

KB

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

.: Mine

> (thunks Mine)

.: {thunk-1}

> (use User)

.: User

> (thunk “hello world”)

.: thunk-2

> (thunks)

.: {thunk-2}

```

##### Related

function, module, modules, rule, rules, symbols

## tick

Creates a tick or returns nanoseconds since year zero.

##### Syntax
```

(tick nanoseconds)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| nanoseconds | number | 0-1 | A number of nanoseconds. |

##### Results

| Taxon | Description |
| --- | --- |
| tick | nanoseconds since the year zero. |

##### Remarks

If no argument is supplied, this function returns the current date and time in nanoseconds, otherwise it attempts to construct a tick from the supplied argument.

##### Example
```

> (tick)

.: 63552721198807000t

> (tick 5465464)

.: 5465464t

```

##### Related

date, moment, idle

## tie

Assigns symbols to values. .

##### Syntax
```

(tie manner assignment ... )

assignment ::= symbol value

assignment ::= {symbol ... } list

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| manner | literal | 0-1 | The manner in which the assignements are performed either the literal parallel or tandem (default if omitted) |
| assignment | expression | 1+  | A symbol and value pair. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | Returns the last assigned value. |

##### Remarks

If a list of symbols is provided for an assignment, then the value must be a list with the corresponding number of elements. The symbol must have previously been defined otherwise a symbol not found failure shall occur. Returns the value of the last assignment. If parallel is specified as the manner, the symbols are defined in parallel, otherwise the symbols are assigned in tandem (by default).

##### Example
```

> (tie ?person DrWho)

.: DrWho

> ?person

.: DrWho

> (tie parallel {?x ?y ?z} {1 2 3})

.: 3

```

##### Related

<-- before tie, --> after tie, assume, constant, dynamic, given, global, local, presume

## time

Performs time operations.

##### Syntax
```

(time unit operation value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| unit | literal | 1   | one of { year, month, week, weekday, days, day, hour, minute, second, millisec, moment, microsec, nanosec, tick, zone. zmin }. |
| operation | literal | 1   | One of {\+ (addition), - (difference), of, in, part, ytd} |
| value | time | 1+  | A time value |

##### Results

| Taxon | Description |
| --- | --- |
| number | The operation performed on the time value(s). |

##### Remarks

Returns the value of the operation in the specified units. If + is specified as the operation, the times are added together and the total is returned in the unit. If \- is specified as the operation, the difference of the times are returned in the specified unit. If of is specified for the operation, then the specified unit is extracted for the specified time value. If in is specified for the operation, then the total time value is converted to the units. If part is specified for the operation, and if the time is converted to a moment segment (day part takes a number between 1 and 366, returning a number between 1 and 999; hour part takes takes a number between 0 and 23, returning a number between 0 and 99; minute part takes a number between 0 and 59, returning a number between 0 and 99; seconds part takes a number between 0 and 59, returning a number between 0 and 99). If ytd is specified then the units are computed for the year to date for the date specified as the time. Otherwise the part of the time value is returned.

##### (imExample

> (time seconds - 5s 10s)

.: -5

> (time hour part 18)

.: 75

> (time seconds in 26226s)

.: 26226

> (time day ytd 2014-04-09T14:24:19.488Z)

.: 9

> (time month of (tick))

.: 12

> (time month of (moment))

.: 12

> (time month of (date))

.: 12

> (@ {mon tue wed thu fri sat sun} (time weekday part (date 2019 8 31)))

.: sat

##### Related

date, epoch, interval, is, moment, second, tick

## top

Creates a subsequence of the first elements.

##### Syntax
```

(top sequence count)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The sequence to search |
| count | number | 0-1 | The number of elements.( Default is 1.) |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A sub sequence containing the desired quantity of elements |

##### Remarks

None.

##### Example
```

> (top {a b c d e f g} 3)

.: {a b c}

> (top {a b c d e f g})

.: {a}

```

##### Related

@ element, but, last, rest

## transfer

Transfers a value from one sequence to another.

##### Syntax
```

(transfer source destination option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| source | symbol | 1   | A symbol bound to a sequence |
| destination | symbol | 1   | A symbol bound to a sequence |
| option | expression | 0+  | A key value pair where the key is from position - The position in the source (defaults to 1) to position - The position in the destination (defaults to 1)  <br>unique prohibited (Boolean) - indicates if duplicate values are allowed. (Default is false.) |

##### Results

| Taxon | Description |
| --- | --- |
| value | Returns the value that was transferred. |

##### Remarks

Modifies two sequences by removing a value from the source and adding a value to the destination.

##### Example
```

> (let ?x {a b c d e f} ?y {})

.: true

> (transfer ?x ?y)

.: a

> (transfer ?x ?y unique true from 2 to 2)

.: c

> ?x ?y

.: {b d e f} {a c}

```

##### Related

but, exchange,last, pop, push, rest, reverse, swap, top

## traverse

Loops through the coordinates of a sequence.

##### Syntax
```

(traverse symbol binding sequence limit dimensions expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol holding the index or coordinates of the current element of the sequence. |
| binding | literal | 1   | One of the following: into - varies the inner (rightmost) coordinates first across - varies the outer (leftmost) coordinates first. |
| sequence | sequence | 1   | A possibly nested sequence. |
| limit | literal | 1   | the keyword literal limit |
| dimensions | list | 1   | if the keyword limit is supplied, then this is a list of indicies indicating the maximum dimensions that shall be traversed. |
| expression | expression | 0+  | An expression to be evaluated. |

##### Results

| Taxon | Description |
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
```

(trim sequence option … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | The target sequence |
| option | expression | 0+  | A key value pair: cut delimiters - a string or list containing the delimiters. on location - the literal left, right, or both (default). |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | The modified sequence |

##### Remarks

Removes delimiter characters from the front or rear of a sequence. If the location is left, then only the left portion is trimmed. If the location is right, then only the right portion of the string is trimmed. If the location is both or if the location is omitted, then both the left and right portion of the sequence is trimmed.

##### Example
```

> (trim " the quick brown fox ")

.: "the quick brown fox"

> (trim " the_quick_brown_fox \__" cut "\_")

.: " the_quick_brown_fox "

> (trim " the quick brown fox " on left)

.: "the quick brown fox "

> (trim {the quick brown fox} cut {the fox} on both)

.: {quick brown}

```

##### Related

split

## truncate

Rounds a number towards zero.

##### Syntax
```

(truncate number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number. |

##### Results

| Taxon | Description |
| --- | --- |
| number | An integer |

##### Remarks

None.

##### Example
```

> (truncate 10.5)

.: 10

> (truncate 10.4)

.: 10

> (truncate 10.49)

.: 10

> (truncate -10.5)

.: -10

> (truncate -10.4)

.: -10

> (truncate -10.49)

.: -10

```

##### Related

%, ceiling, floor, round,

## try

Evaluates expressions and recovers from signals.

##### Syntax
```

(try expression … learn symbol recovery … finally cleanup … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| expression | expression | 1+  | Expressions to do some processing |
| learn | literal | 1   | The literal learn |
| symbol | symbol | 0-1 | A failure cause variable |
| recovery | expression | 0+  | Expressions for failure recovery and learning |
| finally | literal | 0-1 | The literal finally |
| cleanup | expression | 0+  | Expressions to do some clean up |

##### Results

| Taxon | Description |
| --- | --- |
| value | Returns last call in normal operation, or last failure call if a failure was thrown |

##### Remarks

Try performs failure handling The fail function shall return to the learn tag and bind the failure to the symbol. The escape function shall return to the resume tag. If failure is learned, it shall be returned.

##### Example
```lisp

> (function main {& list ?args}
    (tell user ($ \n Attempting dangerous operation... \n))
    (try
      (dangerousOperation)
      (tell user ($ \n Goodbye \n))
     learn ?cause
      (case (:Name ?cause)
       of ResourceFailure
          (tell user ($ Resource failure occurred \n))
       else
          (tell user ($ \n (:Text ?cause) \n)))
          (tell user ($ \n Goodbye \n))
          (resignal ?cause) ; rethrow failure
      finally
       (tell user ($ Whew, we dodged a bullet.)))
   )

.: main

> (main)

Attempting dangerous operation...

The function dangerousOperation not defined.

Goodbye

.: [Failure :Name User :Text "The function dangerousOperation was not found."]

> (let {?file nil}

(try

(set ?file (file name "quick.txt" seek 1 mode read type text))

(tell user ($ (read ?file) \n))

learn ?e

(signal ?e)

finally

(close ?file)))

The quick brown fox jumped over the lazy dogs.

.: told

> ; implement a REPL.  


    (forever

(tell user ($ "\n=>" (try (eval (ask user "\n\* ")) learn ?failure))))

\* HELLO WORLD

\=> HELLO WORLD

\*

```

##### Related

can, confirm, confute, did, ensure, escape, fail, may, signal

## tuple

Creates a tuple.

##### Syntax
```

(tuple value … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0+  | Any value |

##### Results

| Taxon | Description |
| --- | --- |
| tuple | Returns a tuple containing the values. |

##### Remarks

A tuple can also be created by simply enclosing the elements with square brackets, [ ].

##### Example
```

> (tuple a b c {d})

.: [a b c {d}]

> (tuple "a b c")

.: ["a b c"]

> (tuple 500)

.: [500]

> (tuple)

.: []

> [a b c {d}]

.: [a b c {d}]

> ["a b c"]

.: ["a b c"]

```

##### Related

&, inside, list-p, sequence-p  

## uid

Creates a unique identifier.

##### Syntax
```

(uid)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| uid | A new unique identifier. |

##### Remarks

None.

##### Example
```

> (uid)

.: 90A836B0-63E8-4049-B411-908A6B30F69F

> (uid)

.: CE79CB00-F400-429A-BFC3-8F9801B7B017

```

##### Related

id, unique

## unbound

Creates a list of free symbols in a function.

##### Syntax
```

(unbound function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of symbols not declared in the parameter list (aka free variables). |

##### Remarks

None.

##### Example
```

> (function foo {?x ?y + ?z}

(bar ?x ?y)

(baz ?z ?a))

.: foo

> (bound foo)

.: {?x ?y ?z}

> (unbound foo)

.: {?a}

> (bound (' (given {?s} (@ ?s ?p))))

.: {?s}

> (unbound (' (given {?s} (@ ?s ?p))))

.: {?p}

```

##### Related

bound

## unbound-p

True if a symbol is unbound.

##### Syntax
```

(unbound-p symbol)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| symbol | symbol | 1   | A symbol. |

##### Results

| Taxon | Description |
| --- | --- |
| bool | True if the symbol is unbound. |

##### Remarks

None.

##### Example
```

> (let ?a 1 ?b 2)

.: true

> (unbound-p ?a)

.: false

> (unbound-p ?b)

.: false

> (unbound-p ?c)

.: true

```

##### Related

unbound-p

## unicode

The Unicode of a string’s first position.

##### Syntax
```

(unicode string)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | input string |

##### Results

| Taxon | Description |
| --- | --- |
| number | The Unicode of the first position |

##### Remarks

None

##### Example
```

(unicode "A")

.: 65

(Unicode "apple")

.: 97

```

##### Related

char, format, lexemes, lowercase, ngrams, split, trim, uppercase

## union

Concatenates sequences removing duplicates.

##### Syntax
```

(union sequence sequence … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 2+  | input sequences |

##### Results

| Taxon | Description |
| --- | --- |
| sequence | A single de-duped sequence. |

##### Remarks

None

##### Example
```

> (union {a b c} {b c d} {d e f})

.: {a b c d e f}

> (union "abc" "bcd" "def")

.: "abcdef"

```

##### Related

difference, disjoint, distinct, intersection

## unique

Creates a unique literal based on a prefix.

##### Syntax
```

(unique prefix)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| prefix | variant | 0-1 | A literal or string prefix for the id. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | A new literal |

##### Remarks

If prefix is not provided the default prefix "G" is used. Hyphens and underscores are removed from the prefix. This function increments a counter to generate a new literal.

##### Example
```

(unique)

.: G1

(unique)

.: G2

(unique "hello")

.: hello1

(unique My-Object)

.: MyObject1

(unique "my_Object_")

.: MyObject2

(unique "my-object-")

.: MyObject3

```

##### Related

Id, uid

## unless

Branched conditional evaluation.

##### Syntax
```

(unless condition false-case true-case )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| false-case | variant | 1   | An expression to evaluate |
| true-case | variant | 1   | An expression to evaluate |

##### Results

| Taxon | Description |
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
```

(unlike sequence pattern)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A string or list of strings to be compared. |
| pattern | string | 1   | A regex pattern. |

##### Results

| Taxon | Description |
| --- | --- |
| variant | If sequence is a string, then a truth is returned. If sequence is a list, then a list of non-matches is returned |

##### Remarks

If the candidate argument is a list, then this function Creates a new list containing only those elements not matching the pattern. If the candidate is a string, then this function returns true if the pattern does not match the candidate, and false otherwise. Standard RegEx matching is used.

##### Example
```

> (unlike "abc" "bc")

.: false

> (unlike "abc" "xy")

.: true

> (unlike {"abc" "bcd" "def" "ghi"} "bc")

.: {"def" "ghi"}

```

##### Related

like

## unqualified

The function literal without the module prefix.

##### Syntax
```

(unqualified function)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| function | function | 1   | A function literal |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The function literal without a module |

##### Remarks

None

##### Example
```

> (unqualified Math.sum)

.: sum

```

##### Related

qualified, qualifiers

## unseal

Permits new records for a protoytpe.

##### Syntax
```

(unseal prototype)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| prototype | literal | 1   | The name of a prototype. |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns unsealed |

##### Remarks

Calling the new function on a sealed relation shall fail. Sealed relations must be unsealed before the new function shall work again.

##### Example
```

> (relation Q)

.: Q

> (new Q)

.: Q_1

> (seal Q)

.: sealed

> (new Q)

.: [Failure :Name Permission :Text "Attempt to modify sealed relation Q"]

> (unseal Q)

.: unsealed

> (new Q)

.: Q_2

```

##### Related

new, relation, seal, structure

## unsigned

Converts a value to an unsigned number.

##### Syntax
```

(unsigned value )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A number value or the literal minimum or maximum |

##### Results

| Taxon | Description |
| --- | --- |
| integer | An integer number. |

##### Remarks

If the value is minimum (or maximum) the minimum (or maximum) unsigned number is returned; otherwise, if the value cannot be converted to an unsigned number, the function fails. The fractional part of the number shall be truncated.

##### Example
```

> (unsigned {a b c})

.: [Failure :Name ArgumentValue :Text "{a b c} is not a number."]

> (unsigned "a b c")

.: [Failure :Name ArgumentValue :Text "'a b c' is not a number."]

> (unsigned 500.3)

.: 500u

> (unsigned "23.4")

.: 23u

> (unsigned (\* 2 2))

.: 4u

```

##### Related

ceiling, complex, floor, is, long, rational, real, round, truncate  

## until

Loops expressions until a condition is true.

##### Syntax
```

(until condition expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| expression | expression | 0+  | An expression to be evaluated |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last value of the last iteration |

##### Remarks

None

##### Example
```

> (modular ?i 0)

.: true

> (until (>= ?i 10) (idle 1s) (--> ++ ?i))

.: 10

```

##### Related

for, iterate, loop, repeat, step, while

## unwrap

Permits modifications to a module.

##### Syntax
```

(unwrap module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | literal | 1   | A module |

##### Results

| Taxon | Description |
| --- | --- |
| literal | Returns unwrapped |

##### Remarks

This function has no effect on already unwrapped modules.

##### Example
```

> (module Math

(function sum ?args (apply + ?args)))

.: Math

> (wrap Math)

.: wrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.: [Failure :Name Permission :Text "Can't modify a wrapped module"]

> (unwrap Math)

.: unwrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.: Math

```

##### Related

extend, module, wrap

## uppercase

Converts a string touppercase.

##### Syntax
```

(uppercase string)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| string | string | 1   | A value to convert |

##### Results

| Taxon | Description |
| --- | --- |
| string | The converted string |

##### Remarks

None

##### Example
```

> (uppercase "the quick brown fox")

.: "THE QUICK BROWN FOX"

```

##### Related

capitalize, lexemes, lowercase

## uppercase-p

True if a string's first position is upper case.

##### Syntax
```

(uppercase-p value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the value is a string and its first position is upper case. |

##### Remarks

None

##### Example
```

> (uppercase-p "the quick brown fox")

.: false

> (uppercase-p "This and that")

.: true

```

##### Related

letter-p, lowercase-p

## url

Creates a URL resource.

##### Syntax
```

(url option … )

(url address )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| address | string | 0-1 | The url address. |
| option | expression | 0+  | A key value pair. One of scheme scheme \- the url scheme (e.g., file, http, https) user user \- the name of the user password password \- the password of the user host host - hostname or the literal ip for this ip address port port \- port number or the literal new path path \- file path query query \- query key value pairs. fragment fragment - section specification.. address url - A full url address. |

##### Results

| Taxon | Description |
| --- | --- |
| url | A url resource. |

##### Remarks

If no arguments are provided, then this function returns the universal resource locator for the SubSubThought Premise Language interpreter running on the current machine. If new is specfied as the port, an unused port number is utilized.

##### Example
```

> (url scheme https host "www.youtube.com" path "watch" query "v=kqicbyONxO8")

.: Url-1

> (address Url-1)

.: "https://www.youtube.com/watch?v=kqicbyONxO8"

```

##### Related

address, ask, is, listen, tell

## use

Creates a scope for knowledge based operations.

##### Syntax
```

(use knowledge expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| knowledge | variant | 1   | A knowledge base or url to a knowledge base. |
| expression | variant | 0+  | An expression. |

##### Results

| Taxon | Description |
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

(with [Fact :All as ?x :Are as ?y]

[Fact :All = ?y :Are as ?z]

list (knew [Fact :All ?x :Are ?z]))

)

.: Fact_3

> (use

(knowledge name Mathematics path "c:/premise/kb/" units MB size 2 max 10

log 1 growth 10)

(relation Circle :Radius)

)

.: Circle

```

##### Related

attach, detach, each, get, knowledge, put, using, which, with

## values

Creates a list of values for an assortment.

##### Syntax
```

(values assortment)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| assortment | assortment | 1   | A environment, enumeration, or lexicon. |

##### Results

| Taxon | Description |
| --- | --- |
| list | A list of values |

##### Remarks

For collections this function returns the same result as the keys function.

##### Example
```

> (global ?M nil)

.: true

> (set ?M (lexicon :X 1 !m noop :T nil A 2))

.: true

> (values ?M)

.: {1 noop nil 2}

> (filter (keys ?M) (given {?v} (term-p ?v)))

.: {:X !m :T}

> (filter (values ?M) (given {?v} (not (term-p ?v))))

.: {1 noop nil 2}

> (values (collection the quick brown fox))

.: {the quick brown fox}

```

##### Related

@ element, add, bindings, cut, free, get, in, key, keys, size

## vector

Creates a vector of atoms.

##### Syntax
```

(vector atom … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| atom | atom | 0+  | An atomic value such as a number, time, or literal. |

##### Results

| Taxon | Description |
| --- | --- |
| vector | Returns a vector containing the atoms. |

##### Remarks

A vector is an immutable sequence of atoms. Vectors can also be created by simply enclosing the elements with vertical bars called pipes ( | ). Whenever vectors are manipulated, a new vector is created. Vectors cannot be embedded, and cannot contain sequences.

##### Example
```

> (vector a b c d)

.: |a b c d|

> (vector 500)

.: |500|

> (vector foo)

.: |foo|

> |a b c d|

.: |a b c d|

```

##### Related

& merge, && abridge, inside, list

## version

Provides version information.

##### Syntax
```

(version)

```
##### Module

KB

##### Parameters

None

##### Results

| Taxon | Description |
| --- | --- |
| nil | Returns nil |

##### Remarks

Prints system and version information.

##### Example
```

> (version)

[Premise :Version 0.2.0 20180201.001 :OS Windows 10 :Edition Community]

.: nil

```

##### Related

bye, help, copyright

## void-p

True if a container has zero elements.

##### Syntax
```

(void-p sequence)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the sequence has zero items. |

##### Remarks

True if the container has zero items.

##### Example
```

> (void-p "not empty")

.: false

> (void-p (expression))

.: true

> (void-p "")

.: true

> (void-p {})

.: true

> (void-p (call))

.: true

> (void-p [])

.: true

```

##### Related

more-p

## wait

Waits for tasks to end.

##### Syntax
```

(wait tasks timeout )

```
##### Module

Tasks

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| tasks | list | 1   | A list of task resources |
| timeout | instant | 0-1 | The amount of time to wait for the task. The default is eternity which implies to wait indefinitely |

##### Results

| Taxon | Description |
| --- | --- |
| list | The task resources. |

##### Remarks

The wait function waits for either the timeout duration or for the task to complete. This function allows tasks to complete in a blocking manner.

##### Example
```

> (assign ?tasks (wait (concurrent (repeat 1000000 foo)

(repeat 2000000 bar)

(repeat 3000000 baz))

10s))

.: {task-1 task-2 task-3}

> (map ?tasks (given {?t}(await ?t 0s)))

.: {foo bar baz}

> (free (wait (complete

(repeat 1000 foo)

(repeat 2000 bar)

(repeat 3000 baz))))

.: freed

```

##### Related

wait, abort, concurrent, await, complete, do, done-p, free, task, tarry

## which

Creates a list of thoughts for a pattern..

##### Syntax
```

(which category criterion … option …)

category ::= relation

category ::= list

criterion := slot binding

criterion ::= slot condition

criterion ::= slot condition

binding ::= as symbol

iteration ::= each symbol

condition ::= slot \= value

condition ::= slot /\= value

condition ::= is unary-predicate

condition ::= not unary-predicate

condition ::= binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

option ::= scan number

option ::= limit number

option ::= group slot … by slot … into symbol

option ::= merge value …

option ::= sort ordering …

ordering ::= term comparator

action ::= give expression

action ::= list value …

action ::= tally

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| relation | variant | 1   | A relation name or list of thoughts. |
| criterion | expression | 0+  | A slot referent pair or method function pair. |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |

##### Results

| Taxon | Description |
| --- | --- |
| list | Returns a list of premises matching the pattern. |

##### Remarks

Looks for existing thoughts matching the criteria. If no symbols are specified, the relation name is used, e.g. the Employee shall use an ?Employee symbol for each instance found. If the action is give, then the expression is immediately returned from the which call on the first match. If the action is either list, then a list containing each expression is returned or an empty list is returned if nothing matched. If the action is tally, then the number of matched premises is returned, or zero if no matches.

##### Example
```

(relation Car :Make :Model :Year)

(which Car :Make Toyota)

(which (which Car :Make Toyota) each ?thought

[Dealer :Has (:Make ?tuple)]

deem true)

> (relation Pairs :A :B)(new Pairs :A 1 :B 2)(new Pairs :A 3 :B 4)

.: Pairs Pairs_1 Pairs_2

> (which Pairs :B 2)

.: Iterator-1

> (relation Fact :All :Are)

.: Fact

> (new Fact :All people :Are mortal) (new Fact :All philosophers :Are people)

.: Fact_1 Fact_2

> (function ExcludedMiddle {}

(with [Fact :All as ?s :Are as ?m]

[Fact :All ?m :Are as ?p]

(no [Fact :All ?s :Are ?p])

list (premise (knew A :All ?s :Are ?p))))

.: ExcludedMiddle

> (ExcludedMiddle)

.: {[Fact ^ Fact_3 :All philosophers :Are mortal]}

> (which Fact ^ as ?a :Are mortal)

.: Iterator-2

> (with Fact :Are mortal)

.: {[Fact ^ Fact_1 :All people :Are mortal]

[Fact ^ Fact_3 :All philosophers :Are mortal]}

> (relation Fruit :Name :Size :Shape :Color)

.: Fruit

> (step ?i from 1 to (random 1 to 1000)

(new Fruit :Size (pick {small medium large})

:Shape (pick {ellipsoid spheroid bananoid})

:Color (pick {red orange yellow green})))

.: Fruit_387

> (with [Fruit ^ as ?f :Name as ?name :Size as ?size :Shape spheroid :Color orange]

(null-p ?name)

(in {small medium} ?size)

deem Orange else Other)

.: Orange

> (with

[Fruit as ?f]

(let ?f :Size ?size :Shape ?shape :Color ?color)

(in {small medium} ?size)

(= ?shape bananoid)

(= ?color yellow)

deem true else false)

.: true

> (relation Customer :CustomerId :FirstName :LastName)

.: Employee

> (relation Order :OrderId :CustomerId :Quantity :Product)

.: Order

> (step ?i from 1 to (random 1 to 10)

(let ?c (new Customer))

(step ?j from 1 to (random 0 to 10)

(new Order :CustomerId ?c)))

.: Order_347

> (with [Customer as ?c]

[(with Order as ?o (= (:CustomerId ?o) (:CustomerId ?c))) each ?orders]

tally)

.: 2

> (with

[Customer as ?c :CustomerId ?x]

[(with Order as :CustomerId ?y (= ?x ?y)) as ?orders]

scan 30

limit 5

list

[R :Customer ?c :Orders (# ?orders)])

.: {[R :Customer Customer_1 :Orders 3]

[R :Customer Customer_2 :Orders 7]

[R :Customer Customer_4 :Orders 4]

[R :Customer Customer_3 :Orders 9]}

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

.: Student_12

> (which Student ^ ?student

(let ?exam 3 ?score 90)

(> (@ (:Tests ?student) ?exam) ?score)

list {:Name (:Last ?student) :Score (@ (:Tests ?student) ?exam)})

.: {{:Name Bates :Score 98}{:Name Luria :Score 97}{:Name Parker :Score 94}

{:Name Castaneda :Score 95}{:Name Rose :Score 98}{:Name Pushkin :Score 100}}

> (which Student as ?s

group ?s

by :Year into ?g

list ?g

sort 1 <)

.: {{1 [Student :First Yong :Last Lee :No 17 :Year 1 :Tests {78 79 90 95}]

[Student :First Patrice :Last Jones :No 13 :Year 1 :Tests {99 95 94 72}]

[Student :First Alex :Last Sartre :No 22 :Year 1 :Tests {85 97 86 95}]}

{2 [Student :First John :Last Jones :No 20 :Year 2 :Tests {100 56 87 86}]

[Student :First Phillipa :Last Sanchez :No 18 :Year 2 :Tests {85 87 89 97}]

[Student :First Charlie :Last Rose :No 11 :Year 2 :Tests {97 98 98 97}]}

{3 [Student :First Lexie :Last Bates :No 16 :Year 3 :Tests {67 68 98 87}]

[Student :First Jenny :Last Luria :No 15] :Year 3 :Tests {99 98 97 99}]

[Student :First Boris :Last Pushkin :No 19 :Year 3 :Tests {100 85 100 100}]}

{4 [Student :First Paul :Last Gates :No 14 :Year 4 :Tests {86 89 88 89})

[Student :First Jesus :Last Castaneda :No 12 :Year 4 :Tests {98 89 95 94}]

[Student :First Elizabeth :Last Wilson :No 021 :Year 4 :Tests {100 100 85 95})}]}}}

> (which Student as ?s :Id ?id

group ?id

by (given {?s} (@ ($ (:Last ?s)) 1)) into ?g

list ?g)

.: {{"B" 16}{"C" 12}{"G" 14}{"P" 19}{"R" 11}{"L" 17 15}{"W" 21}{"S" 18 22}{"J" 20 13}}

> (which Student as ?s :Tests ?t

(let ?percentile (/ (avg ?t) 10))

group ($ (:First ?s) (:Last ?s))

by ?percentile into ?g

list ?g

sort 1 < )

.: {{8 "John Jones" "Lexie Bates" "Yong Lee" "Paul Gates" "Phillipa Sanchez"}

{9 "Jenny Luria" "Patrice Jones" "Jesus Castaneda" "Charlie Rose" "Boris Pushkin" "Alex Sartre" "Elizabeth Wilson"}}

> (with Student as ?s

group [R :FirstLetter (@ ($ (:Last ?s)) 1)

:Score (:Score ?s)]

by (given {?s} (> (@ (:Tests ?s) 1) 85)])

into ?g

list ?g

sort (given {?x} (:FirstLetter ?x)) <)

.: {{"C" [R :FirstLetter "C" :Score 98]}{"J" [R :FirstLetter "J" :Score 100]

[R :FirstLetter "J" :Score 99]}{"L" [R :FirstLetter "L" :Score 99]}

{"G" [R :FirstLetter "G" :Score 86]}{"P" [R :FirstLetter "P" :Score 100]}

{"R" [R :FirstLetter "R" :Score 97]}{"W" [R :FirstLetter "W" :Score 100]}}

```

##### Related

each, knew, known, new, relation, such, suppose, unless, using, with

## while

Loops expressions while a condition is true.

##### Syntax
```

(while condition expression … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| condition | truth | 1   | A truth expression |
| expression | expression | 0+  | A call to be evaluated. |

##### Results

| Taxon | Description |
| --- | --- |
| value | The last value of the last iteration |

##### Remarks

None

##### Example
```

> (modular ?i 0)

.: true

> (while (< ?i 1000)

(--> ++ ?i)) ; assign ?i to the increment of ?i.

.: 1000

```

##### Related

for, iterate, loop, repeat, step, until

## whitespace-p

True if the first position of a string is whitespace.

##### Syntax
```

(whitespace-p value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 1   | A value. |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the value is a string and the first position is whitespace. |

##### Remarks

Whitespace is a space, newline, or tab.

##### Example
```

> (whitespace-p {a b c})

.: false

> (whitespace-p "a b c")  


.: false

> (whitespace-p " a b c")

.: true

> (whitespace-p 450)

.: false

> (whitespace-p " foo")

.: true

> (whitespace-p "hello world")

.: false

```

##### Related

capitalized-p, letter-p, lowercase-p, uppercase-p

## with

Matches patterns against the knowledge base.

##### Syntax
```

(with premises option … action )

premises ::= premise

premises ::= premise premises

premises ::= premise premises

premises ::= premise restriction … premises

restriction ::= (predicate value …)

premise ::= [category descriptor … ]

category ::= type

category ::= list

descriptor ::= slot binding

descriptor ::= slot condition

binding ::= as symbol

binding ::= each symbol

condition ::= slot \= value

condition ::= slot /= value

condition ::= slot is unary-predicate

condition ::= slot not unary-predicate

condition ::= slot binary-predicate value

condition ::= slot n-ary-predicate value-list

condition ::= (predicate value …)

option ::= scan number

option ::= limit number

option ::= group slot … by slot … into symbol

option ::= merge value …

option ::= sort ordering …

action ::= deem value1 else value2

action ::= do expression …

action ::= give expression

action ::= list value …

action ::= tally

action ::= yield expression

ordering ::= term comparator

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| clauses / premises | expression | 1+  | Either one or more clauses, or, one or more premises |
| option | expression | 0-2 | Either scan, limit, group, merge, sort, or any combination. |
| action | literal | 0-1 | Either deem, do, give, list, tally, yield. |
| expression | expression | 0+  | An expression |

##### Results

| Taxon | Description |
| --- | --- |
| expression | if the action is deem, then either the success or failure value is returned; if the action is do then the last expression value on the last iteration or nil; If the action is list, then a list of premises or an empty list; if the action is tally, then the number of matches or zero, if the action is give, then the expression is returned. |

##### Remarks

Note that a predicate is a truth function, scan tells the number of matches to attempt (default is infinity), and limit tells how many results to return (default is infinity). If the action is deem, then the subsequent value is returned if the final descriptor is matched, otherwise the else value is returned. If the action is do, then for each match the expressions are run, and for the last match, the last value of the last expression is returned, or nil is returned if all descriptors were false or had no matches. If the action is give, then the expression is immediately returned from the with call on the first match, akin to return from with. If the action is yield, then the expression is immediately returned from the with call, but may be resumed with a next function call. When all matches are completed, the done function is implicitly called to terminate the generator. If the action is group, followed by a list of slots and values from which the group is picked, then the literal by and a set of slots and values that determines the grouping inclusion , and finally the literal into followed by a symbol to which the group shall be bound on each iteration. If the action is either list (or merge), then a (merged) list is returned or an empty list if nothing matched. If the action is sort then the list of slots and comparators should follow. (Note that list is required if the sort action is selected.) If the action is tally, then the number of matched premises is returned, or zero if no matches.

##### Example
```

> (relation Fact :All :Are)

.: Fact

> (new Fact :All people :Are mortal) (new Fact :All philosophers :Are people)

.: Fact_1 Fact_2

> (function ExcludedMiddle {}

(with [Fact :All as ?s :Are as ?m]

[Fact :All = ?m :Are as ?p]

(no [Fact :All = ?s :Are = ?p])

list (premise (knew A :All ?s :Are ?p))))

.: ExcludedMiddle

> (ExcludedMiddle)

.: {[Fact ^ Fact_3 :All philosophers :Are mortal]}

> (which Fact ^ as ?a :Are = mortal list ?a)

.: {Fact_1 Fact_3}

> (which Fact :Are mortal)

.: {[Fact ^ Fact_1 :All people :Are mortal]

[Fact ^ Fact_3 :All philosophers :Are mortal]}

> (relation Fruit :Name :Size :Shape :Color)

.: Fruit

> (step ?i from 1 to (random 1 to 1000)

(new Fruit :Size (pick {small medium large})

:Shape (pick {ellipsoid spheroid bananoid})

:Color (pick {red orange yellow green})))

.: Fruit_387

> (with [Fruit ^ as ?f :Name as ?name :Size as ?size :Shape = spheroid

:Color = orange]

(null-p ?name)

(in {small medium} ?size)

deem Orange else Other)

.: Orange

> (with

[Fruit as ?f]

(let ?f :Size ?size :Shape ?shape :Color ?color)

(in {small medium} ?size)

(= ?shape bananoid)

(= ?color yellow)

deem true else false)

.: true

> (relation Customer :CustomerId :FirstName :LastName)

.: Employee

> (relation Order :OrderId :CustomerId :Quantity :Product)

.: Order

> (step ?i from 1 to (random 1 to 10)

(let ?c (new Customer))

(step ?j from 1 to (random 0 to 10)

(new Order :CustomerId ?c)))

.: Order_347

> (with [Customer as ?c]

[(which Order as ?o (= (:CustomerId ?o) (:CustomerId ?c))) each ?orders]

tally)

.: 2

> (with

[Customer as ?c :CustomerId ?x]

[(with Order :CustomerId = ?x) as ?orders]

scan 30

limit 5

list

[R :Customer ?c :Orders (# ?orders)])

.: {[R :Customer Customer_1 :Orders 3]

[R :Customer Customer_2 :Orders 7]

[R :Customer Customer_4 :Orders 4]

[R :Customer Customer_3 :Orders 9]}

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

.: Student_12

> (with Student ^ ?student

(let ?exam 3 ?score 90)

(> (@ (:Tests ?student) ?exam) ?score)

list {:Name (:Last ?student) :Score (@ (:Tests ?student) ?exam)})

.: {{:Name Bates :Score 98}{:Name Luria :Score 97}{:Name Parker :Score 94}

{:Name Castaneda :Score 95}{:Name Rose :Score 98}{:Name Pushkin :Score 100}}

> (with [Student as ?s]

group ?s

by :Year into ?g

list ?g

sort 1 <)

.: {{1 [Student :First Yong :Last Lee :No 17 :Year 1 :Tests {78 79 90 95}]

[Student :First Patrice :Last Jones :No 13 :Year 1 :Tests {99 95 94 72}]

[Student :First Alex :Last Sartre :No 22 :Year 1 :Tests {85 97 86 95}]}

{2 [Student :First John :Last Jones :No 20 :Year 2 :Tests {100 56 87 86}]

[Student :First Phillipa :Last Sanchez :No 18 :Year 2 :Tests {85 87 89 97}]

[Student :First Charlie :Last Rose :No 11 :Year 2 :Tests {97 98 98 97}]}

{3 [Student :First Lexie :Last Bates :No 16 :Year 3 :Tests {67 68 98 87}]

[Student :First Jenny :Last Luria :No 15] :Year 3 :Tests {99 98 97 99}]

[Student :First Boris :Last Pushkin :No 19 :Year 3 :Tests {100 85 100 100}]}

{4 [Student :First Paul :Last Gates :No 14 :Year 4 :Tests {86 89 88 89})

[Student :First Jesus :Last Castaneda :No 12 :Year 4 :Tests {98 89 95 94}]

[Student :First Elizabeth :Last Wilson :No 021 :Year 4 :Tests {100 100 85 95})}]}}}

> (which Student as ?s :Id as ?id

group ?id

by (given {?s} (@ ($ (:Last ?s)) 1)) into ?g

list ?g)

.: {{"B" 16}{"C" 12}{"G" 14}{"P" 19}{"R" 11}{"L" 17 15}{"W" 21}{"S" 18 22}{"J" 20 13}}

> (with [Student as ?s :Tests as ?t]

(let ?percentile (/ (avg ?t) 10))

group ($ (:First ?s) (:Last ?s))

by ?percentile into ?g

list ?g

sort 1 < )

.: {{8 "John Jones" "Lexie Bates" "Yong Lee" "Paul Gates" "Phillipa Sanchez"}

{9 "Jenny Luria" "Patrice Jones" "Jesus Castaneda" "Charlie Rose" "Boris Pushkin" "Alex Sartre" "Elizabeth Wilson"}}

> (with [Student as ?s]

group [R :FirstLetter (@ ($ (:Last ?s)) 1)

:Score (:Score ?s)]

by (given {?s} (> (@ (:Tests ?s) 1) 85)])

into ?g

list ?g

sort (given {?x} (:FirstLetter ?x)) <)

.: {{"C" [R :FirstLetter "C" :Score 98]}{"J" [R :FirstLetter "J" :Score 100]

[R :FirstLetter "J" :Score 99]}{"L" [R :FirstLetter "L" :Score 99]}

{"G" [R :FirstLetter "G" :Score 86]}{"P" [R :FirstLetter "P" :Score 100]}

{"R" [R :FirstLetter "R" :Score 97]}{"W" [R :FirstLetter "W" :Score 100]}}

```

##### Related

assert, assume, each, retract, such, which

## within

True if a position is inside a sequence.

##### Syntax
```

(within sequence position )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| sequence | sequence | 1   | A sequence. |
| position | variant | 1+  | A number or coordinate (i.e. a list of numbers). |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the position is in the sequence, false otherwise. |

##### Remarks

None.

##### Example
```

> (within "not empty" 5)

.: true

> (within {not empty} 1)

.: true

> (within "" 1)

.: false

> (within {} 5)

.: false

> (within {{a b}{c d}{e f}} {3 2})

.: true

> (within {{a b}{c d}{e f}} {7 4})

.: false

```

##### Related

@ element, beyond, length, empty, more

## wrap

Prohibits modifications to a module.

##### Syntax
```

(wrap module)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| module | module | 1   | A module |

##### Results

| Taxon | Description |
| --- | --- |
| literal | The literal wrapped |

##### Remarks

None

##### Example
```

> (module Math

(function sum ?args (apply + ?args)))

.: Math

> (wrap Math)

.: wrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.: [Failure :Name Permission :Text "Can't modify a wrapped module"]

> (unwrap Math)

.: unwrapped

> (extend Math

(function prod ?args (apply \* ?args)))

.: Math

```

##### Related

unwrap

## write

Writes values to a writeable resource.

##### Syntax
```

(write file value )

```
##### Module

IO

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| file | resource | 1   | A file or pipe. |
| value | variant | 1   | A value to write |
| bits | integer | 0-1 | The size of the byte or character in bits. Either 7, 8, 16,o,r 32. (Default is 8.) |

##### Results

| Taxon | Description |
| --- | --- |
| resource | Returns the resource |

##### Remarks

None.

##### Example
```

> (let ?file (file name "test.txt"))

.: true

> (read ?file)

.: "Hello"

> (seek ?file 1)

.: File-1

> (write ?file ($ Goodbye my friends.))

.: File-1

> ­(close ?file)

.: closed

```

##### Related

bytes, close, file, read, reposition, write

## xnor

Logical equivalance.

##### Syntax
```

(xnor truth truth)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 2   | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the argument values are equal |

##### Remarks

Implements logical equivalence as the result is true when both arguments are the same.

##### Example
```

> (xnor true false)

.: false

> (xnor false true)

.: false

> (xnor false false)

.: true

> (xnor true true)

.: true

```

##### Related

and, nand, void, nor, not, or, is, xor

## xor

Logical exclusive disjunction.

##### Syntax
```

(xor truth truth)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| truth | truth | 2   | A truth value |

##### Results

| Taxon | Description |
| --- | --- |
| truth | True if the argument values are not equal |

##### Remarks

None.

##### Example
```

> (xor true false)

.: true

> (xor false true)

.: true

> (xor false false)

.: false

> (xor true true)

.: false

```

##### Related

and, nand, void, nor, not, or, is, xnor

## yield

Returns a result from a series generator.

##### Syntax
```

(yield value)

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| value | variant | 0-1 | Any value to be returned. Default is nil. |

##### Results

| Taxon | Description |
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

.: myGenerator

> (collect ?x in (myGenerator true) ?x)

.: {1 2}

> (collect ?x in (myGenerator false) ?x)

.: {1 2 3 4}

```

##### Related

done, generator-p, series

## zap

Updates associations and sequences with nil values.

##### Syntax
```

(zap container place … )

```
##### Module

KB

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| container | variant | 1   | A sequence or assortment |
| place | variant | 0+  | A slot, key, or position. |

##### Results

| Taxon | Description |
| --- | --- |
| container | Returns the modified container. |

##### Remarks

If no places are provided, then all keys, positions, or slots are set to nil.

##### Example
```

> (relation A :X 1 :Y 2 :Z 3)

.: a

> (get (new A))

.: [A ^ A_1 :X 1 :Y 2 :Z 3]

> (zap A_1 :Y)

.: A_1

> (get A_1)

.: [A ^ A_1 :X 1 :Y nil :Z 3]

> (zap A_1)

.: A_1

> (get A_1)

.: [A ^ A_1 :X nil :Y nil :Z nil]

```

##### Related

let, new, nix

## zero-p

True if a number is zero.

##### Syntax
```

(zero-p number)

```
##### Module

Math

##### Parameters

| Name | Taxon | Qty | Description |
| --- | --- | --- | --- |
| number | number | 1   | A number |

##### Results

| Taxon | Description |
| --- | --- |
| truth | Returns true if the number is zero. |

##### Remarks

None.

##### Example
```

> (zero-p 100)

.: false

> (zero-p 0)

.: true

> (zero-p -0)

.: true

> (zero-p -30)

: false

```

##### Related

even-p, negative-p, odd-p, positive-p

# Appendix

## thought Cell

A thought cell is an evaluator for expressions. Given one or more expressions, it shall evaluate each expression and return a corresponding result which may even be a failure premise.

A cell has the following attributes

| # | Attribute | Type | Description |
| --- | --- | --- | --- |
| 1   | Reader |     | The input reader |
| 2   | Writer |     | The output writer |
| 3   | Evaluator |     | Procedure used to evaluate expressions. |
| 4   | Self | SbTask | The current task |
| 5   | Me  | SbMachine | The current machine |
| 6   | KB  | SbKnowledge | The associated knowledge base |
| 7   | Current | SbActivation | The expression being evaluated |
| 8   | Stack | SbStack |     |
| 9   | State | SbState |     |
| 10  | Globals | SbEnvironment | Link to the global environment. |
| 11  | Scope | SbEnvironment | The current environment |
| 12  | Status | CsStatus | One of Pending, Started, Successs, Failure. |
| 13  | Result | SbVariant | The Last result |
| 14  | Anomaly | SbFailure | The current machine |
| 15  | Use | SbModule | The current module |

### Call Graph Node

A stack frame

| # | Attribute | Type | Description |
| --- | --- | --- | --- |
| 1   | Prior | SbStackFrame | The prior frome. |
| 2   | Scope | SbEnvironment | Variable environment |
| 3   | Expression | SbVariant | Expression to evaluate |
| 4   | Result | SbVariant | Result of evaluation |
| 5   | Return | SbLocation | Where to return: function body or arg list |
| 6   | Next | SbStackFrame | The next frame |
| 7   | Depth | long | The current depth of the frame. |
| 8   |     |     |     |

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
