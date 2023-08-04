# This project

For this project, I wanted to build a simple site with [eleventy](https://www.11ty.dev/). I set myself two challenges:

- Avoid looking at my previous projects, or documentation as much as possible
- Build an MVP site as quickly as I could

I set myself these goals to focus on my fundamental knowledge of how 11ty sites fit together, and to keep focused only on the fundamentals of getting a site live.

## Set up

Setting up an eleventy site is pretty straightforward. In the terminal run:

`npm init -y`

The -y flag here saves the faff of giving the project a name, and choosing your specific settings for the npm installer.

Then run:

`npm i @11ty/eleventy`

I set up my base files quickly by running

```
touch index.html .eleventy.js style.css .gitignore
mkdir _includes
```

and initialised my repo to be tracked with Git using:

```
git init
git branch -m main
```

In my `.gitignore` I add the following:

```
_site
node_modules
```

and then add the following scripts to my `package.json`:

```json
    "dev": "npx eleventy --serve",
    "build": "npx eleventy",
```

## Rendering the homepage

Eleventy works with layouts stored in the `_includes` folder which can be referenced on different pages. For this site, I'll use one layout and only have one page. It's perhaps a bit of a convuluted example but the goal here was solidifying learning.

Within the `_includes` folder I add a base layout (`base.html`) which is populated with boilerplate HTML (using the ! Emmett abbreviation). Inside here, I'll add a header component (which would display on every page) and a simple base layout.

Inside the `<body>` we can add `{{content}}` which lets Eleventy know we want to render whatever content is on the page here.

In the `index.html` file in the root of the project, I'll add at the top:

```
---
layout: base.html
---
```

Which will render the page with the base layout mentioned above.

At this point, I made the decision to change this file type to Markdown. I realised that I wasn't really harnassing the power of Eleventy as a static site generator by using HTML for my root page. Eleventy allows me to write up pages in Markdown (which is definitely easier and quicker than in HTML) and it will render these as HTML.

## Connecting the CSS file

I could remember as much as that for the CSS we needed to have a `addPassthroughCopy` into the `.eleventy.js` file but not the exact syntax for how to do this.

I succumbed to having a look at some doc's and happily failing challenge 1 😅

The 11ty site has [good documentation](https://www.11ty.dev/docs/assets/) on how to add CSS files. I followed these steps but unfortunately hit an error.

In my console, I read:

`Refused to apply style from 'http://localhost:8080/style.css' because its MIME type ('text/html') is not a supported stylesheet MIME type, and strict MIME checking is enabled.`

and Googled this error. I recalled having faced it before in my previous project too. This error is usually a result of the filepath being incorrect for the reference to the CSS file.

I played around with a few different other ways of referencing the CSS file but none of these resovled the error. Filepaths seem to be my Achilles Heel – so simple but I rarely get them right first time.

A StackOverflow answer suggested to navigate to the CSS file in the browser and check whether some CSS shows up there. For me, it didn't which helped indicate that something else was going wrong here.

I took a closer look at my `eleventy.js` file, which included the following:

```js
module.exports = function (eleventyConfig) {
  eleventyConfig.addPassthroughCopy("style.css");
  eleventyConfig.addWatchTarget("style.css");
};
```

Some more head scratching later, I realised my error. I had missed out the `.` from the start of the file name. That's right, I had `eleventy.js` instead of `.eleventy.js`. A simple error, which threw off the site's functionality.

## Finishing up

I added the content to my `index.md` file and added some basic styling to the page (changing fonts, adding some padding to list items, and a little bit of colour). Admittedly the site looks very 1990s, but hey – it's an MVP.

[The initial site](./V1.jpg)

My final time, just over an hour.
