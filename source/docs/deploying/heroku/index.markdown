---
layout: page
title: "Using Octopress with Heroku"
date: 2011-09-10 17:58
sidebar: false
footer: false
---

If you don't already have a Heroku account, [create one](https://api.heroku.com/signup), it's free. Then install the Heroku gem.

## Basic Octopress setup

First make sure you've installed the Heroku gem.

```sh
gem install heroku
```

Next create a heroku app for deployment. If this is your first time using the `heroku` gem, this command will ask for your account credentials.  If you don't already have a public key follow [Github's guide and create one](http://help.github.com/set-up-git-redirect/).  Then run the command:

```sh
heroku keys:add
```

to upload your public SSH key to Heroku.

Now type:

```sh
heroku create
```

This will create a new Heroku app for you to deploy to.

The `heroku create` command will ask you for your credentials and print an output similar to the following:

```
Creating cool-name-9999... done, stack is cedar
http://cool-name-9999.herokuapp.com/ | git@heroku.com:cool-name-9999.git
```

Take the URL for the git repository this command has given you and use it to add a remote to your local Octopress repository like so:

```sh
git remote add heroku git@heroku.com:cool-name-9999.git
```

Run the following command to set heroku as the default remote for push and fetch operations:

```sh
git config branch.master.remote heroku
```

Edit the `.gitignore` in the root of your repository and remove `public`. This will let you add generated content for deploying it to Heroku.

```sh
rake generate
git add .
git commit -m 'site updated'
git push heroku master
```

That's it, you just deployed to Heroku. If you want to set up a custom domain check out the [docs at Heroku](http://devcenter.heroku.com/articles/custom-domains).