## Python Regular Expression Tutorial

- Regular Expressions or Regex, are a sequence of characters to check whether a pattern exists in a given text(string) or not.
- used at server side to vliadate the format of email addresses or passwords during registration
- used for parsing text data file to find.
- `import re` brings in the regular expression lib

### Basic Patterns

- The match() function returns a match object if the text matches the pattern, otherwise it will return None.
`pattern r"Cookie"`
`sequence = Cookie`
`if re.match(pattern, sequnce):`
    `print("Match")`
`else: print("Not a match!")`
- The r at the start of the pattern Cookie is called a raw string literal. It changes how the string literal is interpreted. Not need in the above example but it's good practice and useful when using special characters like `\` escape sequences as it prevents these characters from being interpreted as such.


### Wild Card Chars: Special Characters

- The `.search()` you can scan through the given string/sequnce and look for the first location where the regular expression produces a match.
- The `group()` returns the string matched by the re.
`.` A period. Matches any single character except the newline char
`^` A caret. Matches the start of the string. Helpful when you want to make sure a doc/sentence starts with certain chars
`$` Matches the end of string. 
`[abc]` - Matches a or b or c.
`[a-zA-Z0-9]` - Matches any letter from (a to z) or (A to Z) or (0-9).
`\` - Backslash. Can be used in front of all the metacharacters to remove their special meaning. 
`\w` - Lowercase 'w'. Matches any single letter, digit, or underscore.
`\W` - Uppercase 'W'. Matches any sinlge char not part of \w (lowercase w).
`\s` - Matches a single whitespace char like: space, newline, tab, return.
`\S` - Matches any char not part of \s (lowercase s).
`d\` - Matches decimal digit 0-9.
`\D` - Matches any char that is not a decimal digit.
`\t` - Lowercase t. Matches tab.
`\n` - Lowercase n. Matches newline.
`\r` - Lowercase r. Matches return.
`\A` - Uppercase a. Matches only at the start of the string. Works across multiple lines as well.
`\Z` - Uppercase z. Matches only at the end of the string.

### Grouping in Regular Expressions

- parts of the re pattern bounded by parenthesis `()` are called groups. The parenthesis does not change what the expression matches, but rather form groups within the matched sequence.
- You can also use `<>` brackets instead to create name groups. This will make your code a bit more readable.


### Function provided by 're'

- `compile()` you can compute a regular expression pattern into a regular expression object. This can save time.
- The `match()` function checks for a match only at the beginning of the string (defualt) whereas the `search()` function checks for a match anywher in the string.
- The `findall()` function finds all the possible matches in the entire sequence and returns them as a list of strings.
- The `finditer()` is useful when you want to have more information returned from your search, such as their position in the original text.