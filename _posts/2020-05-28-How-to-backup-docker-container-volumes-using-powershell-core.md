---
layout: post
comments: true
category: code
tags: [docker,powershell,linux,windows]
summary: Learn how to convert a `Markdown` file to a PDF by using a single `Docker` command. No need to install any other software except Docker. This will work on both `Windows` and `Linux` and could easily work with GitHub actions.
---

# How to convert Markdown to PDF with Pandoc and Docker

Using a docker container to convert your files, means you don't have to install Pandoc or any other libraries.

## Requirements

* Docker Desktop

## Instructions

From the directory where your markdown file is, run the following command:

### Powershell
  ``` bash
  docker run -v "$((pwd).Path):/data" pandoc/latex pandoc README.md --pdf-engine=xelatex -o example13.pdf
  ```

### Bash *un-tested syntax
  ``` bash
  docker run -v "`pwd`":/data pandoc/latex pandoc README.md --pdf-engine=xelatex -o example13.pdf
  ```

