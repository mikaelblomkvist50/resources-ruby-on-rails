https://books-heroku-ror.herokuapp.com/

### Tech Stack

![books_heroku_ror_tech_stack](https://user-images.githubusercontent.com/22141530/36624821-83047326-1968-11e8-869d-fd05f2b9cd28.png)


### Site Map

![books_heroku_ror_site_map](https://user-images.githubusercontent.com/36538863/36625474-40f97380-1974-11e8-966d-1a3de584727d.png)


### DB Schema

<img width="585" alt="screen shot 2018-02-24 at 4 55 46 pm" src="https://user-images.githubusercontent.com/22141530/36626253-a7a7f228-1983-11e8-8c2f-fbad60f5f786.png">

## Entity relationship diagram

Book Table:

<img width="1116" alt="screen shot 2018-02-25 at 3 36 42 pm" src="https://user-images.githubusercontent.com/22141530/36638182-d999dcec-1a41-11e8-8e57-c765f1c2ab40.png">

**Primary Key** is an **attribute** (being the `book_id` in this case) that uniquely identifiers every recored in that certain table. Since a single attribute can accomplish all that, it makes sense that you will have 1 **Primary Key** per an **Entity**. So for this Book Table, the Primary Key is going to be a value that makes it so that first book in the first row isn't like any other book in the rest of the table (meaning it's attributes combined must be unique in the Book Table).

Primary Key Rules:
1. Unique
2. Never Changing
3. Never Null

You can't rely on `title` because two different book might share the same `title` hence breaking the rule of **Unique**. You also can't rely on `description` because a books description can change over time hence breaking the rule of **Never Changing**. So that leaves us with `book_id`. By design any sort of `id` is typically programmed to increment for each addition of the table. You can see how `book_id` satisfies all the rules for a **Primary Key**. **The Martian**'s `book_id` will completely identify it as a particular instance in our database and that value will never be repeated in this **Book Table** hence it's the **Primary Key**.

User Table:

<img width="361" alt="screen shot 2018-02-26 at 2 29 42 pm" src="https://user-images.githubusercontent.com/36538863/36652224-8a4d636e-1b01-11e8-9b11-5dba098b9164.png">

**Primary key** is an **attribute** (being the `user_id` in this case) that uniquely identifiers every record in that certain table. Since a single attribute can accomplish all that, it makes sense that you will have 1 **Primary Key** per an **Entity**. So for this **User Table**, the **Primary Key** is going to be a value that makes it so that first user in the first row isn't like any other user in the rest of the table (meaning it's attributes combined must be unique in the User Table).

Primary Key Rules:
1. Unique
2. Never Changing
3. Never Null

You can't rely on `email` because email addresses change like the season hence breaking the rule of **Never Changing**. So that leaves us with `user_id`. by design any sort of `id` is typically programmed to increment for each addition of the table. You can see how `user_id` satisfies all the rules for a **Primary Key**. **name@example.com**'s' `user_id` will completely identify it as a particular instance in our database and that value will never be repeated in this **User Table** hence it's the **Primary Key**.

What's the minimum amount of Users a Book might have? **1** (For this atleast because a book can only be cerated by one user)

What's the maximum amount of Users a Book might have? **1** For this atleast because a book can only be cerated by one user)

<img width="617" alt="screen shot 2018-02-26 at 3 30 59 pm" src="https://user-images.githubusercontent.com/36538863/36653573-1b620488-1b0a-11e8-9ee3-0f970a8b02b3.png">

What's the minimum amount of Books a User might have? **0**

What's the maximum amount of Books a User might have? **many**

<img width="616" alt="screen shot 2018-02-26 at 3 29 39 pm" src="https://user-images.githubusercontent.com/36538863/36653555-ea99c1ec-1b09-11e8-8870-c164f80a9162.png">

**Foreign Key** is the same as a **Primary Key** but just located in a foreign place. So maybe you have **Primary Key** in one entity but it will be helpful to pull that data into another entity, that's where you get a **Foreign Key**. And we want to make note of these **Foreign Keys** so we can make better understand how our entities relate to one another.

We've already established `user_id` as the **Primary Key** for the User entity. But that same attribute is also present in the Book entity, that's because for each Book we create we want to know exactly which User created that Book.

The Book entity is simply referencing the `user_id` from the User entity. That's what makes it a **Foreign Key**. We can further show this relationship on this diagram by adjusting this relation ship to line up with the **Primary Key** and **Foreign Key**.

<img width="613" alt="screen shot 2018-02-26 at 4 34 49 pm" src="https://user-images.githubusercontent.com/36538863/36654809-061f3ba0-1b13-11e8-9955-5c58b9d7ab38.png">

This reinforces the fact that this **Foreign Key** and the Book Entity is referencing the **Primary Key** of the User entity.

You can read out this diagram as:
* a **Book** has **one and only one** User. (Rails terminology `belongs_to :user`, `#<Book id: 13, user_id: "1"...>`)
* a **User** has **zero to many** Books. (Rails terminology `has_many :books`)

### Reference

What's the minimum amount of Orders a Customer might have? **0**

What's the maximum amount of Orders a Customer might have? **many**

<img width="476" alt="screen shot 2018-02-26 at 3 05 15 pm" src="https://user-images.githubusercontent.com/36538863/36653004-84f8979e-1b06-11e8-8007-95b16594cb9f.png">

Whats' the minimum amount of Customers a Order might have? **1**

What's the maximum amount of Customer a Order might have? **1**

<img width="475" alt="screen shot 2018-02-26 at 3 07 45 pm" src="https://user-images.githubusercontent.com/36538863/36653054-dbc1e684-1b06-11e8-8b99-8998732b3dd1.png">

What's the minimum amount of Product's an Order might have? **1**

What's the maximum amount of Product's an Order might have? **many**

<img width="509" alt="screen shot 2018-02-26 at 3 15 54 pm" src="https://user-images.githubusercontent.com/36538863/36653262-01068732-1b08-11e8-8b27-33301b8d7c0e.png">

What's the minimum amount of Order's a Product might have? **0**

What's the maximum amount of Order's a Product might have? **many**

<img width="510" alt="screen shot 2018-02-26 at 3 18 52 pm" src="https://user-images.githubusercontent.com/36538863/36653310-6682c24c-1b08-11e8-9e7f-e35efca957b1.png">

<img width="478" alt="screen shot 2018-02-26 at 3 11 02 pm" src="https://user-images.githubusercontent.com/36538863/36653129-532aea7c-1b07-11e8-89bf-15b929c7d47b.png">


### Stories

* As a **Visitor** I want to see Books index.
* As a **Visitor** I want to see Book show.
* As a **Visitor** I want to Sign Up devise.
* As a **User** I want to see Books index.
* As a **User** I want to Book new/Book create.
* As a **User** I want to Book edit/Book update.
* As a **User** I want to Book show.
* As a **User** I want to Book destroy.
* As a **User** I want to Login devise.

### Steps

1. [RVM gemset container](https://gist.github.com/JuliusRobertOppenheimer/c098915268af721d8e12bda9448d4e3d)
2. [RoR Heroku setup](https://gist.github.com/JuliusRobertOppenheimer/8c7513fda7237226dcfd3251b7e2d466)
3. [RoR Bootstrap 4 setup](https://gist.github.com/JuliusRobertOppenheimer/01055071590bf5bb931e1468e115cd43)
4. [Navbar](https://gist.github.com/JuliusRobertOppenheimer/6ee5f6330062e488fe7148811bd2b547)
5. [Book Entity independent attributes](https://gist.github.com/JuliusRobertOppenheimer/bfa0f01a3f6c3ab9d5e4fc0c380d14f4)
6. [Heroku create/push](https://gist.github.com/JuliusRobertOppenheimer/10d0885b821ce3e2ee7dd5264819cf2f)
7. [Book FriendlyId](https://gist.github.com/JuliusRobertOppenheimer/664c15ea2285b83dd846b261875a44bb)
8. [Heroku create/push second time](https://gist.github.com/JuliusRobertOppenheimer/fd38704482695ccdc50860a585ac46d2)
9. [Book seeds](https://gist.github.com/JuliusRobertOppenheimer/f26b772b9ae552c228d1de9f5ab61862)
10. [Book Will Paginate](https://gist.github.com/JuliusRobertOppenheimer/59357535b42e229fb3b35c35cfcec328)
11. [CarrierWave](https://gist.github.com/JuliusRobertOppenheimer/3a48cff0996e30adfa182c4ebc0b92f6)
12. [MiniMagick](https://gist.github.com/JuliusRobertOppenheimer/45ba2a8b68e05836e48cc3f2a11fc475)
13. [Book index clean up](https://gist.github.com/JuliusRobertOppenheimer/526078844dc42efd1fb48a0cc1571146)
14. [Book form clean up](https://gist.github.com/JuliusRobertOppenheimer/afe5a0dc087736cee201620ee6261aa9)
15. [Book show clean up](https://gist.github.com/JuliusRobertOppenheimer/8457c2828979b9823e3862489e924916)
16. [AWS S3 Heroku](https://gist.github.com/JuliusRobertOppenheimer/d4b4fef51fe32e8d957893eb9e889a62)
17. [DO Spaces Heroku](https://gist.github.com/JuliusRobertOppenheimer/1fa00bdf1945cf28d20a175b59a172f8)
18. [Deivse books](https://gist.github.com/JuliusRobertOppenheimer/71906b7450be807a028d95ca622371c4)
