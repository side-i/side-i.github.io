---
layout: post
title:  "Pico CTF: Irish-Name-Repo 1"
date:   2023-02-18 14:30:42 -05:00
tags: [poem]
---

![image](./Pico%20CTF%20Irish-Name-Repo%201%200d1f42efdd7c4318a4ec4bee152346b1/Untitled%201.png)

[https://jupiter.challenges.picoctf.org/problem/39720/](https://jupiter.challenges.picoctf.org/problem/39720/)

The first thing I see when I go to that link is some pictures of people with their names listed underneath. Our goal here is to find a way to log into the admin portal on the login.html page, so I began clicking around.

On the support page, I notice a question asked by a user.

![image](Pico%20CTF%20Irish-Name-Repo%201%200d1f42efdd7c4318a4ec4bee152346b1/Untitled%201.png)

Nice! So this user gets a SQL error when he enters the name “Conan O’Brien”. This has to be because the apostrophe. I know that in SQL, the single quote specifies the beginning/end of a string. Therefore, the SQL error tells me the query to the database is not escaping the apostrophe (or single quote) character, and I can use this to my advantage.

![image](Pico%20CTF%20Irish-Name-Repo%201%200d1f42efdd7c4318a4ec4bee152346b1/Untitled%202.png)

I notice that when try to log in with normal credentials, I get a login failed page. But, when I input a SQL query:

```sql
SELECT * FROM users WHERE name='admin'
```

The “Login Failed” page is bypassed and the website returns a black screen.

 However, I am not too familiar with SQL injection yet, so I have to do some research. I found a [SQL Injection Authentication Bypass Cheat](https://github.com/mrsuman2002/SQL-Injection-Authentication-Bypass-Cheat-Sheet/blob/master/SQL%20Injection%20Cheat%20Sheet.txt), but this still didn’t really help me.

At this point I was pretty lost. I remember from a couple weeks back my friend SquareZero did a [writeup on a PortSwigger SQLi Lab](https://squarezero.dev/Portswigger-Lab-SQL(UNION)/). 

In his writeup, he posts his solution to how to bypass a password in a login page by putting a single quote after the username, followed by a some dashes to comment out the password. 

![image](Pico%20CTF%20Irish-Name-Repo%201%200d1f42efdd7c4318a4ec4bee152346b1/Untitled%203.png)

![image](Pico%20CTF%20Irish-Name-Repo%201%200d1f42efdd7c4318a4ec4bee152346b1/Untitled%204.png)

Wow! On the first attempt it actually worked. Thanks for the help SquareZero!