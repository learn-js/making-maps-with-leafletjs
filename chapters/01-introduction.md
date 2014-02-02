# Introduction

## Thank you.
I really appreciate the support you’ve given by purchasing this book.
I welcome you to help guide the direction of this book and the Learn.js series of javascript books. If there are particular libraries, development tools, or programming patterns that you'd like to see covered, please email me at [hi@learnjs.io](mailto:hi@learnjs.io).

The Learn.js series is highly inspired by the lean publishing model ([read more about it](https://leanpub.com/manifesto)) proposed by Peter Armstrong, founder of leanpub.com. It has proven successful as a way to receive feedback from you, the readers, so that together we can make the best book about javascript tools and libraries possible.

You’ll get updates about upcoming books in the series, and I’d love to hear your thoughts on what would be most useful.

## Tools we'll use in this book

Many of the tools used in this book are covered in detail in one of my other books, Development Environments for Beginners.

If you’re feeling like you could use more information about what a development environment is and how best to set one up, you can purchase the Development Environments book at [superbigtree.com/books/dev-envs](http://superbigtree.com/books/dev-envs).

If needed you can check out the Development Environments book on GitHub for free here: [github.com/sethvincent/dev-envs-book](http://github.com/sethvincent/dev-envs-book).

### Sublime text editor

Sublime is a popular text editor with versions for Mac, Windows, and Linux. 

You can download an evaluation copy for free, and pay for a license when you're ready.

In this book we'll be using version 2 of Sublime, in future updates to the book we'll switch to version 3.

### Install
Go to [sublimetext.com](http://www.sublimetext.com/) and click the download button.

### Terminal

You'll be using the terminal (or command-line) for many of the tutorials in this book. [The Terminal chapter in Development Environments for Beginners](https://github.com/sethvincent/dev-envs-book/blob/master/manuscript/terminal.md) will help you get started.

### Node.js

We'll be using node.js mostly to get at npm, node's bundled package manager.

We will also write modules in the style of node.js.

Our code written for the browser will utilize the node.js style of modules thanks to browserify, a tool for bundling node modules for the browser.

This means that we won’t cover the RequireJS/AMD toolset for javascript development, but will focus on node/CommonJS modules whenever possible.

You’ll learn more about this later in the book as we go into depth with using Leaflet.js alongside browserify.

### npm

npm is the package manager that comes bundled with node.js. Sometimes people call it the node package manager, but I prefer a term used by programmer Max Ogden: "node packaged modules". The idea is that we can store whatever modules we want on npm. Leaflet.js is an example.

In each chapter we'll explore npm a little more, and by the end of the book you'll have learned it pretty thoroughly.

### git

For many of the examples we'll use git as our version control software. If you're new to git, learn more about it in this [Git chapter of the Development Environments book](http://git-scm.com/book), the [Try Git interactive tutorial](http://try.github.io/), and the [Pro Git book that's available for free on the git website](http://git-scm.com/book).

### GitHub Pages

All of the examples we work through in the book can be hosted using GitHub Pages. I recommend that put each map you make while reading this book up on GitHub Pages. It'll be good practice if you're new to git and GitHub.

Learn more about GitHub pages in the [related chapter of the Development Environments book](https://github.com/sethvincent/dev-envs-book/blob/master/manuscript/github.md), and on [GitHub's Help section](https://help.github.com/categories/20/articles).

## Chapters

Here's the progress I've made so far on chapters. As you likely know, I'm releasing this book in pieces, a few chapters at a time, and you're essentially subscribed to those chapter releases. The upcoming chapter list is somewhat revisable. I'm particularly interested in hearing your thoughts on what chapters would be valuable to you. Email me at seth@superbigtree.com to let me know what types of Leaflet.js content you would find useful.

### Completed:
- The simplest possible map you can make
  - html file
  - Remote script and stylesheet files
  - A map with one marker
  - Put the map on GitHub Pages
- Getting started with Leaflet.js using node.js, npm, and browserify

### Started:

- Useful Leaflet.js plugins
  - Leaflet.markercluster
  - Leaflet.label
  - Leaflet.awesome-markers
  - Leaflet.TextPath
  - leaflet-hash
  - L.GeoSearch
  - Leaflet.draw
  - leaflet-search

### Upcoming:
- Data visualization styles you can use in your maps
- Customizing your maps
  - Map tiles
    - CloudMade
    - MapBox
    - Stamen
  - Markers
  - Controls
- Drawing shapes on maps
- Advanced layer types
- GeoJSON & Leaflet.js
  - TopoJSON
- Using remote data in your maps
  - Google Spreadsheet and Tabletop.js
  - Twitter
  - Instagram
  - LocalWiki
- Using D3.js with Leaflet.js
- Additional resources directory

Please feel free to suggest topics or chapters by emailing me at seth@superbigtree.com, 

## Who are you? Who am I? What is this?

### The book
This book is meant as an introductory text that will get people up to speed for building interactive maps with Leaflet.js.

This book is an introductory text. I aim for this book to be a conversational and low-barrier approach to learning javascript and Leaflet. Everything we work on in this book can be done with just a browser, a terminal, and a text editor.

### The reader
I expect that the ideal reader for this book is someone who likes exploring, imagining, and inventing for themselves. You might even have some experience with javascript already. And that’s OK, because practicing, and even repetition is an important part of learning.

### The author
I’m Seth Vincent. I write code, stories, and music. 

I’m an independent programmer, designer and writer that is passionate about news, publishing and civic technology – particularly as it applies to local issues.

I’m a co-organizer of [seattle.io](http://seattle.io), [Code for Seattle](http://codeforseattle.org/), and [SeattleWiki](http://seattlewiki.net/). 

In case you couldn’t tell, I currently live in Seattle, Washington.

I write books like the one you’re reading, and build things like [crtrdg.js, a toolkit for 2d games](http://crtrdg.github.io/) at [Super Big Tree](http://superbigtree.com/).

## Setting up a development environment
There’s a lot of wind-up to getting started programming. You should understand things like git, github, the terminal, and more.

Instead of baking that information into each book in the series, I created a book called Development Environments for Beginners that helps you set up a javascript development environment (as well as ruby and python, but you can skip those sections if needed).

From that book you’ll learn how to install node.js, work with version control and testing tools, best practices for automating tasks and other programming tips and tricks.

If you’re feeling like you could use more information about what a development environment is and how best to set one up, you can purchase the Development Environments book at [superbigtree.com/books/dev-envs](http://superbigtree.com/books/dev-envs).

If needed you can check out the Development Environments book on GitHub for free here: [github.com/sethvincent/dev-envs-book](http://github.com/sethvincent/dev-envs-book).

Though, if you’re feeling generous and able to purchase the book, that’ll get you pdf, epub, and mobi versions, as well as support my work.

