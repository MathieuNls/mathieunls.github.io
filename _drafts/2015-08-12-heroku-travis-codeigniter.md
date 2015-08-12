---
layout: post
title: Toolwatch : Heroku, Travis, Github
tags:
- toolwatch
- travis
- codeigniter
- heroku
---

{% include toolwatch_serie.html %}

At <a href="https://toolwatch.io">Toolwatch</a> we use a full fledged development environment based on different tools and technologies. In this post, I'll explain why we pick those and how to ingrate them smoothly.

#Github : Build software better, together.

In case you don't know, Github is the absolute web repository hosting service. It provides (for free !) a git-based distributed source code management, access control, bug tracking, feature requests, milsetone management, pull request and even the possibility to host a jekyll based website and a wiki for each of your project.

## Why we love it so much

Well... GIT ! With git comes branching, rebasing, merging, cherry-picking and much more. All these features will come handy in almost every programming session.

Also, the bug tracking, feature requests and milsetone management makes Github the perfect spot for technical and non-technical folks to exchange about the project and see where you at and what's going on.

<a href="https://twitter.com/MarcAime">@Marc</a>, the founder of toolwatch, will also tell you that the mobile website is so well-designed that he don't mind spending his daily four hours of commute on it.

## How to do it

* Go on <a href="https:https://github.com/">Github</a> and create an account.
* Go to your profile, then repository, then new, or simply browse to <a href="https://github.com/new">https://github.com/new</a> while logged.

<img src="/public/github-new-repo.png" alt="Github new rep"/>

* Give your repository a name and off you go !

### I start from scrash

If you start from scrash, the following will create a readme, add the readme modification for commit, commit the readme with the message "first commit" and push the whole thing on github.

{% highlight bash %}
cd MyAwesomeRepoFolder
echo "# myAwesomeRepo" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:MathieuNls/myAwesomeRepo.git
git push -u origin master
{% endhighlight %}

### I already have some code but it's not versionned with git

{% highlight bash %}
cd MyAwesomeRepoFolder
git init
git add .
git commit -m "first commit"
git remote add origin git@github.com:MathieuNls/myAwesomeRepo.git
git push -u origin master
{% endhighlight %}

### I already have some code and it's versionned with git

{% highlight bash %}
cd MyAwesomeRepoFolder
git remote add origin git@github.com:MathieuNls/myAwesomeRepo.git
git push -u origin master
{% endhighlight %}

## What Should I Be Careful About ?

In short: passwords, salt and API keys.

If you stay with the free plan (unlimited public repository) your code will be public, meaning every one can see it. I personally open-source as much as I can (see <a href="/projects/bumper">Bumper</a> for an example) bug I make sure that passwords and API key are not versionned in Github. Why ? Because, as <a href="http://www.devfactor.net/2014/12/30/2375-amazon-mistake/">Andrew Hoffman</a> you could've your repository scanned by a script looking for API key and end up with a $2375 bill in your inbox !

Passwords and salt for you database, for example, will be major security breach. If you do need an explanation about this <a href="http://security.stackexchange.com/users/27048/u2702">u2702</a> and <a href="http://security.stackexchange.com/users/3339/lucas-kauffman">Lucas Kauffman</a> are here for you on <a href="http://security.stackexchange.com/a/38480">stackexange</a>

#Heroku : Focus on the app.

<a href="https://heroku.com">Heroku</a> is one of the first cloud plateform as a service that has been created in '07 by ames Lindenbaum, Adam Wiggins and Orion Henry. To keep it simple, Heroku gives access to virtual machines based (called Dynos) on Debian that you can use to serve your code.

Currently (august 2015), Heroku supports Ruby, Java, Scala, Clojure, Python, PHP and Perl.

## Why we love it so much

## What Should I Be Careful About ?


#Bonus: Travis, Test and Deploy with Confidence

