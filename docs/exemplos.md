develop
# ARTIGO DE EXEMPLO

## TITULO 1

### TITULO 2

#### TITULO 3

- fds
- fds

Emphasis, aka italics, with *asterisks* or _underscores_.

Strong emphasis, aka bold, with **asterisks** or __underscores__.

Combined emphasis with **asterisks and _underscores_**.

Strikethrough uses two tildes. ~~Scratch this.~~

1. First ordered list item
2. Another item
   ⋅⋅- Unordered sub-list
3. Actual numbers don't matter, just that it's a number
   ⋅⋅1. Ordered sub-list
4. And another item

⋅⋅⋅You can have properly indented paragraphs within list items. Notice the blank line above, and the leading spaces (at least one, but we'll use three here to also align the raw Markdown).

There are two ways to create links:

[I'm a basic link](https://www.google.com)

[Hover over me to see my link title](https://www.google.com "Google's Homepage")

[Link para outro arquivo markdown (marcas)](./brand/brands.md)


Here's our logo (hover to see the title text):

![Stoplight Logo](https://stoplight.io/images/home/logo-blue-black.png "Stoplight Logo")

Sem Efeito
<!--
focus: false
-->
![Stoplight Logo](https://stoplight.io/images/home/logo-blue-black.png "Stoplight Logo")

Exemplo de JSON
```json
{
  "JSON": "Syntax Highlighting"
}
```
json com titulo
```json title="Passed via meta tag" lineNumbers
{
  "title": "User",
  "type": "object"
}
```
l

<!--
type: tab
title: Json
-->
```json title= Json
{
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    }.
    "number": {
      "type": "integer"
    }
  }
}
```
<!--
type: tab
title: Json Schema
-->
```json json_schema
{
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    },
    "name": {
      "type": "string",
      "description": "The user's full name."
    },
    "age": {
      "type": "number",
      "minimum": 0,
      "maximum": 150
    }
  },
  "required": ["id", "name"]
}
```
<!-- type: tab-end -->

json schema

```json json_schema
{
  "title": "User",
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    },
    "name": {
      "type": "string",
      "description": "The user's full name."
    },
    "age": {
      "type": "number",
      "minimum": 0,
      "maximum": 150
    }
  },
  "required": ["id", "name"]
}
```

Colons can be used to align columns.

| Tables        |      Are      |   Cool |
| ------------- | :-----------: | -----: |
| col 3 is      | right-aligned | \$1600 |
| col 2 is      |   centered    |   \$12 |
| zebra stripes |   are neat    |    \$1 |
There must be at least 3 dashes separating each header cell. The outer pipes (|) are optional, and you don't need to make the raw Markdown line up prettily. You can also use inline Markdown.

| Markdown | Less      | Pretty     |
| -------- | --------- | ---------- |
| _Still_  | `renders` | **nicely** |
| 1        | 2         | 3          |


> Blockquotes are very handy in email to emulate reply text.
> This line is part of the same quote.

Quote break.

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can _put_ **Markdown** into a blockquote.

Before.

---

After.

Exemplo link de vídeo

[![Everything Is AWESOME](https://img.youtube.com/vi/s7UUawSvtX0/hqdefault.jpg)](https://www.youtube.com/watch?v=s7UUawSvtX0 "Everything Is AWESOME")

Exemplo de Gif
![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)


<!-- theme: danger -->

> #### Danger Will Robinson!
>
> Here is my danger callout!

<!-- theme: warning -->
> #### Watch Out!
>
> Here is my warning callout!

<!-- theme: success -->

> #### Mission Accomplished!
>
> Here is my success callout!


- [ ] one
- [x] two
- [ ] three




