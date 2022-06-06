# THM  - Regular Expressions

> Michael Jack | 06/2022

[TryHackMe | Regex](https://tryhackme.com/room/catregex)

Help: https://martinkubecka.github.io/posts/thm/regular-expressions/

---

## Task 1 - Introduction

> Regular expressions (or Regex) are patterns of text that you define to search documents and match exactly what you're looking for.

---

## Task 2 - Charsets

Regular expressions help you search for patterns of text. We can do this using *charsets*.

A charset is defined by what you enclose inside square brackets (```[``` & ```]```) as part of your regex.

It will find every occurrence of the pattern you have defined in whatever you are searching.

### Examples
- ```[abc]``` would match every occurrence of ```a```, ```b```, and ```c```.
- ```[abc]zz``` would match ```azz```, ```bzz```, and ```czz```. What's left out is treated like a normal string search modified by the charset pattern.
- We can also use ranges! So the above could also be ```[a-c]zz```. 
	- We can combine ranges to like ```[a-cx-z]zz```.
- Commonly used is matching every alphabetic character with ```[a-zA-Z]```.
- Numbers also work: ```file[1-3]``` would give ```file1```, ```file2```, and ```file3```.
- IF we want to exclude characters we use ```^```. We can use this with specific characters individually, or with ranges,

*Note the questions here will really suck as they want one randomly chosen answer by the author.* 
*Does not take into account that overly general searches are less practical while preferring the vaguest possible regex as the proper answer.*

### Questions

> Match all of the following characters: c, o, g

```
[cog]
```

> Match all of the following words: cat, fat, hat

```
[cfh]at
```

> Match all of the following words: Cat, cat, Hat, hat

```
[CcHh]at
```

> Match all of the following filenames: File1, File2, file3, file4, file5, File7, file9

```
[fF]ile[1-9]
```

> Match all of the filenames of question 4, except "File7" (use the hat symbol)

```
[fF]ile[^7]
```

---

## Task 3 - Wildcards and Optional Characters

> The wildcard that is used to match any single character (except the line break) is the `.` dot. That means that `a.c` will match `aac`, `abc`, `a0c`, `a!c`, and so on.
> Also, you can set a character as optional in your pattern using the `?` question mark. That means that `abc?` will match `ab` and `abc`, since the `c` is optional.
> Note: If you want to search for `.` a literal dot, you have to **escape it** with a `\` reverse slash. > That means that `a.c` will match `a.c`, but also `abc`, `a@c`, and so on. But `a\.c` will match **just** `a.c`.

### Questions

> Match all of the following words: Cat, fat, hat, rat

```
.at
```

> Match all of the following words: Cat, cats

```
[cC]ats?
```

> Match the following domain name: cat.xyz

```
cat\.xyz
```

> Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz

```
[ch]ats?\.xyz
```

> Match every 4-letter string that doesn't end in any letter from n to z

```
...[^n-z]
```

> Match bat, bats, hat, hats, but not rat or rats (use the hat symbol)

```
[^r]ats?
```

---

## Task 4 - Metacharacters and Repetitions

There are easier ways to match bigger charsets. For example, `\d` is used to match any **single** digit. Here's a reference:  

- `\d` matches a digit, like `9`  
- `\D` matches a non-digit, like `A` or `@`  
- `\w` matches an alphanumeric character, like `a` or `3`  
- `\W` matches a non-alphanumeric character, like `!` or `#`  
- `\s` matches a whitespace character (spaces, tabs, and line breaks)  
- `\S` matches everything else (alphanumeric characters and symbols)

Note: Underscores `_` are included in the `\w` metacharacter and not in `\W`. That means that `\w` will match every single character in `test_file`.

Often we want a pattern that matches many characters of a single type in a row, and we can do that with repetitions. For example, `{2}` is used to match the preceding character (or metacharacter, or charset) two times in a row. That means that `z{2}` will match exactly `zz`.

Here's a reference for each repetition along with how many times it matches the preceding pattern:

- `{12}` - **exactly 12** times.  
- `{1,5}` - **1 to 5** times.  
- `{2,}` - **2 or more** times.  
- `*` - **0 or more** times.  
- `+` - **1 or more** times.

### Questions

> Match the following word: catssss

```
cats{4}
```

> Match all of the following words (use the * sign): Cat, cats, catsss

```
[Cc]ats*
```

> Match all of the following sentences (use the + sign): regex go br, regex go brrrrrr

```
regex go br+
```

> Match all of the following filenames: ab0001, bb0000, abc1000, cba0110, c0000 (don't use a metacharacter)

```
[abc]{1,3}[01]{4}
```

> Match all of the following filenames: File01, File2, file12, File20, File99

```
[Ff]ile\d{1,2}
```

> Match all of the following folder names: kali tools, kali     tools

```
kali\s+tools
```

> Match all of the following filenames: notes~, stuff@, gtfob#, lmaoo!

```
\w{5}\W
```

> Match the string in quotes (use the * sign and the \s, \S metacharacters): "2f0h@f0j0%!     a)K!F49h!FFOK"

```

```