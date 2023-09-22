# Markdown syntax guide

<br>

Bitbucket Data Center 및 Server는 CommonMark에 지정된 대로 Markdown을 사용하여 text 서식을 지정.  
다음 위치에서 Markdown 사용 가능:
- Pull request의 descriptions나 comments
- README files(file 확장자가 .md인 경우)

Markdown을 미리 보려면, `Control+Shift+P`나 `Command+Shift+P` 사용.  
Bitbucket Data Center 및 Server는 HTML tags를 지원하지 않으며 모든 HTML tags는 escape됨.

<br>

## Markdown syntax
### Headings
```
# This is an H1
## This is an H2
###### This is an H6

This is also an H1
==================

This is also an H2
------------------
```

<br>

### Paragraphs
Paragraphs은 빈 줄로 구분되고 새 Paragraph를 만들려면 \<return\>(\<Enter\>)을 두 번 누르면 됨.
```
Paragraph 1

Paragraph 2
```


<br>

### Character styles
```
*Italic characters* 
_Italic characters_
**bold characters**
__bold characters__
~~strikethrough text~~
```

<br>

### Unordered list
```
*  Item 1
*  Item 2
*  Item 3
    *  Item 3a
    *  Item 3b
    *  Item 3c
```

<br>

### Ordered list
```
1.  Step 1
2.  Step 2
3.  Step 3
    1.  Step 3.1
    2.  Step 3.2
    3.  Step 3.3
```

<br>

### List in list
```
1.  Step 1
2.  Step 2
3.  Step 3
    *  Item 3a
	*  Item 3b
	*  Item 3c
```

<br>

### Quotes or citations
```
Introducing my quote:

> Neque porro quisquam est qui 
> dolorem ipsum quia dolor sit amet, 
> consectetur, adipisci velit...
```

<br>

### Inline code Characters
```
Use the backtick to refer to a `function()`.
 
There is a literal ``backtick (`)`` here.
```

<br>

### Code blocks
```
Indent every line of the block by at least 4 spaces.

This is a normal paragraph:

    This is a code block.
    With multiple lines.

Alternatively, you can use 3 backtick quote marks before and after the block, like this:

\```
This is a code block
\```

To add syntax highlighting to a code block, add the name of the language immediately
after the backticks: 

\```javascript
var oldUnload = window.onbeforeunload;
window.onbeforeunload = function() {
    saveCoverage();
    if (oldUnload) {
        return oldUnload.apply(this, arguments);
    }
};
\```
```

Bitbucket은 CodeMirror를 사용하여 comments, READMEs 및 pull request descriptions의 rendering된 markdown에 구문 강조를 적용.  
C, C++, Java, Scala, Python 및 JavaScript를 포함한 모든 일반적인 coding 언어가 지원됨.

Code block 내에서 amperands(`&`)와 angle brackets(`<` 및 `>`)는 자동으로 HTML entities로 변환됨.

<br>

### 외부 websites links
```
This is [an example](http://www.example.com/) inline link.

[This link](http://example.com/ "Title") has a title attribute.

Links are also auto-detected in text: http://example.com/
```

<br>

### Issue keys를 JIRA applications에 연결
Comments 및 pull request descriptions에 Jira application issue keys(기본 형식)를 사용하면, Bitbucket은 자동으로 이를 Jira application instance에 연결.

기본 Jira application issue key 형식은 두 개 이상의 대문자(`[A-Z][A-Z]+`) 뒤에 hyphen과 issue 번호가 옴(ex: TEST-123).

<br>

### Pull requests에 연결
Bitbucket 4.9에 도입된 기능으로 다른 pull requests의 comments 및 descriptions에서 pull requests 참조 가능.  
Pull request에 연결하는 구문은 다음과 같음:
```
projectkey/repo-slug#pr_id
```

**동일한 project 및 repository에 있는 pull request에 연결하려면**, pull request ID만 포함하면 됨.
```
#123
```

**동일한 project이지만 다른 repository에 있는 pull request에 연결하려면**, pull request ID앞에 repository slug를 포함.
```
example-repo#123
```

**다른 project 및 repository 의 pull request에 연결하려면**, pull request ID앞에 project key와 repository slug를 포함.
```
PROJ/example-repo#123
```

<br>

## Images


### Tables
```
| Day     | Meal    | Price |
| --------|---------|-------|
| Monday  | pasta   | $6    |
| Tuesday | chicken | $8    |
```

<br>

## Backslash escapes
특정 문자는 특수한 Markdown 의미 대신 문자 그대로의 표시를 유지하기 위해 앞에 backslash를 사용하여 escape 가능.  
이는 다음 문자에 적용됨:
```
\  backslash
`  backtick
*  asterisk
_  underscore
{} curly braces
[] square brackets
() parentheses
#  hash mark
>  greater than
+  plus sign
-  minus sign (hyphen)
.  dot
!  exclamation mark
```

<br>

## README files
Repository에 root 수준의 README.md file이 포함되어 있는 경우, Bitbucket은 file 확장자가 .md이면 repository의 **Source** page에 해당 내용을 표시. 
File에는 Markdown만 포함 가능.

<hr>

## 참고
- **Markdown syntax guide** - https://confluence.atlassian.com/bitbucketserver0813/markdown-syntax-guide-1283690270.html
