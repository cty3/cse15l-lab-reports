# MarkdownParse Snippet Tests
[My implementation can be found here](https://github.com/cty3/markdown-parse.git)

[The implementation I reviewed can be found here](https://github.com/maotcha/markdown-parse)

* Since the implementation I reviewed changed the header of the getLinks method, my methods for both implementations would differ for each snippet

> **Snippet 1**

* I used VScode preview to decide what it should produce: `google.com, google.com, ucsd.edu

**My implementation**
* Code in the test
```
@Test
public void testSnippet1() throws IOException {
    Path filename = Path.of("snippet1.md");
    String contents = Files.readString(filename);
    assertEquals(List.of("`google.com", "google.com", "ucsd.edu"), MarkdownParse.getLinks(contents));
    }
```
* My implementation didn't pass the test.
* Output:

![Image](labreport4-1.png)

* I would need more than 10 lines to fix it, as the influence of ticks appear to vary for parenthesis and brackets. I might need to define the order of priority/importance of ticks, brackets, and parentheses. The program will therefore be able to return the correct list of links, of which url.com doesn't appear when the content in its brackets are interrupted by the ticks.

**The implementation I reviewed**
* Code in the test
```
@Test
public void testSnippet1() throws IOException {
    Path filename = Path.of("snippet1.md");
    String contents = Files.readString(filename);
    String[] contentsArray = contents.split("\n");
    assertEquals(MarkdownParse.getLinks(contentsArray), List.of("`google.com", "google.com", "ucsd.edu"));
}
```
* The implementation I reviewed didn't pass the test.
* Output: 

![Image](labreport4-extra.png)

> **Snippet 2**

* I used VScode preview to decide what it should produce: a.com, a.com(()), example.com

**My implementation**
* Code in the test
```
@Test
 public void testSnippet2() throws IOException {
    Path filename = Path.of("snippet2.md");
    String contents = Files.readString(filename);
    assertEquals(List.of("a.com", "a.com(())", "example.com"), MarkdownParse.getLinks(contents));
}
```

* My implementation didn't pass the test.
* Output:

![Image](labreport4-2.png)

* It's possible to make my program work for a nested parenthesized url with a change that takes fewer than 10 lines.I'll need to make sure that getLinks return the content between first open paren after the closing bracket and the last closing paren before the next open bracket. 

**The implementation I reviewed**
* Code in the test
```
@Test
public void testSnippet2() throws IOException {
    Path filename = Path.of("snippet2.md");
    String contents = Files.readString(filename);
    String[] contentsArray = contents.split("\n");
    assertEquals(List.of("a.com", "a.com(())", "example.com"), MarkdownParse.getLinks(contentsArray));
}
```
* The implementation I reviewed didn't pass the test.
* Output: 

![Image](labreport4-3.png)


> **Snippet 3**

* I used CommonMark demo site to decide what it should produce: https://ucsd-cse15l-w22.github.io/

**My implementation**
* Code in the test: 
```
@Test
public void testSnippet3() throws IOException {
    Path filename = Path.of("snippet3.md");
    String contents = Files.readString(filename);
    assertEquals(List.of("https://ucsd-cse15l-w22.github.io/"), MarkdownParse.getLinks(contents));
}
```
* My implementation didn't pass the test.
* Output:

![Image](labreport4-4.png)

* It would need more than 10 line to fix it. First, we need to use readString to make sure that the link output doesn't have blank spaces around it. Secondly, we need to somehow introduce functions to skip the current set of brackets/parentheses when contents in them have super long line breaks, as well as when brackets/parentheses are not paired before the next link.

**The implementation I reviewed**
* Code in the test
```
@Test
public void testSnippet3() throws IOException {
    Path filename = Path.of("snippet3.md");
    String contents = Files.readString(filename);
    String[] contentsArray = contents.split("\n");
    assertEquals(List.of("https://ucsd-cse15l-w22.github.io/"), MarkdownParse.getLinks(contentsArray));
}
```
* The implementation I reviewed didn't pass the test.
* Output: 

![Image](labreport4-5.png)