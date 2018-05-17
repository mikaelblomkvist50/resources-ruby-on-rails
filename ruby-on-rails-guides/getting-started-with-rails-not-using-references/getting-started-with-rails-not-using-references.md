### You can read out this diagram as:
* an Article has **zero to many** Comments. (Rails terminology `has_many :comments`)
* a Comment has **one and only one** Article. (Rails terminology `belongs_to :article`, `#<Comment id: 3, article_id: "2"...`)

### Breaking it down further to ERD cardinality:

What's the minimum amount of **Comments** an **Article** might have? **0**<br/>
What's the maximum amount of **Comments** an **Article** might have? **many**<br/>
**0** + **many** = **zero to many**<br/>
Hence a **Article** has **zero to many Comments**.

---

What's the minimum amount of **Articles** a **Comment** might have? **1**<br/>
What's the maximum amount of **Articles** a **Comment** might have? **1**<br/>
**1** + **1** = **one and only one**<br/>
Hence a **Comment** has **one and only one Article**.

### Steps

1. [RVM gemset container](https://gist.github.com/JuliusRobertOppenheimer/c098915268af721d8e12bda9448d4e3d)
2. [Getting Started with Rails](http://guides.rubyonrails.org/getting_started.html)
3. [3.2 Creating the Blog Application ~ 4.3 Setting the Application Home Page](https://gist.github.com/JuliusRobertOppenheimer/b65bf0edd298ad6a7b0ab8bdda5ea34d)
4. [5 Getting Up and Running ~ 5.13 Deleting Articles](https://gist.github.com/JuliusRobertOppenheimer/847f19c79c1b87907fb3898751d715c8)
5. [6 Adding a Second Model ~  8.1 Deleting Associated Objects (not using references unlike original way in the guides)](https://gist.github.com/JuliusRobertOppenheimer/5aee86999252c4983040210778f61293)
6. [Articles Comments Seeds Hirb (not using references)](https://gist.github.com/JuliusRobertOppenheimer/425b518f94e684e005228ba105c52e92)

### Differences between using references and not using references

When `using references` inside the `comment.rb` file it automatically adds `belongs_to :article` like so:

```ruby
class Comment < ApplicationRecord
  belongs_to :article #Automatically included thanks to '$ rails generate model Comment commenter:string body:text article:reference'
end
```

Where as `not using references` inside the `comment.rb` file the `belongs_to :article` had to be manually added in like so:

```ruby
class Comment < ApplicationRecord
  belongs_to :article  #Manually added
end
```

---

When `using references` it automatically adds an `article_id` attribute to the `comment table`.

```
$ rails console

```


Where as `not using references` doesn't add an `article_id` attribute to the `comment table` instead it has to be add manually like so:

<pre><code>
$ <b>rails generate migration add_article_id_to_comments article_id:string</b>

$ <b>rake db:migrate</b>
== 20180328141618 AddArticleIdToComments: migrating ===========================
-- add_column(:comments, :article_id, :string)
   -> 0.0011s
== 20180328141618 AddArticleIdToComments: migrated (0.0012s) ==================
</pre></code>

```
$ rails console
Running via Spring preloader in process 76781
Loading development environment (Rails 5.1.5)
2.4.1 :001 > Article.all
  Article Load (1.7ms)  SELECT  "articles".* FROM "articles" LIMIT ?  [["LIMIT", 11]]
 => #<ActiveRecord::Relation [#<Article id: 1, title: "Best place to start learning Rails?", text: "Are these resources anygood? http://guides.rubyonr...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12">, #<Article id: 2, title: "Where to buy Bitcoin in Australia?", text: "Apart from local BitCoins, where else could I purc...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12">]>
2.4.1 :002 > Comment.all
  Comment Load (0.4ms)  SELECT  "comments".* FROM "comments" LIMIT ?  [["LIMIT", 11]]
 => #<ActiveRecord::Relation [#<Comment id: 1, commenter: "John", body: "Yes those are both informative and begginer friend...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "1">, #<Comment id: 2, commenter: "Mike", body: "I also recommend https://pragprog.com/book/rails51...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "1">, #<Comment id: 3, commenter: "Satoshi", body: "Checkout https://www.coinjar.com.au/", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "2">, #<Comment id: 4, commenter: "random", body: "https://www.coinspot.com.au/", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "2">]>
2.4.1 :003 >
```

---

When `using references` it automatically adds an index to the `article_id` inside the `db/schema.rb`:

```ruby
ActiveRecord::Schema.define(version: 20180327054904) do

 create_table "articles", force: :cascade do |t|
   t.string "title"
   t.text "text"
   t.datetime "created_at", null: false
   t.datetime "updated_at", null: false
 end

 create_table "comments", force: :cascade do |t|
   t.string "commenter"
   t.text "body"
   t.integer "article_id"
   t.datetime "created_at", null: false
   t.datetime "updated_at", null: false
   t.index ["article_id"], name: "index_comments_on_article_id"
 end

end
```

Where as `not using references` doesn't automatically add an index to the `article` as you can see inside the `db/schema.rb`:

```ruby
ActiveRecord::Schema.define(version: 20180328141618) do

  create_table "articles", force: :cascade do |t|
    t.string "title"
    t.text "text"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "comments", force: :cascade do |t|
    t.string "commenter"
    t.text "body"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.string "article_id"
  end

end
```

---

Where as `not using references` the `article_id` attribute has a data type of string (because I chose to):

```
$ rails console
Running via Spring preloader in process 76781
Loading development environment (Rails 5.1.5)
2.4.1 :001 > Article.all
  Article Load (1.7ms)  SELECT  "articles".* FROM "articles" LIMIT ?  [["LIMIT", 11]]
 => #<ActiveRecord::Relation [#<Article id: 1, title: "Best place to start learning Rails?", text: "Are these resources anygood? http://guides.rubyonr...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12">, #<Article id: 2, title: "Where to buy Bitcoin in Australia?", text: "Apart from local BitCoins, where else could I purc...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12">]>
2.4.1 :002 > Comment.all
  Comment Load (0.4ms)  SELECT  "comments".* FROM "comments" LIMIT ?  [["LIMIT", 11]]
 => #<ActiveRecord::Relation [#<Comment id: 1, commenter: "John", body: "Yes those are both informative and begginer friend...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "1">, #<Comment id: 2, commenter: "Mike", body: "I also recommend https://pragprog.com/book/rails51...", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "1">, #<Comment id: 3, commenter: "Satoshi", body: "Checkout https://www.coinjar.com.au/", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "2">, #<Comment id: 4, commenter: "random", body: "https://www.coinspot.com.au/", created_at: "2018-03-28 14:27:12", updated_at: "2018-03-28 14:27:12", article_id: "2">]>
2.4.1 :003 >
```
