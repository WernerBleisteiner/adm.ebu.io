# EBU ADM Website


## Overview

This repository hosts the [adm.ebu.io](https://adm.ebu.io/) website, which contains the EBU's ADM homepage, and other related pages including the ADM guidelines.

The site is generated using [MkDocs](http://www.mkdocs.org). The graphs within the document are generated with [graphviz](https://www.graphviz.org).

## How to Contribute to [adm.ebu.io](https://adm.ebu.io)

If you want to contribute or improve to the published version, you have to to apply general git workflows.

### 1. Get/fork the source

```
git clone git@git.ebu.io:as/ebu-adm-io.git
```

### 2. Install requirements

You should consider running [`venv`](https://docs.python.org/3/library/venv.html) or other virtual environments like [virtualenv](https://virtualenv.pypa.io/en/stable/) to install the respective python requirements:

```
pip install -r requirements.txt
```

Install graphviz

On Ubuntu, use
```
sudo apt install graphviz
```

On OSX with [homebrew](http://www.homebrew.sh) use
```
brew install graphviz
```

### 3. Create your lokal develop branch

We recommend to create local branches if you intend substantial contributions - i.e. one or more pages. 


### 4. Live preview during writing

Given you've followed the steps of 1., you can run a live preview while editing with

```
mkdocs serve
```
and then using the URL `127.0.0.1:8000/` in a browser.
Be aware of the notifications that will be shown in the terminal. They will inform you about errors or inconsistencies of the present structuring.

Continue editing until you consider your contribution ready for review.


### 5. Create a public version of your fork or make a local static build

You may apply Github CI to create a publicly visible preview of your forked repo. For details, [see here](https://github.com/squidfunk/mkdocs-material/blob/master/docs/publishing-your-site.md)

After having activated this, you need to

* push your 'dev-branch' into your 'main' branch
* after a little while for building and deploying (you will be notified on the proceeding of thos action), you will be able to see the result as a site on `https://yourGithubName.github.io/adm.ebu.io/`. 

Alternatively, you can build the site locally with

```
mkdocs build
```
in the project folder and then and host on your own web server by swapping it up.

If you have made any changes to or added some `dot` files, you should firt run
```
./convert_dot_graphs.sh
```
in the project folder.

For more information and options, please refer to the [mkdocs manual](http://www.mkdocs.org)

### 6. Create a Pull Request (PR) to the  source adm.ebu.io repo

Access [https://github.com/ebu/adm.ebu.io](https://github.com/ebu/adm.ebu.io) in a browser or via the Github app and select 'Compare & pull request'. Check and the open the PR

It is advisible to provide the link to the Github CI of your fork or self-hosted version (c.f. under 5.)

Further discussion will then take place within the respective Github thread.

When your contribution is 
eventually accepted, it will be pushed into 'main' and then an updated version of the website is automatically published withon a few minutes (don't forget to clean your browser's cache, you've accessed the main site meanwhile).

### 7. 'Sync' your fork and clean it up

It is advisable to apply the 'sync' function to your fork some time after completion. This will bring your 'main' branch in line with the source. You should also delete you development branch that was merged.




