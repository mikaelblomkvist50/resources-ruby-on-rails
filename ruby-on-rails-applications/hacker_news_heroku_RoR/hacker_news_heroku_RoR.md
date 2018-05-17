https://hacker-news-heroku-ror.herokuapp.com/

![hacker_news_heroku_ror](https://user-images.githubusercontent.com/36538863/37075428-ddfb1530-2225-11e8-9eaf-5f8bdd436c99.png)

### You can read out this diagram as:
* a User has **zero to many** Links. (Rails terminology `has_many :links`)
* a User has **zero to many** Comments. (Rails terminology `has_many :comments`)
* a Link has **one and only one** User. (Rails terminology `belongs_to :user`)
* a Comment has **one and only one** User. (Rails terminology `belongs_to :user`)
* a Link has **zero to many** Comments. (Rails terminology `has_many :comments`)
* a Comment has **one and only one** Link. (Rails terminology `belongs_to :link`)

### Breaking it down further to ERD cardinality:

What's the minimum amount of **Links** a **User** might have? **0**<br/>
What's the maximum amount of **Links** a **User** might have? **many**<br/>
**0** + **many** = **zero to many**<br/>
Hence a **User** has **zero to many Links**.

---

What's the minimum amount of **Comments** a **User** might have? **0**<br/>
What's the maximum amount of **Comments** a **User** might have? **many**<br/>
**0** + **many** = **zero to many**<br/>
Hence a **User** has **zero to many Comments**.

---

What's the minimum amount of **Users** a **Link** might have? **1**<br/>
What's the maximum amount of **Users** a **Link** might have? **1**<br/>
**1** + **1** = **one and only one**<br/>
Hence a **Link** has **one and only one User** .

---
What's the minimum amount of **Users** a **Comment** might have? **1**<br/>
What's the maximum amount of **Users** a **Comment** might have? **1**<br/>
**1** + **1** = **one and only one**<br/>
Hence a **Comment** has **one and only one User**.

---
What's the minimum amount of **Comments** a **Link** might have? **0**<br/>
What's the maximum amount of **Comments** a **Link** might have? **many**<br/>
**0** + **many** = **zero to many**<br/>
Hence a **Link** has **zero to many Comments**.

---
What's the minimum amount of **Links** a **Comment** might have? **1**<br/>
What's the maximum amount of **Links** a **Comment** might have? **1**<br/>
**1** + **1** = **one and only one**<br/>
Hence a **Comment** has **one and only one Link**.

### Site Map

![site-map](https://user-images.githubusercontent.com/36538863/37131056-b31a362e-22da-11e8-8bac-a0b773140d9e.png)

### Navbar

![navbar](https://user-images.githubusercontent.com/36538863/37131466-a2212dbc-22dc-11e8-9132-339e21f3fe4e.png)

### Steps

1. [RVM gemset container](https://gist.github.com/JuliusRobertOppenheimer/c098915268af721d8e12bda9448d4e3d)
2. [RoR Heroku setup](https://gist.github.com/JuliusRobertOppenheimer/8c7513fda7237226dcfd3251b7e2d466)
3. [RoR Bootstrap 4 setup](https://gist.github.com/JuliusRobertOppenheimer/01055071590bf5bb931e1468e115cd43)
4. [Navbar](https://gist.github.com/JuliusRobertOppenheimer/6ee5f6330062e488fe7148811bd2b547)
5. [Link Entity independent attributes](https://gist.github.com/JuliusRobertOppenheimer/884b16d46c8822a7562a52d0fc50ae42)
6. [Heroku create/push](https://gist.github.com/JuliusRobertOppenheimer/10d0885b821ce3e2ee7dd5264819cf2f)
7. [Link FriendlyId](https://gist.github.com/JuliusRobertOppenheimer/532c75f50ef3b349dda8a866d97c1350)
8. [Heroku create/push second time](https://gist.github.com/JuliusRobertOppenheimer/fd38704482695ccdc50860a585ac46d2)
9. [Devise links](https://gist.github.com/JuliusRobertOppenheimer/ca0a3fd6ee2625ac63f969d30b7b9df3)
10. [Users Links Seeds Hirb](https://gist.github.com/JuliusRobertOppenheimer/acd1be0de4f6b3380bd6ea1b88a308c2)
11. [Link index clean up](https://gist.github.com/JuliusRobertOppenheimer/8b94979deef62cb32dc9ca840a4f8078)
12. [Link show clean up](https://gist.github.com/JuliusRobertOppenheimer/3ee95974eb92aee73bc284d2831be966)
13. [Link form clean up](https://gist.github.com/JuliusRobertOppenheimer/5e04a78daf2b38e510dbd61d90833878)
14. [Act as votable link](https://gist.github.com/JuliusRobertOppenheimer/e020e1513f9a04f5877e5467e9433211)
15. [Comment entity independent attributes and dependent attributes](https://gist.github.com/JuliusRobertOppenheimer/0683e63e558f56a0e7c5971cd22bf6a6)
