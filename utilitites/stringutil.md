# StringUtil

Strings manipulation is a common and frequent task in the everyday life of a developer. JDK doesn't provide much help on this topic. The `StringUtil` class offers more than **100** additional string utilities \(and still growing\). And each one is optimized for speed. Description of some methods follows, more details can be founded in JavaDoc and test cases.

### Replacing

`replace()` is one of the most missing functionality String needs. It doesn't use a regular expression, just simply replaces all founded substrings. Alternatively, there is a method that replaces just first or last occurrence of some substring: `replaceFirst()` and `replaceLast()`, respectively.

Besides substrings, it is possible to replace a single character as well as several characters at once, by using `replaceChars()`.

### Removing

Similar to replace methods, removing methods removes all substring occurrences from the provided target string: `remove()`. The same can be done for removing a single character, as well as more characters at once: `removeChars()`.

### Empty string detection

`StringUtil` provides methods for the detection of empty and blank strings. Empty strings are those that are either `null` or with zero-length; `isEmpty()`, `isNotEmpty()`. Blank strings are those that are either empty or that contains just whitespaces; `isBlank()`, `isNotBlank()`.

`StringUtil` also may check several strings at once: `isAllBlank()`, `isAllEmpty()`.

### Safe equals

`equals()` offers safe compression of provided strings: it will not fail if one of the arguments is `null`. Similarly, there is `equalsIgnoreCase()` for checking two strings ignoring the characters case.

### Capitalization

Two methods that are always needed: `capitalize()` and `uncapitalize()`.

### Splitting

When parsing, splitting a string into substrings is also a common task. `StringUtil` offers several split methods.

`split(String src, String delimiter)` splits a string into several parts \(tokens\) that are separated by a delimiter. A delimiter is **always** surrounded by two strings \(tokens\)! If there is no content between two delimiters, an empty string will be returned for that token. Therefore, the length of the returned array will always be `#delimiters + 1`. This method is much, much faster than regexp variant `String.split()` and just a bit faster than `StringTokenizer`.

`splitc(String src, char d)` and `splitc(String src, String d)`splits a string into several parts \(tokens\) that are separated by delimiter **characters**. A delimiter may contain any number of characters, and it is always surrounded by two strings.

### IndexOfs

`StringUtil` provides many missing `indexOf` methods. It is possible to scan just an inner part of a string, to ignore case while searching, to scan in both directions \(from start or and of the string\)... There are also more scanners, such: `lastIndexOfWhitespace()` and `lastIndexOfNonWhitespace()`.

In the same manner, `startsWithIgnoreCase()` and `endsWithIgnoreCase()` are commonly needed methods.

But that is not all:\) It is also possible to scan for more strings at the same time. Such methods return an `int` array, where the first element is a substring index and the second element is founded position.

There are also character-oriented scanners, that search for the first/last occurrence of provided character\(s\).

### Strips, crops, trims, and cuts

Another set of common methods for trimming \(removing whitespaces from left and right\), cropping \(setting empty strings to `null`\), stripping \(first or last characters from a string in a safe manner\) and cutting \(cut a string from the beginning or from the end up to the first occurrence of some substring, or cutting last or first words\).

### indexOfRegion

This is a powerful region scanning method that returns indexes of the first occurrence of some string region. The region is and substring defined by its left and right boundary. The return value is an array of the following indexes: start of left boundary index, region start index \(i.e. end of the left boundary\), region end index \(i.e. start of the right boundary\), and end of right boundary index.

Escape characters may be used to prefix boundaries so they can be ignored. Double escaped regions will be found, and the first index of the result will be decreased to include one escape character. If a region is not founded, `null` is returned.

### And more!

Obviously, this is just a subset of the ever-growing number of utilities we provide in the `StringUtil`. Please check the code or the JavaDocs :\)

