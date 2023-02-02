---
layout: post
title:  "Creating a website with Jekyll and Github Pages"
date:   2023-01-27 11:40:40 -0500
categories: jekyll update
---
In this post I'll walk through the steps necessary to create and host a website created with Jekyll on Github pages. I'll be doing this on Windows 11 that has the Windows Subsystem for Linux (WSL) installed.

# Requirements:
- Windows 11 with Ubuntu installed as a subsystem
- Gitub repo
- Jekyll:
	- Ruby
	- Bundler

# Ruby, Bundler, and Jekyll installation on Ubuntu for Windows:
I'll be following the steps in [Ruby's website][ruby-setup]: 

First we install rbenv, a manager for ruby installations, and then ruby
{% highlight bash %}
sudo apt-get update

sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev

cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL

rbenv install 3.2.0
rbenv global 3.2.0
{% endhighlight %}

Check the version of ruby installed and add the executable to the PATH
{% highlight bash %}
ruby -v
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~./bashrc
{% endhighlight %}

Finally we install Bundler and Jekyll
{% highlight bash %}
gem install bundler
gem update --system 3.4.5
rbenv rehash
gem install jekyll
{% endhighlight %}


# Create a new repository:
Follow the steps from [Github's tutorial][ghpages-setup]. Roughly the following: 

- Go to Github
- Create a new repo and name it <user>.github.io
- Clone repo in your local machine by git clone <repo-url>

# Creating the site:

In the main directory of your repo do:

{% highlight bash %}
jekyll new --skip-bundle .
{% endhighlight %}

Then:
- Comment out the jekyll gem in Gemfile
- Add the github-pages gem in the Gemfile like this:
gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
replacing the version with the one listed [here][ghpages-version] 

Then do:

{% highlight bash %}
bundle install
{% endhighlight %}

# Note about testing your site locally
The steps above install the latest version of ruby. However, as of today, testing the site locally with that version of ruby isn't working. Therefore, we need to bump the ruby version down to test our site locally. For this do:

Check which versions are available to install
{% highlight bash %}
rbenv install -l
{% endhighlight %}

{% highlight bash %}
For me it was 2.7.7, install it
{% endhighlight %}

{% highlight bash %}
rbenv install 2.7.7
rbenv global 2.7.7
{% endhighlight %}


Then you're good to go to test your site locally once you build it

# Test your site locally

In the main repository run:

{% highlight bash %}
bundle exec jekyll serve
{% endhighlight %}

and follow instructions to go to your website. The output of this command contains the url where the website is served.

[ruby-setup]: https://gorails.com/setup/windows/11
[ghpages-setup]: https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=linux
[ghpages-version]: https://pages.github.com/versions
