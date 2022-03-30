# OSPO website

This is the website for eBay's OSPO. This is written with [hugo](https://gohugo.io).


## Setup

We use `hugo` to compile the website. Install it with `brew install hugo`.

This repository has a self-link to the `public` folder for the `gh-pages` branch
of the repo. This is a bit of an odd setup, but github pages wants us to have a
dedicated branch to the compiled output. Hugo wants to stick compiled output
into the `public` folder.


Here's an example workflow.
```
git clone ..repo-info-here..
git submodule init

# make your edits

hugo serve # launches a webserver so you can see your changes


# when you're happy
hugo  # compiles out the edits into the `public` folder.
git commit -am "made my edits"
cd public
git commit -am "Update to compiled output"
```
