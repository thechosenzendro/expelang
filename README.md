# Language feature ideas
## Symbols and accessors
Symbols can have different implementation depending on the context and os, but they always have the same meaning and outcome.
Symbol definitions should be only used for clarity.
```python
today: system.time.now.date
```
The accessor syntax defines some subset of data provided by the symbol.
```python
file("data.json").content
```

## Data transormation - map, take, filter
Declarative way of defining data transormation.
```python
5 sanitized(posts) as a(_.link) where _.published is today


# Gets five recent posts and transforms the to html links
(# posts: {
    {published: yesterday, link: "/1"},
    {published: today, link: "/2"},
    {published: today, link: "/3"},
    {published: today, link: "/4"},
    {published: today, link: "/5"},
    {published: today, link: "/6"},
} => {
    "<a href=\"/2\">",
    "<a href=\"/3\">",
    "<a href=\"/4\">",
    "<a href=\"/5\">",
    "<a href=\"/6\">",
}
#)
```
## Functions - transformers
Functions are just transformers of data where the type can be entirely discerned from the body.
they should be ideally without side effects. The type information is also really extensive, including side effects, potentional paths the function can take and much more.
```python
sanitized posts:
    posts as escaped_html(_) # Uses the escape_html() transformation on every post
```

## Data types
```python
# Table
{1, 2, 3, four: 4}
# Text
"Hello World"
# Number
14.7
# Logic value
True
False
```

## Comments
```python
# A comment
(#
Multiline
comment
#)
```
## Control flow
```python
# If expression
customer_dashboard() if user.costumer else dashboard()
```
# Rejected ideas
- imperative language
```python
posts
    sanitize :: {.success, ...}
    filter _.published is today
    take 5
    map a(_.link)

```
