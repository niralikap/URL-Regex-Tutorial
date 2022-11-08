# Regex (Matching a URL)

Introductory paragragh

URL regular expressions can be used to verify if a string has a valid URL format as well as to extract a URL from a string.

There are two types of URL Regex:

1. URL regex that starts with HTTP or HTTPS

HTTP and HTTPS URLs that start with protocol can be validated using the following regular expression:

Example: 
`/^https?:\/\/(?:www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&\/=]*)$/`

2. URL regex that does not start with HTTP or HTTPS

The regular expression to validate URL without protocol is very similar:

Example:
`/^[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&//=]*)$/`



## Summary

The regex that I will be describing is as follows:

Matching a URL: `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

Code snippet:

var expression = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
var regex = new RegExp(expression);
var t = 'https://berkeley.edu/about';

if (t.match(regex)) {
  alert("Successful match");
} else {
  alert("No match");
}

Output:
String that matches:

`https://berkeley.edu/about`

String that doesn't match:

`http://google.com/some/file!.html` (contains an exclamation point)



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

While this expression may seem obscure upon initial inspection, let's see if we can break it down into its individual elements in order to understand how the sequence works. The individual elements are described below:


### Anchors

The two principal anchors in this regex expression are the `^` at the beginning and the `$` at the end which constitute an exact string match with the components included within the two anchors. 

The `^` anchor signifies a string that begins with the characters that follow it and an exact string match.
The `$` anchor signifies a string that ends with the characters that precede it. Just as with the `^` character, it can be preceded by an exact string or a range of possible matches.

By enclosing the regex between these two anchors, we are asking the search function to match exactly what is included between them (what it begins AND ends with).


### Quantifiers

Quantifiers set the limits of the string that your regex matches (or an individual section of the string). They frequently include the minimum and maximum number of characters that your regex is looking for. Quantifiers are also used to define the number of times a given expression may be identified. 

The quantifiers in the above expression are `?`,`*`, and `{}`.

The `?` makes a single instance of the character preceding the quantifier optional, whereas the `*` makes multiple instances of the characters preceding the quantifier optional.

- `(https?:\/\/)?`

The above first capturing group is all optional. It allows the URL to begin with `http://`, `https://`, or neither of them (the input begins with `www.`). The same applies for the `/` at the very end of the expression.

The `?` after the `s` allows URLs that have http or https. In order to make this entire group optional, a `?` is added to the end of it.


- `([\/\w \.-]*)*`

The `*` makes the above expression optional, but in this case it may be one or more instances that are optional. The expression is allowing for any number of filepath characters that may follow an initial specified domain. 

This section is for the optional files and directories. Inside the group, we want to match any number of forward slashes, letters, numbers, underscores, spaces, dots, or hyphens. Then we say that this group can be matched as many times as we want. This allows multiple directories to be matched along with a file at the end. I have used the star instead of the question mark because the star says zero or more, not zero or one. 

- `{2,6}`

Finally, the `{}` quantifier defines a range of possible instances where a match may be identified. In evaluating the Top level domain, the regular expression allows for the top level domain to consist of 2 to 6 characters.



### Grouping Constructs

The grouping in regex is done using parentheses `()`. If we examine the expression, we can see that there are a number of components separated by parentheses `()`. Parentheses are used in regex to create separate groups of interest. Within each of these groups, there is a regex that we may look at separately to see what is evaluated. These include:

- The initial https component: `(https?:\/\/)`

- The domain name (e.g. www.google, or pets): `([\da-z\.-]+)\.`

- The top level domain (.com, .gov, etc): `([a-z\.]{2,6})`

- The file path: `([\/\w \.-]*)*`



### Bracket Expressions

Bracket expressions include anything inside of a set of square brackets ([]). These patterns are known as bracket expressions, but they are also known as a positive character group, because they outline the characters we want to include. We can write these expressions to include all of the characters we want to match. The following are the bracket expressions: 

- `[\da-z\.-]`

The above expression matches for any digits (\d) OR any characters between a and z (`a-z`) OR any '.' (`\.`) OR any '-' (`-`).

- `[a-z\.]`

Same as the above excluding the digits.

- `[\/\w \.-]`

The above expression matches for any file path and it could include `.` or `-`.


### Character Classes

The main character classes to consider in the above expression include the `\d` character class which looks for any digit, and the `\w` character class that looks for any alphanumeric character.

Also, `.` matches any character except the newline character (`\n`).


### The OR Operator

The main OR operator used in the above regex is the `[]`. The expression will match for any characters or character classes included in the brackets. For example:

 - `[\da-z\.-]` expression matches for any digits (`\d`) OR any characters between a and z (`a-z`) OR any '.' (`\.`) OR any '-' (`-`).


### Flags

Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits for the regex. They include:

- `g` for global search
- `i` for case-insensitive search
- `m` for multi-line search

There are no flags in the above URL regex.


### Character Escapes

The backslash (`\`) in a regex escapes a character that otherwise would be interpreted literally. For example, adding a backslash before the open curly brace (`\{`) means that the regex should look for the open curly brace character instead of beginning to define a quantifier. 

All special characters, including the backslash (`\`), lose their special significance inside bracket expressions.

There are no character escapes in the above URL regex.



## Author

This regex tutorial was created by Nirali Kapadia. 

Github profile: `https://github.com/niralikap`
