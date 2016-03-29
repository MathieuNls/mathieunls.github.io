---
layout: post
title: Toolwatch Deployment Process Github, Travis and Heroku
tags: [toolwatch, deployment, github, heroku, travis]
excerpt: How we integrated Github, Travis and Heroku at toolwatch for a fully automatized deployment process.
comments: true
---

At <a href="https://toolwatch.io">Toolwatch</a> we use a full fledged development environment based on different tools and technologies. Let's see how to integrate Github, Travis and Heroku for a fully automatized deployment process.

<!--more-->

#Github : Build software better, together.

In case you don't know, Github is the absolute web repository hosting service. It provides (for free !) a git-based distributed source code management, access control, bug tracking, feature requests, milestone management, pull request and even the possibility to host a <a href="http://jekyllrb.com/">jekyll</a> based website (<i>This blog takes advantage of that. Here's the <a href="repo">https://github.com/MathieuNls/mathieunls.github.io</a></i>) and a wiki for each of your project.

## Why we love it so much

Well... GIT ! With git comes <a href="http://git-scm.com/docs/gittutorial#_managing_branches">branching</a>, <a href="http://git-scm.com/docs/git-rebase">rebasing</a>, <a href="http://git-scm.com/docs/git-rebase">merging</a>, <a href="http://git-scm.com/docs/git-cherry-pick">cherry-picking</a> and much more. All these features will come handy in almost every programming session.

Also, the bug tracking, feature requests and milestone management makes Github the perfect spot for technical and non-technical folks to exchange about the project and see where you at and what's going on.

<a href="https://twitter.com/MarcAime">@Marc</a>, the founder of toolwatch, will also tell you that the mobile website is so well-designed that he don't mind spending his daily four hours of commute on it.

## How to do it

* Go on <a href="https:https://github.com/">Github</a> and create an account.
* Go to your profile, then repository, then new, or simply browse to <a href="https://github.com/new">https://github.com/new</a> while logged.

<img src="/images/github-new-repo.png" alt="Github new rep"/>

* Give your repository a name and off you go !

### I start from scratch

If you start from scratch, the following will create a readme, add the readme modification for commit, commit the readme with the message "first commit" and push the whole thing on github.

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

If you stay with the free plan (unlimited public repository) your code will be public, meaning every one can see it. I personally open-source as much as I can (see <a href="/projects/bumper">Bumper</a> for an example) but I make sure that passwords and API key are not versionned in Github. Why ? Because, as <a href="http://www.devfactor.net/2014/12/30/2375-amazon-mistake/">Andrew Hoffman</a>, you could've your repository scanned by a script looking for API key and end up with a $2375 bill in your inbox !

Passwords and salt for you database, for example, will be major security breach. If you do need an explanation about this <a href="http://security.stackexchange.com/users/27048/u2702">u2702</a> and <a href="http://security.stackexchange.com/users/3339/lucas-kauffman">Lucas Kauffman</a> are here for you on <a href="http://security.stackexchange.com/a/38480">stackexange</a>

## What's missing ?

Hear me here, the project management capabilities of Github are good, very good : issues, features, tags, developer assignation, comments on code and request both. The only thing that I would like to see in Github is a time tracking engine very much like <a href="http://www.redmine.org/">redmine</a>. I am using a combination of tools, mainly zappier and toggle, to track the time I spent on things in order to improve myself. Consequently, I wish I could have these data directly in Github, associated with the issues.

#Heroku : Focus on the app.

<a href="https://heroku.com">Heroku</a> is one of the first cloud platform as a service that has been created in '07 by James Lindenbaum, Adam Wiggins and Orion Henry. To keep it simple, Heroku gives access to virtual machines based (called Dynos) on Debian that you can use to serve your code.

Currently (august 2015), Heroku supports Ruby, Java, Scala, Clojure, Python, PHP and Perl.

## Why we love it so much

In one word : Simplicity.

With Heroku, we can deploy, in matter of seconds our github repository and make it accessible for our users. Moreover, Heroku is a cloud platform, so we can, on the fly, throw more virtual machines to increase our processing capacity. Last but not least, heroku proposes hundreds of third party add-ons. Some handy examples includes <a href="https://elements.heroku.com/addons/cleardb">databases as a service</a>, <a href="https://elements.heroku.com/addons/algoliasearch">search engines</a> or <a href="https://elements.heroku.com/addons/fastly">caching mechanisms</a>.

## How to do it

* Go on <a href="https://www.heroku.com/">heroku</a> and create an account.
* Then login. You'll be redirected to your dashboard. The dashboard is where you can manage your different projects and virtual machines.
* Click on the big plus on the top right or go to <a href="https://dashboard.heroku.com/new">https://dashboard.heroku.com/new</a> to create your first heroku app.

<img src="/images/heroku-new-account.png" alt="Heroku new app"/>

* Choose where you want your app to be host.
* Go in the deploy tab, then Github and connect to your Github repository.

<img src="/images/heroku-github.png" alt="Connect Heroku to Github"/>

<p class="message">
Wait, what ?! Heroku provides a git repository and you didn't use it ? We could use it, and we did for a while, but then, we do not leverage what's makes Github awesome: the project management.
</p>

* You can also enable automatic deploy in order to have each commit pushed in github pull by heroku and delivered to your users automatically.

<img src="/images/heroku-auto-deploy.png" alt="Heroku autodeploy"/>

* Then, we have to tell heroku what's our app is all about. Create a file named composer.json at the root of your project containing the following for a php project.

{% highlight json %}
{
    "require" : {
        "php": "~5.6.5",
        "ext-mysql": "*",
        "monolog/monolog": "~1.7"
  },
  "require-dev": {
      "heroku/heroku-buildpack-php": "*",
      "mikey179/vfsStream": "1.1.*"
  }
}
{% endhighlight %}

<p class="message">
Go <a href="https://devcenter.heroku.com/articles/php-support">here</a> for a full-blown tutorial about that.
</p>

* Earlier, I told you it was dangerous to put your passwords and API keys in Github. Either you store them in a file that won't ever be versionned and you upload that file through the heroku <a href="https://toolbelt.heroku.com/">toolbet</a> OR your use heroku capacity to create environment variables. To do so, go to the setting tab and click on reveal variables environment, then the green +. Finally, add your key name and value.

<img src="/images/heroku-env-variables.png"/>

* Finally, you can retrieve them in your code. As example, here what you can do for database connection in php.

{% highlight php %}
//With an environment variable named DB_URL
//which have mysql://user:password@host/db-name as value
$url = parse_url(getenv("DB_URL"));
$db['default']['hostname'] = $url["host"];
$db['default']['username'] = $url["user"];
$db['default']['password'] = $url["pass"];
$db['default']['database'] = substr($url["path"], 1);
{% endhighlight %}


## What Should I Be Careful About ?

Automatic deploys are a beautiful yet dangerous thing. Indeed, each one of your commit will be <i>live</i> automatically seconds after you push them. Sure, you should only push bug-free and complete commit, but what if ? What if you do introduce a new bug ? Well, that's the subject of the next tool we use at toolwatch: Travis.

#Travis, Test and Deploy with Confidence

Travis is an online continuous integration tool. Simply put, it will automatically run your unit tests (that you already wrote, right ?!) and provide you a report. If your tests are all green, your code will be deployed on heroku. Otherwise, you'll be notified that something went wrong and you can check which test failed and fix what you broke.

## Why we love it so much

Once again, simplicity. With the Github login, all your repositories are instantly accessible and testable. Moreover, the fact that heroku can wait for test to pass in order to deploy is a really awesome fail safe in our deployment process.

## How to do it

* Go to <a href="https://travis-ci.org/">https://travis-ci.org/</a> and click on <i>Sign in with Github</i>.

<img src="/images/travis-new-account.png"/>

* Open your profile and activate your repository.

<img src="/images/travis-new-repo.png"/>

* Click on the wheel right besides your repository's name to access the setting.
* Activate the <i>Build only if .travis.yml is present</i> option.
* You can also add environment variables for your tests.

<img src="/images/travis-new-repo-config.png"/>

* Add a file named <i>.travis.yml</i> and create your test configuration. For testing a php application with php 5.6 and 5.5 and be notified by email, you could write the following:

{% highlight xml %}
language: php
php:
  - 5.6
  - 5.5

notifications:
  email: true

script: cd application/tests/ && phpunit --coverage-text
{% endhighlight %}

<p class="message">
The <i>script</i> attribute tells travis where and what to execute in order to run your tests. You can find all the possible options for the <i>.travis.yml</i> file <a href="http://docs.travis-ci.com/user/customizing-the-build/">here</a>.
</p>

* In heroku, activate the <i>Wait for CI to pass before deploy</i> option.

## What Should I Be Careful About ?

As Edsger W. Dijkstra wrote in <i>Software Engineering Techniques, April 1970, p. 16. Report on a conference sponsored by the NATO Science Committee, Rome, Italy, 27–31 October 1969.</i> : <b>Testing shows the presence, not the absence of bugs</b>. What does it means ? Well, the efficiency of your tests depends of your efficiency to write good tests. If you only write trivial tests, they'll never fail and they won't show the presence of any bugs. Consequently, you have to challenge yourself when writing test in order to imagine all probable possibilities. Even then, it's impossible to test each on every possibility by hand, you'll have to turn on formal methods to do that.

# Summary

In this entry, I described the deployment process we adopted at toolwatch. First, the source code is versioned on Github and Travis runs the unit test we wrote automatically for each and every commit. If all goes well, Heroku kicks in and pull your commit from Github in order to deploy your modification to your users.
