# Maintainable Regular Expressions
### Matchers, Ready To Eat

A maintainable (and commentable!) way to write regexes in Java code. Everything is expressed as plain Java code; regex fragments can be reused across patterns. No more opaque regex strings!

## Example

```java

import sgreben.mre.CaptureGroup;
import sgreben.mre.Captured;
import sgreben.mre.Mre;

// Build a regular expression with capture groups
CaptureGroup word = Mre.capture(Mre.word());
CaptureGroup sentence = Mre.capture(Mre.seq(
    Mre.sepBy(Mre.whitespace(), word),
    Mre.seq(
        Mre.character('.'), 
        Mre.whitespaceOpt()
    )
));
Mre expression = Mre.many(sentence);

// Compile the expression into a matcher and process a string.
Matcher m = Mre.compile();
String s = "There are things. Things have properties.";
m.read(s)

// Comfortably extract matches and sub-matches
Captured capturedSentences = sentence.getCaptured();
Captured sentence1 = capturedSentences.get(0);
Captured sentence1Words = sentence1.getNested(word);
String sentence1Word2 = sentence1Words.getString(2);
assertEquals("things", word1);
  
```