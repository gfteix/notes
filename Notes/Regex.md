---
created-date: 2022-03-18
---

# Regex - JS

 `.test()` method takes the regex, applies it to a string (which is placed inside the parentheses), and returns `true` or `false` if your pattern finds something or not.
 
 1. **Match Literal Strings**

```javascript
let waldoIsHiding = "Somewhere Waldo is hiding in this text.";
let waldoRegex = /Waldo/; // Change this line
let result = waldoRegex.test(waldoIsHiding);
```

2. **Match a Literal String with Different Possibilities**

You can search for multiple patterns using the `alternation` or `OR` operator: `|`.
Complete the regex `petRegex` to match the pets `dog`, `cat`, `bird`, or `fish`.

```javascript 
let petString = "James has a pet cat.";
let petRegex = /dog|cat|bird|fish/; // Change this line
let result = petRegex.test(petString);
```

3. **Ignore Case While Matching**

`i flag`
`/ignorecase/i`
```javascript
let myString = "freeCodeCamp";
let fccRegex = /freeCodeCamp/i;
let result = fccRegex.test(myString);
```

4. **Extract Matches**

So far, you have only been checking if a pattern exists or not within a string. You can also extract the actual matches you found with the `.match()` method.

```javascript
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/;
let result = extractStr.match(codingRegex);
```

5. **Find More Than the First Match**

So far, you have only been able to extract or search a pattern once.
To search or extract a pattern more than once, you can use the `g` flag.

```javascript 
let twinkleStar = "Twinkle, twinkle, little star";
let starRegex = /twinkle/ig; 
let result = twinkleStar;
```

6. **Match Anything with Wildcard Period**

Sometimes you won't (or don't need to) know the exact characters in your patterns. Thinking of all words that match, say, a misspelling would take a long time. Luckily, you can save time using the wildcard character: `.`
For example, if you wanted to match `hug`, `huh`, `hut`, and `hum`, you can use the regex `/hu./` to match all four words.

Complete the regex `unRegex` so that it matches the strings `run`, `sun`, `fun`, `pun`, `nun`, and `bun`. Your regex should use the wildcard character:

```javascript
let exampleStr = "Let's have fun with regular expressions!";
let unRegex = /.un/;
let result = unRegex.test(exampleStr);
```

7. **Match Single Character with Multiple Possibilities**

For example, you want to match `bag`, `big`, and `bug` but not `bog`. You can create the regex `/b[aiu]g/` to do this. The `[aiu]` is the character class that will only match the characters `a`, `i`, or `u`.

Use a character class with vowels (`a`, `e`, `i`, `o`, `u`) in your regex `vowelRegex` to find all the vowels in the string `quoteSample`.
```javascript
let quoteSample = "Beware of bugs in the above code; I have only proved it correct, not tried it.";
let vowelRegex = /[aeiou]/gi;
let result = quoteSample.match(vowelRegex);

```

8. **Match Letters of the Alphabet**

For example, to match lowercase letters `a` through `e` you would use `[a-e]`.
Match all the letters in the string `quoteSample`.
```javascript
let quoteSample = "The quick brown fox jumps over the lazy dog.";
let alphabetRegex = /[a-z]/gi;
let result = quoteSample.match(alphabetRegex);
```

9. **Match Numbers and Letters of the Alphabet**
 `/[0-5]/` matches any number between `0` and `5`, including the `0` and `5`.
Also, it is possible to combine a range of letters and numbers in a single character set.

Create a single regex that matches a range of letters between `h` and `s`, and a range of numbers between `2` and `6`. Remember to include the appropriate flags in the regex.
```javascript

let quoteSample = "Blueberry 3.141592653s are delicious.";
let myRegex = /[h-s2-6]/gi;
let result = quoteSample.match(myRegex);
```

10. **Match Single Characters Not Specified**

you could also create a set of characters that you do not want to match. These types of character sets are called negated character sets.
For example, `/[^aeiou]/gi` matches all characters that are not a vowel.
Create a single regex that matches all characters that are not a number or a vowel. Remember to include the appropriate flags in the regex
```javascript
let quoteSample = "3 blind mice.";
let myRegex = /[^aeiou0-9]/gi; // Change this line
let result = quoteSample.match(myRegex); // Change this line
```

11. **Match Characters that Occur One or More Times**

 Sometimes, you need to match a character (or group of characters) that appears one or more times in a row. This means it occurs at least once, and may be repeated.
 You can use the `+` character to check if that is the case. Remember, * **the character or pattern has to be present consecutively**. That is, the character has to repeat one after the other
 For example, `/a+/g` would find one match in `abc` and return `["a"]`. Because of the `+`, it would also find a single match in `aabc` and return `["aa"]`.
If it were instead checking the string `abab`, it would find two matches and return `["a", "a"]` because the `a` characters are not in a row - there is a `b` between them. Finally, since there is no `a` in the string `bcd`, it wouldn't find a match.

You want to find matches when the letter `s` occurs one or more times in `Mississippi`. Write a regex that uses the `+` sign.

```javascript
let difficultSpelling = "Mississippi";
let myRegex = /s+/gi; // Change this line
let result = difficultSpelling.match(myRegex);
```

12. **Match Characters that Occur Zero or More Times**