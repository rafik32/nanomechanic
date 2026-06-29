# RPI Computational Nanomechanics group website
This git repository houses the website for professor Picu's lab group. The previous versions of the web page can be found in website_archive.zip which has been kept for archival purposes. All future versions of the site should probably use version control to track the history more effectively.

# Installation
This site uses a static site generator Jekyll to make writing the content simpler and less error prone. This allows us to write the majority of the content in markdown (with the exception of images and mathematics).

To use the site install a copy of [ruby](https://www.ruby-lang.org) and [bundler](http://bundler.io/). Now get the websites files and install the needed ruby gems.

```bash
git clone git@gitlab.com:jacob.merson/nanomechanics.git
cd nanomechanics
bundle install
```

Now you should see the required software install.

# Testing the site locally
It's very important to see if the changes you are making to the site are going to turn out correct on the web.

When testing the site locally you can run

```bash
bundle exec jekyll serve -b /nanomechanics/ --incremental
```

Now in your browser go to `http://localhost:4000/nanomechanics/`. The homepage should load and you should be able to verify your changes. You can leave this running and edit files. After any change just save the text and reload the web browser.

# Writing pages

## Front Matter
The information at the top of the page between the three dashes is called front matter. For now an in depth explanation is not provided here, see the existing pages for examples of how to use this. Note that the front matter is only important if it is used by the layout.

## Basic writing
Basic text files are written in markdown. See [here](http://daringfireball.net/projects/markdown/syntax) for syntax details. Beyond basic syntax tables are also enabled. See [here](https://help.github.com/articles/organizing-information-with-tables/) for examples.

## Math
If math is inside of a section of writing that is markdown than it must be enclosed in a code block. This is done by surrounding the equation in back ticks (\`). Inside of the back ticks you must also surround your equation in `\(` `\)` for inline math, or `\[` `\]` for equations that should be centered and on a new row.

In a raw HTML block e.g. a figure caption the back ticks are not needed.

## Citations
To cite an author use {% cite cite_key %}. More info can be found here. The citation key can be found in the main [bibtex file](./_bibliography/Nanomechanics\ \(Group Website\).bib) in the [_bibliography](./_bibliography/). More info can be found here.



# Helpful hints
## Image conversion
If images are tiffs or some weird windows format convert them to pngs...use the convert tool which is available on Linux:

```bash
convert file.tif file.png
```

## Spell checking markdown files
Note you can write markdown files in word or libre office, and use that spell checker, just make sure to not save it as a `.docx`. I typically edit files in gedit or vim or notepad++. If this is the case you can use the handy tool aspell to check your spelling:

```
aspell --sug-mode=bad-spellers file1.mkd
```

## File Conversion
It is possible to convert word files to markdown with a tool called [pandoc](http://pandoc.org/). It won't work perfectly and you will likely need to fix things by hand, particularly the figures and citations.

# Notes for the current site maintainer

## Pushing a new update to the website
After updating a page the easiest way to push the updates to the web is with rsync... This is like scp, but it will be much faster because it will only copy files that have been changed since the last update.

```bash
bundle exec jekyll build
rsync -a _site/ jumpgate.scorec.rpi.edu:/net/web/scorec/nanomechanics
```

The `-a` tells rsync to do a recursive copy.

## Updating the package dependencies
To update the packages in the project run:

```
bundle update
```

This should appropriately update the [Gemfile.lock](./Gemfile.lock) file.
