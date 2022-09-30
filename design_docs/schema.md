# Postgres Database Schema

add this where you need to (remove this comment later -- give this person a strike if this is still here)
| `$` | string/integer/float/boolean | not null, indexed, foreign key, unique |

## `users`

| column name       | data type | details                   |
| :---------------- | :-------: | :------------------------ |
| `id`              |  integer  | not null, primary key     |
| `username`        |  string   | not null, indexed, unique |
| `email`           |  string   | not null, indexed, unique |
| `password_digest` |  string   | not null                  |
| `session_token`   |  string   | not null, indexed, unique |
| `created_at`      | datetime  | not null                  |
| `updated_at`      | datetime  | not null                  |

- index on `username, unique: true`
- index on `email, unique: true`
- index on `session_token, unique: true`
- `has_many posts`
- `has_many likes`
- `has_many friends` (references users)
- `has_many comments`

## `posts`

| column name  | data type | details                        |
| :----------- | :-------: | :----------------------------- |
| `id`         |  integer  | not null, primary key          |
| `body`       |   string  | not null                       |
| `author_id`  |  integer  | not null, indexed, foreign key |
| `created_at` | datetime  | not null                       |
| `updated_at` | datetime  | not null                       |

- `author_id` references `users`
- index on `author_id`
- `belongs_to author`
- `has_many likes`
- `has_many comments`

## `likes`

| column name  | data type | details                        |
| :----------- | :-------: | :----------------------------- |
| `id`         |  integer  | not null, primary key          |
| `user_id`    |  integer  | not null, indexed, foreign key |
| `post_id`    |  integer  | not null, indexed, foreign key |
| `created_at` | datetime  | not null                       |
| `updated_at` | datetime  | not null                       |

- `user_id` references `users`
- `post_id` references `post`
- index on [:post_id, :user_id], unique: true
- `belongs_to post`
- `belongs_to user`

## `comments`

| column name  | data type | details                        |
| :----------- | :-------: | :----------------------------- |
| `id`         |  integer  | not null, primary key          |
| `body`       |   string  | not null                       |
| `user_id`    |  integer  | not null, indexed, foreign key |
| `post_id`    |  integer  | not null, indexed, foreign key |
| `created_at` | datetime  | not null                       |
| `updated_at` | datetime  | not null                       |

- `user_id` references `users`
- `post_id` references `post`
- index on [:post_id, :user_id], unique: true
- `belongs_to post`
- `belongs_to user`