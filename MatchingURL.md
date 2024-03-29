# Regex: Tutorial on Matching a URL

Regular expressions, commonly referred to as Regex, constitute a highly valuable and potent tool for extracting information from textual sources, encompassing code, log files, spreadsheets, and documents. Among the myriad applications, a prevalent use case involves the validation and matching of Uniform Resource Locators (URLs).

This tutorial will provide comprehensive guidance on employing Regex to ascertain the adherence of a given string to the standardized URL format.

## Summary

Within this document, I will elucidate the utilization of a regular expression designed to validate URLs, guaranteeing adherence to a specific pattern:

```regex
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

While the sequence of characters may appear cryptic at first glance, it represents a structured assembly of regular expression components, each of which will be thoroughly explored in the subsequent discussion.

Let us delve into the intricacies of each Regex Component, elucidating the process of constructing a robust URL matching pattern using the content provided in this document.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
The characters ^ and $ function as anchors, employed to match the start and end of a string, respectively.

### Quantifiers
Quantifiers permit the specification of how frequently a particular regex string should match. Two variants exist: lazy and greedy. By default, regex matching is eager, seeking to match as much as possible. This behavior may not always be desired. Lazy quantifiers restrict the matched content. Quantifiers include:

- `+` matches the pattern one or more times.
- `*` matches the pattern zero or more times.
- `?` matches the pattern zero or one time.
- `{}` curly brackets establish limits for a match:
    - `{n}` matches the pattern exactly n times.
    - `{n,}` matches the pattern at least n times.
    - `{n,x}` matches the pattern from a minimum of n times to a maximum of x times.

Breakdown of the provided regex:

- `(https?:\/\/)?` is an optional group, allowing for either "http://" or "https://".
- `([\da-z\.-]+)` captures the domain name, permitting alphanumeric characters, dots, or hyphens.
- `\.([a-z\.]{2,6})` matches the top-level domain (TLD), consisting of two to six lowercase letters or dots.
- `([\/\w \.-]*)*` captures optional path segments, query parameters, or fragments, allowing any character from the set [/, \w (alphanumeric), space, dot, hyphen].
- `\/?` matches an optional trailing slash.

### OR Operator
The OR operator, denoted by the vertical bar `|`, specifies alternatives within a pattern, allowing the matching of one pattern or another.

### Character Classes
Character classes(escape) in regex allow the literal matching of specific characters, bypassing their special meanings. Common examples include:

  - `\.` (Escapes the dot (.) character) - it matches a literal dot instead of its special meaning, which is to match any character (except newline) in regular expressions.

  - `\/` (Escapes the forward slash (/) character) - it matches a literal forward slash instead of its special meaning, which is often used as a delimiter in regular expressions.

  - `\\` (Escapes the backslash (\) character) -  it matches a literal backslash instead of its special meaning as an escape character.

  - `\+, \-, \*, etc.` (Escapes special characters like +, -, *, etc.) - it is to match them literally instead of their special meanings in regular expressions.

  - `\d, \w, \s` These are shorthand character classes that match digits (\d), word characters (\w), and whitespace characters (\s), respectively. They are used as escapes to represent these predefined character classes.

Using character classes(escape) enables the precise matching of characters without interpreting their special meanings within the regex syntax.

### Flags
Flags, optional parameters appended to the regex, modify pattern matching behavior, altering how the pattern is interpreted or applied.

### Grouping and Capturing

Grouping and Capturing in regular expressions (denoted by parentheses) amalgamate multiple characters or subpatterns, treating them as a singular unit. The grouped regex looks like:
```regex
(https?:\/\/) ([\da-z\.-]+) ([a-z\.]{2,6}) ([\/\w \.-]*)
```

### Bracket Expressions

Bracket expressions, or character classes, enable the definition of a set or range of characters for matching against a single character position. They are denoted by square brackets `[ ]`. Examples include:

- `[abc]`: Matches either "a", "b", or "c".
- `[0-9]`: Matches any digit from 0 to 9.
- `[a-z]`: Matches any lowercase letter from "a" to "z".
- `[A-Z]`: Matches any uppercase letter from "A" to "Z".
- `[0-9a-fA-F]`: Matches any hexadecimal digit.

A few special characters have special meanings within brackets include:

- Hyphen (-): Specifies a character range. For example, `[a-z]` matches any lowercase letter.
- Caret (^): When used as the first character inside the brackets, it negates the character set. For example, `[^0-9]` matches any character that is not a digit.
- Backslash (\): Escapes a special character inside the bracket expression.

The grouped regex for the provided example:
```regex 
  [\da-z\.-] [a-z\.] {2,6} [\/\w \.-]
```

### Greedy and Lazy Match
As expected, the definition of a greedy match, is a search that will try to find the longest possible string, whereas a lazy match is search will find the smallest possible string. 
Greedy quantifiers are:
- + = one or more revised gist
- * = Zero or more
- {2,4} = Two to four times as greedy
Lazy quantifier:
- ?
This expression : 
```(https?:\/\/)?``` uses the lazy match of ? and is looking http OR https, ```[a-zA-Z0-9()]{1,6}``` is looking for a-z, A-Z, 0-9; one to six times as greedy.

### Boundaries
Boundaries are similar to an anchor and uses the expression \b for word boundaries and \B for non-word boundaries. They are a zero-length match that marks the beginning and end of an alphanumerical sequence and will make it easier to find whole words. The beginning of this expression ```\b([-a-zA-Z0-9()@:%_\+.~#?&//=]*)``` is searching for a whole word or digit.

### Back-references
Backreferences are filters used to match the same text previously matched by a capturing group. An example would be when you desire to search for a repeated word, the first match could use a pattern that extracts a signle word, the second would be a back reference that referes to the captured group. The above example does not include any backreferences.

### Look-ahead and Look-behind
look behind `?<=` means to look after a specified sentence. If an expression would were to have `(?<=The Cat is).*` in a text containing `The Cat is Fuzzy`, the results will highlight the word `Fuzzy` since it is 'behind' the specified string. The opposite use can be included with the look-ahead, which will look for specified characters in front of a selected string. 

## Author

Lufranc Kousse Akodjo is a current student at the Arizona State University Full Stack Develoer Bootcamp.
Github: https://github.com/lufranckousse