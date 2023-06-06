# The Bitcoin Meetup in a Box #

Bitcoin Meetup in a Box (aka bmuiab) is tool to help plebs around the world get a web presence for their meetup fast.

It's a multi-language-enabled install of the Jekyll content management system that comes pre-loaded with bitcoin-centric content and that can readily easily be customized to suite your needs. It generates a 100% flat website that's compact and easy to host, so that all you have to worry about is content: no database, no server-side runtimes, just bring your own web server!

## 1. Prerequisites ##

To get your own instance of bmuiab started, simply fork this repo under the name of your choice, and clone that repo to your local computer. You'll also need Ruby and the Jekyll gem package installed to generate your site. Follow the [instructions on the Jekyll website](https://jekyllrb.com/docs/), or run the scripts in the [install scripts](/_install-scripts) folder.

## 2. Forking and cloning ##

One requirements are installed, you can clone this project or your fork it it. Be aware that since there are submodules involved, there are additional git commands to run.

Navigate to the cloned repo on your local computer, and run:

```
git submodule init
git submodule update
```

You will need to run `git submodule update` whenever upstream changes to submodules are made. 

## 3. Replace the content ##

Getting familiar with a "vanilla" installation of [Jekyll](http://jekyllrb.com) is probably a good idea, but may not be necessary.

The content of this website hinges on two sources of content:

1. The localization files found at the root of `/_i18n`, for example `/_i18n/fr.yml` which contain a series of variables that define base elements of the site, translated in the language of your choice.  
2. The per-language content found in `/_i18n/*LANG_CODE*`, for example  `/_i18n/fr/`, where the "regular" jekyll folder hierarchy is replicated.

*For simplicity's sake, all pages are show in their "raw" pre-render form in english.* Translations of pages within the localization folders should retain the name of the english page, as the translation plugin is dependant on this. For example, `about.md` should not b

## 3. Site elements and customization ##

Getting familiar with a "vanilla" installation of [Jekyll](http://jekyllrb.com) is probably a good idea, but may not be necessary.

The content of this website hinges on two sources of content:

1. The localization files found at the root of `/_i18n`, for example `/_i18n/fr.yml` which contain a series of variables that define base elements of the site, translated in the language of your choice.  
2. The per-language content found in `/_i18n/*LANG_CODE*`, for example  `/_i18n/fr/`, where the "regular" jekyll folder hierarchy is replicated.

*For simplicity's sake, all pages are show in their "raw" pre-render form in english.* Translations of pages within the localization folders should retain the name of the english page, as the translation plugin is dependant on this. For example, `about.md` should not b

All site elements which appear on more than one page are defined in the localization files. They are structure in a hierarchy which makes them more or less self-evident, but here there are on the page.

![Site elements identified](/_README-ASSETS/site-elements.png)

All the elements are dynamically generated with for loops, meaning that you can have as few of those elements as you like.  Simple add or delete a YAML element of the type you want more or less off, and fill in the fields as appropriate. If you enable multi-language sites, make sure that configurations match in all languages!

### 3.1 Navbar ###
Navigation links, usually used to link to internal pages, but can link anywhere you might want. They appear in the order in which they are defined. Takes the following sub-elements:

 * `title`: Text of the menu element
 * `link`: URL, absolute or relative

### 3.2 Carousel ###
The carousel needs at least one element defined, otherwise the theme will break. If you don't want the carousel, use the `no-carousel` layout. Takes the following sub-elements:

 * `image`: Filename of an image file in the `/img/slider/` folder.
 * `alt`: Alternative text; shows on hover-over in most browsers.
 * `title`: Whatever text or HTML you want to show on the uppermost line.
 * `body`: Whatever text or HTML you want to show on the lowermost line.

### 3.3 Contacts ###

Text only entries. You can add links by inserting HTML directly in your content. Takes the following sub-elements:

 * `title`: Text left of the colon.
 * `content`:  Text right of the colon.

 ### 3.4 Links, social ###

 They are the same, save for the fact that they are shown separately. Takes the following sub-elements:

  * `title`: Text of the menu element.
  * `url`: URL, absolute or relative.

### 3.4 Adding pages ###

Jekyll recognizes any HTML or markdown file NOT contained with a folder prefixed with `_` as a page. To add a new page, let's call it `New Page` at location `/newpage/`, we have to:

1. Create a new page at the root of the folder. We'll call it "newpage.md", but the name doesn't matter.
2. Add [frontmatter](https://jekyllrb.com/docs/front-matter/) to the new file, and the liquid express for translated content. Typically it will look like this:
```
---
layout: no-carousel
title: titles.newpage
permalink: /newpage/
permalink_fr: /nouvellepage/
---

{% translate_file newpage.md %}
```
Notice how a permalink for the french translated page has been provided, in addition to the usual layout and title. `titles.newpage`is a variable, and refers for a variable of the same name set in the localization file.
3. Add a title to your localization file. Add a key with the name of the page in the language of your choice, repeat this in every language file that you will use.
4. Add the translate content in the root of your localization folder. In our case, we would create `/_i18n/fr/newpage.md`. There should be no front matter on this page, only content.  

# 4. Running and hosting your site #

While in development, you can run you site by entering you're site's base directory, and running `jekyll serve`. It will be presented at [http://localhost:4000](http://localhost:4000)

To serve your site in production, simply run `jekyll build` to generate the latest version of your site, and copy the contents of the `/_site`to the webroot of whatever web server you like.

[Github Pages](https://pages.github.com) can also host your site for free.
