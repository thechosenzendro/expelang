symbols are just hints, the compiler decides what to do with them

```
db.tables.articles filter (_.published is today) map h1(_.header)
((db.tables.articles) filter (_.published is today)) map h1(_.header)

db.tables.articles
    filter (_.published is today)
    map h1(_.header)
```

the accessor syntax defines some subset of data provided by the symbol
```
file("data.json").contents
```

You can emulate "the chain" using pattern matching
```
# The imperative way to do it
posts
    sanitize :: {.success, ...}
    filter _.published is today
    take 5
    map a(_.link)

# Fuck this is perfect
5 sanitized(posts) as a(_.link) where _.published is today


# Gets five recent posts and transforms the to html links
(# posts: {
    {published: yesterday, link: "/1"},
    {published: today, link: "/2"},
    {published: today, link: "/3"},
    {published: today, link: "/4"},
    {published: today, link: "/5"},
    {published: today, link: "/6"},
}
#)

(# => {
    "<a href=\"/2\">",
    "<a href=\"/3\">",
    "<a href=\"/4\">",
    "<a href=\"/5\">",
    "<a href=\"/6\">",
}
#)
```
symbol definitions should be only used for clarity
```
today: system.time.now.date
```
functions are just transformers of data where the type can be entirely discerned from the body.
they should be ideally without side effects. The type information is also really extensive, including side effects
```
sanitized posts:
    posts as escaped_html(_)
```
compiler has a "symbol resolver" that actually resolves the symbols and decides on implementations based on context.

Data types
```
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

all transformations without side effects will be computed at compile time

comments
```
# A comment
(#
Multiline
comment
#)
```
figure out logic