# Markdown
Github flavoured Markdown cheatsheet.

## Headings
```
# Sample H1
## Sample H2
### Sample H3
#### Sample H4
##### Sample H5
###### Sample H6
```

## Basic Formatting
```
*Italic* or _Italic_
**Bold** or __Bold__
***Bold and Italic*** or ___Bold and Italic___
~~Strikethrough~~
`Inline code` or ``Inline code``
```
Following characters can be `\`-escaped: ``\`*_{}[]()#+-.!|``


## Links
#### Inline links
```
[Link Text](schema://url)
*[Formatted Link Text](schema://url "Optional title")*
[![Image Link](schema://url/image "Optional title")](schema://url)
```

#### Reference style links
```
[Link Text][1]
[Link Text] [2]
[![Image Link](schema://url/image)][3]
...
[1]: schema://url
[2]: schema://url "Title"
[3]: schema://url
```

#### Implicit URLs and e-mails
```
<http://www.domain.com>
<https://www.domain.com>
<person@domain.com>
```


## Blocks
#### Code blocks
```
\`\`\` bash
for I in 1 2 3; do
    echo "$I Hello world"
done
\`\`\`
```


## Lists
#### Unordered lists
```
- First
- Second
  - First nested
  - Second nested
- Third

  Paragraph in list item using __whatever__ formating, block or table.

```
Recognized bullets: `-*+`.

#### Ordered lists
```
1. First
2. Second
  1. First nested
  1. Second nested, numbering will be fixed automatically
3. Third
  - First unordered
  - Second unordered
```


## Tables
```
| Default | Left | Center | Right |
| ------- | :--- | :----: | ----: |
| Text    | Text | Text   | Text  |
```


## Images
```
![Alt text](/path/to/image)
![Alt text](http://domain/image.jpg "Title")
```


## Rulers and Line Breaks
```
___
---
<br>
Two or more spaces at the end of line.__
```
