# EBU ADM Website


## Overview

This repository hosts the ["EBU ADM Website"](https://adm.ebu.io/), which contains the EBU's ADM homepage, and other
related pages including the ADM guidelines.

The Guidelines are generated using [MkDocs](http://www.mkdocs.org). The graphs within the document are generated with [graphviz](https://www.graphviz.org).

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

Given you've followed the steps of 1., you can run a live preview while editing running

```
mkdocs serve
```
and then using the URL `127.0.0./8000` in a browser.
Be aware of the notifucations that will be shown in the terminal. They will inform you about errors or inconsistencies of the present structuring.

Continue editing until you consider your contribution ready for review.

### 5. Create a public version of your fork or make a local static build

You may apply Github CI to create a publicly visible preview if your forked repo with the URL `https://yourGithubName/github.io/ebu.adm.io/`. For details, [see here](https://github.com/squidfunk/mkdocs-material/blob/master/docs/publishing-your-site.md)

Alternatively, you can build the site locally and host on your web server

```
mkdocs build
```
in the project folder.

If you have made any changes to or added some `dot` files run
```
./convert_dot_graphs.sh
```
in the project folder.

For more information and options, please refer to the [mkdocs manual](http://www.mkdocs.org)

### 6. Create a Pull Request (PR) to the main repo


