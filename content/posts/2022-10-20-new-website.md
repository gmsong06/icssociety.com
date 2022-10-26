+++
title = "New Website"
description = ""
tags = [
    "website",
    "hugo",
]
date = "2022-10-20"
categories = [
    "hugo",
    "icssociety.com",
]
menu = "main"
+++

## Step 1. Checkout this website

Go to [github](https://github.com/zvzvzvzv/icssociety.com) to checkout and modify this website

We are using this version of hugo and the hugo-book theme:

* hugo v0.104.3-58b824581360148f2d91f5cc83f69bd22c1aa331+extended
* [hugo-book 6090fddebd](https://github.com/alex-shpak/hugo-book/tree/6090fddebdf7272995c9cef36edf0cff61e261b9)

You can find more about how to install hugo [here](https://gohugo.io/getting-started/installing/)

## Step 2. Build the Docs

Follow the following steps:
```bash
# install hugo
# pick a folder you want to work in, and then:

git clone https://github.com/zvzvzvzv/icssociety.com
cd icssociety.com
hugo server --minify --theme hugo-book --disableFastRender

# now you can edit files in icssociety.com/content/
# see your changes live at http://localhost:1313

# press ctrl-c to kill the hugo server
# run hugo to check that everything compiles:
hugo
```

## Step 3. Create a pull request

Make a branch, make some changes, and make a pull request
