# Core-Mechanics.github.io

## What is this?

This repository stores the code (and data) backing a collection of tools to help organise the Core Mechanics effors in the blaseball elections. Check out https://www.blaseball.com/ if none of that means anything to you (and when you do, make sure to join the Mechanics. We're great, I promise)!

Right now, those tools include:
 - A page summarising our thoughts on different election options
 - A calculator to make dividing up votes between options easy
 - Links to various useful resources

## How to help out

### Getting started

The easiest place to start out is by editing the file [options.yml](https://github.com/Core-Mechanics/Core-Mechanics.github.io/blob/main/_data/options.yml). This file contains the data on the voting options on offer in the current season. Each option has the following properties:
  - **name**: Hopefully self-explanatory
  - **weight**: The weighting we're giving to this option when dividing up votes. For example, if Option A has weight 3 and Option B has weight 2, Option A will be allocated 60% of the votes.
  - **value**: How good we think the option is. A 0 marks the option as 'under evaluation', 1 is actively harmful, 2 is neutral, and 3, 4 and 5 are increasing degrees of beneficial.
  - **chance**: Only used for Blessings. This is how likely we think we are to be able to win the Blessing, on a scale of 1 to 3.
  - **type**: What type of option this is. Right now, this will usually be 'Will' or 'Blessing'.
  - **review**: A short text summary of _why_ we given the option this score.

When you're happy with the edit, scroll to the bottom and add a short description of you changes. Then select 'Create a new branch for this commit' and click 'Propose Changes'. Somebody will come along and review your changes for typos etc., then if all's well the changes will be put live.

### Editing the code on your own machine

If you want to make more complex changes (especially changes that effect multiple files at once), you'll probably need a local copy of the code on your own machine. The code is shared using a program called **git**. Unless you know all this already, you probably don't want to start off using git directly - it was designed by and for Linux kernel developers, and consequently has one of the worst user interfaces in the history of software development. A good starting point is the [Github desktop client](https://desktop.github.com/), made by the website that hosts this code. It's a lot less powerful than using git directly, but you really don't need a chainsaw to butter a slice of toast.

The desktop tool uses the same workflow as editing the code from this site, but requires a few more manual steps. Git tracks this code as a number of 'branches', each of which is made up of 'commits' (individual records of a change to the code). When you make changes, you create a new branch with commits for your changes on it, then open a 'pull request' to merge those changes into the main branch. Once the changes reach the main branch, GitHub will automatically publish them to the website.

To start with you'll need to creat a local copy of the code (known in git as a 'repository'). Select 'clone a repository from the internet', then paste `https://github.com/Core-Mechanics/Core-Mechanics.github.io.git` into the "URL" tab. This creates a local copy of the code on your machine, which you can freely edit before sending it back up to the GitHub website. Then, use the 'Current branch' section to create a new branch for your changes. At this point, you're ready to start developing. Use whatever tool you prefer to make your changes to the files on yout machine (I like [Visual Studio Code](https://code.visualstudio.com/), but any text editor will do).

Once you're done, it's time to create a commit. Select some files, write a short description for you commit and then hit the 'Commit' button in the bottom left. That will create a new commit on your local machine, but won't yet share it with the wider world. To do that, you need to hit the 'Publish' button, sending your changes off to GitHub. Finally, after doing that you can hit 'Create Pull Request', which will request that your changes be merged into the main branch (after which they are automatically published to the website).

### How does this all work?

If you know a little about programming, you may be surprised to be editing the data for the site directly in the code, rather than storing it separately in a database. This is because this site is created using **Jekyll**, which is what's known a static site generator. The idea is that Jekyll does all the wiring up of data to web pages up-front, and the actual content published to the internet is just static files (as opposed to a more traditional website, where the web server dynamically populates the content of the page based on data from a database).

Jekyll does this using three key technologies:
 - **YAML** files contain the data to be published on the site in a (fairly) human-readable format. Thes have a .yml extension.
 - **Liquid** tags are a templating language, used by jekyll to insert data from these YAML files into other pages, typically .html files (more on those later). `{{ }}` tags display data on the page, while `{% %}` contain logic like if statements and loops - for example, we use these to loop over all the different options and display them on one page.
 - **SCSS** files are based on CSS files (see below), but have a more powerful language that allow us do things like reuse colour definitions. Jekyll automatically converts these into the CSS files that are understood by web browsers.

The static files that are then served up come in three kinds:
 - **HTML** files (.html) are the basic layout of a website. These are made up of tags, each of which defines a part of the page. Tags can be nested inside one another, creating a hierarchical structure.
 - **CSS** files (.css) desribe how the page should look. This is done using css classes, which could refer to a type of element (e.g. `table { background: red }` gives a ll tables a red background, or a "css class" defined in the HTML (e.g. `.voting-indicator { background: blue }` gives any element marked with `class=voting-indicator` a blue background.
 - **Javascript** files (.js) define code that can be run in the user's browser. We use for the voting calculator, where we need to update the values displayed in the tabled based on the number of votes typed in by the user.
