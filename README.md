# Research-notes

This project contains my research notes based on a Tufte them Jekyll. I forked and modified the theme from [tufte-jekyll site](https://github.com/clayh53/tufte-jekyll). 

The complied site is: [minhuanli.github.io/notes/](https://minhuanli.github.io/notes/)

## Contributing

If you find typos, errors or you want to contribute to some of the notes, you can submit a pull request with your fixes via GitHub.

The notes are written in Markdown and are compiled into HTML using Jekyll. Please add your changes directly to the Markdown source code. This repo is configured without any extra Jekyll plugins so it can be compiled directly by GitHub Pages. Thus, any changes to the Markdown files will be automatically reflected in the live website.

To make any changes to this repo, first fork this repo. 

If you want to test your changes locally before pushing your changes to the `master` branch, you can run Jekyll locally on your own machine. In order to install Jekyll, you can follow the [instructions](https://minhuanli.github.io/2020/12/31/SetupJekylllocally/) I posted before  Then, do the following from the root of your cloned version of this repo:
1) Make whatever changes you want to the Markdown `.md` files.
2) `rm -r _site/`  # remove the existing compiled site
3) `jekyll serve`  # this creates a running server
4) Open your web browser to where the server is running and check the changes you made.
5) Once you are ok with the current format, commit and push your changes to the `master` branch, then run `rake` locally. This will move the complied contents to `gh-pages` branch and publish it. see [ref](https://github.com/clayh53/tufte-jekyll/issues/69) 

### Notes about writing math equations

- Start and end math equations with `$$` **for both inline and display equations**! To make a display equation, put one newline before the starting `$$` a newline after the ending `$$`.

- Avoid vertical bars `|` in any inline math equations (i.e., within a paragraph of text). Otherwise, the GitHub Markdown compiler interprets it as a table cell element (see GitHub Markdown spec [here](https://github.github.com/gfm/)). Instead, use one of `\mid`, `\vert`, `\lvert`, or `\rvert` instead. For double bar lines, write `\|` instead of `||`.
