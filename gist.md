# Regex Tutorial - URL Validation

Regex, or Regular Expression Syntax, is a useful tool for any web developer. Regular Expressions define a search pattern and are very useful for form input validation, web scraping, and filtering information. Regex may appear intimidating initially, but they can be broken down into smaller components so they can be more easily understood.

Link to Github Gist [here](https://gist.github.com/jsugihara00123/aecb0d7bc99e990de78806e4877b48d9)

## Summary

In this gist, I will be explaining Regex used for matching a URL. Using Regex to match the URL will ensure that all the neccessary components of a URL is present.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Character Escapes](#character-escapes)
- [Resources](#resouces)

## Regex Components

Regular expressions use forward slashes on either side of the expression to seperate the characters. The Regex Expression I will be demonstrating in this tutorial is ```/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/```

This does not validate that the URL is actually operational or connects to a webpage, it merely checks the pattern of the string and ensures the neccessary components are there.

### Anchors

THe anchors are the beginning and the end of this regex expression. The anchors are immediately betweent the forward slashes at the beginning and end of the expression. The beginning anchor is the ```^``` character and the ending anchor is the ```$``` character. Below they are highlighted as part of the expression.

/```^```(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?```$```/

### Quantifiers

Quantifiers are important for Regex Expressions because they count how many times a character, group, or class must be present for a match to be found. 

In the expression covered in this tutorial, there are several quantifiers we can assess.

```/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/```

1. The first quantifier in this expression is the ```?``` character in /^(https```?```:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

    * ```?``` will match zero to one time, which means it will match even if the item is ommitted. The quantifier is preceeded by the ```s``` which in turn means that the URL can start with either ```http``` or ```https```, but ```httpf``` will not match.  

2. The second quantifier in this expression is also the ```?``` character, but this time it follows a group of characters in parenthesis. 

    * /^(https?:\/\/)```?```([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

    * Due to the different placing, this quanitifier has a slightly different role because it validates the entire group present within the parathesis. It will match zero to one time, meanning that it will match weather the https:// or http:// is present or absent. For example, both of the below URLs will match:

    ``` 
    https://www.github.com
    www.github.com
    ```

3. The next quantifier is the ```+``` 

    * /^(https?:\/\/)?([\da-z\.-]```+```)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

    * The ```+``` means it matches one or more times. This means that the item preceeding it must occur atleast once but can occur an infinite amount of time. The preceeding item is the following ```[\da-z\.]``` which means the match will work for any given string between the ```https://``` and the last ```.``` before ```com``` or ```org```.

4. The curly bracket quantifier seen as the ```{2,6}``` in this expression matches the amount of times within the bracket. The comma in the middle signifies it will match an amount of times between the two numbers. In our case, it will match between 2 and 6 times.

    * /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]```{2,6}```)([\/\w \.-]*)*\/?$/

    * This quantifier preceeds the ```[a-z\.]``` which means the domain must be within 2-6 characters. Here are some examples: 

    ```
    .com
    .co
    .edu
    ```

5. The last quantifier type in this expression is the ```*``` which is present two times in this expression

    * /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]```*```)```*```\/?$/

    * One time it is within parenthesis and one time outside which have different functions. The ```*``` will match zero or more times and preceeding the first ```*``` is ```[\/\w \.-]``` which means it will match any leangth string after the ```.com```, ```.edu```, etc. It can be blank or very very long.

    * Here are some examples:

    * The second ```*``` in the expression preceeds the group of characters ```([\/\w \.-]*)``` which is preceeding the entire group in parenthesis which means it will match the url with many levels seperated by ```/``` after the root of the url.

### Grouping Constructs

Grouping constructs are seperated by paranthesis are helpful in breaking down this Regex expression into several parts.
Below are each of the grouping constructs explained.

1. ```(https?:\/\/)```

    * This group will only match if the following are found:
        - The string ```http```
        - ```s``` which may or may not be present due to its quantifier ```?```
        - The colon ```:```
        - Two forward slashes ```//``` written in this expression as ```\/\/```

2. ```([\da-z\.-]+)```

    * The characters in this expression mean it will match if the string contains at minimum one of the characters in the expression due to its quantifier ```+````

3. ```([a-z\.]{2,6}```

    * This group contains a bracket and a quantifier which means it will match only if the number of characters match the quantifier (2-6) and must be from the characters in the brackets (a-z).

4. ```([\/\w \.-]*)```

    * This group along with its quantifier means that it will match with an exmpty string or any string where the characters are the same as between the brackets.

### Bracket Expressions

Bracket expressions demonstrate a range of characters that would need to be matched.

1. ```[\da-z\.-]```

    * ```\d``` means any numeric character
    * ```a-z``` means any lowercase letter
    * ```\.``` means a period is neccessary
    * ```-``` means a hyphen is needed

2. ```[a-z\.]```

    * ```a-z``` means any lowercase letter
    * ```\.``` means a period is neccessary
 
3. ```[\/\w \.-]```

    * ```\/``` a forward slash is needed
    * ```\w``` any alphanumeric character
    * ```" "``` a space
    * ```\.``` a period
    * ```-``` a hyphen

### Character Classes

* This expression has 3 different character classes:

1. ```\d``` matches with any number character ```0-9```
2. ```\w``` matches any alphanumeric character including the underscore: ```a-z```, ```A-Z```, ```0-9```, and ```_```.
3. ```a-z``` matches with any lowercase alphabetic character

### Character Escapes

Character Escapes means an escaping backslash mush be present before special function characters for the Regex to look for strings. There are two in this Regex Expression:

1. ```\/``` used to match with a forward slash ```/```
2. ```\.``` used to match with a period ```.```

## Author

Jon is a Bootcamp student for the University of Utah. Github account [here.](https://github.com/jsugihara00123
) 

## Resources

Below are some of the helpful resources that helped me understand Regex and were helpful in the making of this tutorial:

- [Request-Response: A Full-Stack Blog](https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial)

- [Microsoft Docs- Regular Expressions](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions)

- [Regex 101](https://regex101.com/)

- [Introduction to Regular Expressions- Youtube](https://www.youtube.com/watch?v=7DG3kCDx53c)

- [Regex for URL](https://ihateregex.io/expr/url/)