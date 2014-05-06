---
title: Keeping Secrets Secret Using dotenv
date: 2014-05-06 10:06 UTC
---

This is a somewhat selfish blog post that I am writing so that I remember how to do this later because I had to re-learn
yesterday. So yesterday, we started with APIs. And we used the PivotalTracker API to pull
some of our project data from. At first (before I pushed my code to GitHub of course), I was just using my API token in the file where
my code was running. Then I vaguely remembered something about not leaving that stuff out in the open and vaguely
remembered something about .env files and a gem. So, I looked up the 'dotenv' gem docs, and went from there.
Dotenv keeps your environment variables and allows you to access them when you need them.

All you do is make a file named '.env' to hold your secret things, then list them like this in the '.env' file:
'TOKEN=your token number'. In the file where you want to use them, you put ENV['TOKEN'] in where you need the secret
information. Then, you need to require 'dotenv', and before you do any coding, just put 'Dotenv.load'.

To ignore your '.env' file when you are adding things to Git, you should make a new .gitignore file and put .env in there.
Then, Git will ignore it, and not tell you that it is un-staged all the time. It is as easy as that. Or at least it was for
that application. :-)