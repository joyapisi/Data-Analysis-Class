```sql

CREATE TABLE Users (
    user_id INTEGER PRIMARY KEY,
    username TEXT
);

CREATE TABLE Posts (
    post_id INTEGER PRIMARY KEY,
    content TEXT
);

CREATE TABLE Likes (
    user_id INTEGER,
    post_id INTEGER,
    PRIMARY KEY (user_id, post_id),
    FOREIGN KEY (user_id)
        REFERENCES Users(user_id),
    FOREIGN KEY (post_id)
        REFERENCES Posts(post_id)
);
```

Here, Likes is the junction table. One user can like many posts, and one post can receive likes from many users

