db: sqlite("dev.db")
posts: db.tables.posts

#(
very gut funkcion i lajk it
)#
post data:
    html(
    h1(data.header),
    h3("{data.author} - {data.published}")  
    p(data.body),
    )

new_posts db:
    posts
        _ :: {post...}
        5 _ as post & where &.published is date.today

router path:
    path?
        {"posts", id}: post(posts where &.id is id)
        {"posts", "new"}: new_posts(db)

serve(router)

