# Week 10, Lab Report 5

## How the Tests Were Found
Tests were found using the diff on the results 
of running a bash for loop.<br>

## Test 1
* Test file: 201.md
* .md File Contents:<br>
```
    [foo]: (baz)

    [foo]
```
* Correct Output (Using CommonMark):<br>
```
[(baz)]
```
* My implementation: Incorrect
* My implementation output:
```
[]
```
* Provided implementation: Correct
* Provided implementation output:
```
[baz]
```
* Bug description (my code): My code immediately rules out a possible link if there is anything in-between the closed bracket and open parentheses, which rules out some valid links when there is a colon between the open bracket and the closed parentheses (a different style of marking a link).
* Part of code to be fixed:
```
    if (nextOpenBracket > 0 && 
            markdown.charAt(nextOpenBracket - 1) == '!' ||
            markdown.charAt(openParen - 1) != ']' || 
            newline2 < closeParen && newline2 > openParen) {
        currentIndex = closeParen + 1;
        continue;
}
```

## Test 2
* Test file: 41.md
* .md File Contents:<br>
```
[a](url "tit")
```
* Correct Output (Using CommonMark):<br>
```
[url]
```
* My implementation: Incorrect
* My implementation output:
```
[url &quot;tit&quot;]
```
* Provided implementation: Incorrect
* Provided implementation output:
```
[]
```
* Bug description (my code): My code currently returns all of the text inside the parentheses as the link. However, this fails to account for the unique case in which there is (actual_link "link_label"), for which CommonMark uses actual_link as the link and ignores the "link_label".
* Part of code to be fixed:
```
toReturn.add(markdown.substring(openParen + 1, closeParen));
```

