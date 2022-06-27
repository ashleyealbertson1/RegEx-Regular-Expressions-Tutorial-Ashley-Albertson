# An Overview of Regular Expressions (RegEx)

Regular expressions are essential tools in advanced text processing.  They are special text strings that allow you to not only search literal text, but to also create search patterns with specific rules to find data in a text by matching character combinations in strings. Ordinary text search can be only used to find text strings that are fixed, whereas RegEx can be used to significantly narrow down searches to find much more specific text in a data set.  To illustrate the difference between ordinary text search and regular expressions, let's use an example of a given data set containing people's personal information. Using basic text search, you would only be able to narrow down the search to find a specific phone number. If you were to conduct your search with regular expressions, you would be able to easily find much more detailed information such as: only the phone numbers that are valid, only phone numbers from a specific area code, or only phone numbers starting or ending with certain digits. 

## Summary

Regular expressions, sometimes referred to as rational expressions, can be extremely complex, but they are very flexible and powerful and can be used to perform comparisons that cannot be done using ordinary text search.  They can be strings or objects and allow you to create search modifiers and patterns with specific rules to find data in a text.  These patterns can be composed of simple characters, such as /xyz/, or a combination of simple and special characters, such as /x*yz*c/ or /Section (\x+)\.\x*/.  RegEx can be used to perform all types of text operations by using a variety of string methods such as find(), search(), test(), split(), replace() among many others. 

Components of regular expressions can be found below in the table of contents. Scroll down to read about them or click on one to be brought to that specific section of the document.


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components


### Anchors

Anchors are an odd, unique component of regular expressions because they do not match any characters. Rather, they use positioning to limit searches by asserting the boundaries of the matching process. Anchors are used to match a particular string by specifying where matches are allowed to begin and where they must end: for example, the start/end of the string, the start/end of a line, within/not within a word boundary. 

Types of anchors are as follow:


- ^ (caret): This serves as both a string anchor and line anchor. It requires the match to occur at the beginning of the string or line. For instance, "^The" matches any string that starts with "The".
- (dollar): This serves as both a string anchor and line anchor. It requires the match to occur before the linebreak /n at the end of the string or line. For example, "happiness$" matches any string that ends with "happiness".
- \A (beginning of string): This is a string only anchor. It requires the match to occur at the beginning of the string only.
- \z (very end of string): This is a string only anchor. It requires the match to occur at the end of the string only.  
- \Z (end of string / before line break): This is a string only anchor. It requires the match to occur at the end of the string, or before the final line break at the end of the string. 
- \G (beginning of string / end of previous match): The match is required to start at the position where the previous match ended, or if there was no previous match, at the position in the string where matching began.
- \b (word boundary): The match is required to occur on a word boundary. 
- \B (non-word boundary): The match is required to not occur on a word boundary.

You can also combine anchors, for example, "^abc$" matches a string that starts and ends with "abc" - effectively an exact match comparison.


### Quantifiers

Quantifiers dictate the number of instances a character, character class or sub-expression must be present in order for a match to be found.

Most common types of quantifiers are as follow:

- {n} (exact count): This is the simplest quantifier. The match is required to occur exactly n times in order for a match to be found. ("ab{2}" would require the letter a to be followed by 2 b's in order for a match to be found: "abb").
- {n,}: The match is required to occur at least n times in order for a match to be found.
("ab{2,}" would require the letter a to be followed by at least 2 b's in order for a match to be found: "abb", "abbbbbb", etc.).
- {n,m} (the range): The match is required to occur at least n times, and no more than m times in order for a match to be found.
("ab{2,5}" would require the letter a to be followed by at least 2 b's and no more than 5 b's in order for a match to be found: "abb" - "abbbbb") 
- ?,+,* (shorthands): The match is required to occur: (?) zero or one time, (+) one or more times, (*) zero or more times in order for a match to be found.



### Grouping Constructs and Capturing

Regular expressions are made up of a sequence of sub-expressions.  RegEx grouping constructs allow you to evaluate specific information in a specific order by delineating the sub-expressions of regular expressions, thereby capturing substrings of input strings. Grouping constructs serve a similar purpose to parenthetical / order of operation statements in a math equation.



### Bracket Expressions 

Bracket expressions consist of characters and/or character classes enclosed in brackets []. They are useful for matching characters in a list, whether single characters or a range of characters. For example, expression [ abc ] matches a, b, or c and expression [ a-z ] matches a through z. You can use the caret ^ to negate the characters in the brackets. For example, expression [ ^abc ]  matches any character except a, b, or c.

### Character Classes

Character classes, also referred to as character sets, are always found in bracket expressions. They identify the characters that will match a single character from an input string. For example, let's say you want to search the text for the name "gray" or "grey" because you're not sure how it is spelled in the text as both are acceptable spellings. You would want it to match an 'a' or an 'e', so you would use [ae]. The expression gr[ ae ]y would not match "graay" or "graey", only "gray" or "grey".  Note, the order of the characters inside a character class does not matter; the results are identicle regardless of the order in which the characters appear inside the brackets. You can also use hyphens to specify range as well as numerical values inside a character class. 

Common character class examples include the following: 

- \d (match a single digit or a character from 0 to 9).
- \s (match a single whitespace symbol such as space, \t tab , \n newline).
- \w (match a single word character: all numbers and letters (regardless of case) including Latin alphabets, digits, and _ underscore).
- \D (matches any character except a digit e.g., a symbol or letter).
- \S (matches any character except a whitespace e.g., a digit, special symbol, or letter).
- \W (matches any character except a word character e.g., non-Latin letter, special symbol, or space).
- (.) (special character class that matches any character except \n newline


### The OR Operator

The "OR" operator, denoted by a vertical bar '|' provides search alternatives (find a string that matches this OR this OR this). For example, "hi|hello" matches a string with both "hi" and "hello" in it.

### Flags

Regular expressions may have flags that affect the default searching behavior. It makes a RegEx search in a different way.

There are only 6 of these in JavaScript:

- i (makes the search case-insensitive: no difference between A and a). 
        
        var str = "Hello world!";
        var regex = /hello/i;

        var newStr = str.replace(regex, '(Hello)');

- g (makes the search global look for all matches, without it – only the first match is returned).
        var str = "50 is the half of 50 x 2 that is 80.";
        var newStr = str.replace(/50/g, "40");

        console.log(newStr) "40 is the half of 40 x 2 that is 80."

- m (multi-line mode- makes the boundary characters ^ and $ match the beginning and end of every single line instead of the beginning and end of the whole string).
- s (changes the search to enable “dotall” mode, which allows a dot . to match \n newline).
- u (enables full Unicode support. The flag enables correct processing of surrogate pairs).
- y (enables “sticky” mode- makes the expression start its searching from the index indicated in its lastIndex property / the exact position in the text).



### Character Escapes

The backslash ( \ ) in a regular expression is known as the escape code and precedes a literal character in order to restore it to its orginal, literal meaning. Escape codes are required in order to match with occurance indicators--- *, +, ? and position anchors---  ^, $.

## Author

Ashley has lived in Texas her whole life. She attended the University of Texas at Tyler where she earned a Bachelor's Degree in Marketing and graduated Summa Cum Laude. Ashley is currently enrolled in the Full Stack Web Development program at Southern Methodist University (SMU) and is looking forward to her graduation from the program as a professional software enginneer in August 2022. 

Since college graduation, Ashley's professional career of nearly a decade has been spent in results-driven sales and marketing positions.  She spent her first 2 years after graduation in traditional, business-to-business sales as an outside sales rep before switching gears to digital marketing and online sales management. 

Ashley has spent the last 6 1/2 years of her professional life being in charge of developing, implementing & managing digital marketing campaigns and heading up online sales efforts in small multi-million dollar companies and global coporations for both Business-to-Business (B2B) and Business-to-Customer (B2C) channels.  While holding the position of eCommerce Marketing Manager in both the small business sector and at the global, corporate level, and across very diverse industries, Ashley has proven she can apply her skills, personability, and hard-work ethic to achieve desired results no matter the size of the company or type of industry.

While Ashley has experienced a fulfilling and rewarding career thus far, managing online sales and marketing campaigns, she is very excited about her upcoming professional status as a Full Stack Web Developer and is very much looking forward to her new career path in programming and software engineering. Ashley cannot wait to bring her programming knowledge to contribute to the new workplace and continue her learning through professional programming work. 

### GitHub: 

https://github.com/ashleyealbertson1

### LinkedIn: 

(currently creating this and will add link when complete)


### Sources 

https://evermap.com/RegularExpressions.asp#:~:text=Regular%20expressions%20(regex%20for%20short,tool%20in%20advanced%20text%20processing.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions

https://analytics.webtrends.help/docs/regular-expression-components

https://www.cs.wcupa.edu/rkline/index/regular-expressions.html

https://www.rexegg.com/regex-anchors.html

https://launchschool.com/books/regex/read/anchors

https://docs.microsoft.com/en-us/dotnet/standard/base-types/anchors-in-regular-expressions

https://www.javascripttutorial.net/regular-expression-quantifiers/

https://docs.trendmicro.com/all/ent/imsva/v8.5/en-us/imsva8.5_olh/usg_kw_exp_regexp_brkt.html

https://www.codeguage.com/courses/regexp/flags

https://www.jmp.com/support/help/zh/15.2/index.shtml#page/jmp/escaped-characters-in-regular-expressions.shtml
