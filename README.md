# Language feature ideas
## Symbols and accessors
Symbols can have different implementation depending on the context and os, but they always have the same meaning and outcome.
Symbol definitions should be only used for clarity.
```python
today: date.now
```
The accessor syntax defines some subset of data provided by the symbol.
```python
file("data.json").content

# Proposed syntax
file "data.json" . content
```

## Data transformation - map, take, filter
Declarative way of defining data transformation.
```python
5 sanitized(posts) as a(&.link) where &.published is today


# Gets five recent posts and transforms the to html links
(#
 posts: {
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
They should be ideally without side effects. The type information is also really extensive, including side effects, potentional paths the function can take and much more.
```python
sanitized posts:
    posts as escaped_html(&) # Uses the escape_html() transformation on every post
```
### Anonymous functions
using & in an expression creates an anonymous function.
```python
posts as escaped_html(&)

error_log: log &, level: critical
error_log "Uh oh" 

# Proposed syntax
posts as escaped_html(@)
```

## Data types
```python
# Table
{1, 2, 3, four: 4}
Table accessor syntax
_ . 1
_ 1
_ .four

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

# Documentation comment example
# adds one to @a
add_one a: a + 1

```
## Control flow
Proposals
```python
# If expression
customer_dashboard() if user.costumer else dashboard()

# Question expression
user.costumer?
    true: customer_dashboard()
    dashboard()

# Pattern assert
(#
Pattern assert can be used for replacing chain. It asserts that the constant is of some pattern,
and if it is not, it will return from the block.
#)
x :: {hello: "World", ...}
```

## Blocks
```python
x
    do_something _
    do_something_else _
    
# <- one single expression
```