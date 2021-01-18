---
layout: page
title: .richmediarc
---

## .richmediarc features

Below is a list of features found as part of the [.richmediarc](./richmediarc.md) format

- [File paths are always relative](#file-paths-are-always-relative).
- [Content node](content-node). Everything in this node will be added and parsed by webpack.
- [Using .richmediarc values in HTML](#using-richmediarc-values-in-html). Everything you put in the `.richmediarc` is accessible in html.  
- [Using .richmediarc values in CSS](#using-richmediarc-values-in-css). Everything you put in the `.richmediarc` is accessible in css.
- [Using .richmediarc values in javascript](#using-richmediarc-values-in-javascript). Everything you put in the `.richmediarc` is accessible in JavaScript.  
- [Inheritance](#inheritance). `.richmediarc` can inherit from other .richmediarc files.
- [Feeds](#feeds). Linking dynamic data feeds via Google sheets to `.richmediarc`.

## File paths are always relative.
File paths defined in the .richmediarc are ALWAYS relative to the .richmediarc it self.

## Content node

So everything in this node will be added and parsed by webpack. So lets look at how a default .richmediarc looks like.

```json
{
  "settings": {
    "entry": {
      "js": "./script/main.js", // required: points to the starting js file.
      "html": "./index.html" // required: points to the main html file.
    },
    "size": {
      "width": 300, // required: width of richmedia unit
      "height": 600 // required: height of richmedia unit
    }
  },
  "content": {  // not required: can put anything in here.
    "bgcolor": "#FF0000", 
    "logo": "./img/logo.png" // not required: will be picked up by webpack and png minified.
  }
}
```

So if you want to load this file later you can do this like this.

```JavaScript
// you load the config like this. Why? because when accessing the config like this you 
// will get the parsed version of the config and not just the json file. 
import config from "richmediaconfig";

img.src = config.content.logo;
img.onload = () => {
    document.body.appendChild(img);
}
```

The .richmediarc file is one of the files that gets generated when you start a new project.

You can find it in the root directory of your creative, i.e. /src/300x250.

> **_Important:_** Each creative requires at least one .richmediarc file

In a freshly generated project, the .richmediarc will look something like this

```
{  
  "settings": {  
    "type": "plain",  
    "entry": {  
      "js": "./script/main.js",  
      "html": "./index.html"  
    },  
    "size": {  
      "width": 300,  
      "height": 250  
    }  
  },  
  "content": {  
    "text": "Welcome to this Banner!",  
    "cta": "Click here",  
    "bgcolor": "#FF0000"  
  }  
}
```
As you can see this file contains configuration settings for your creative, as well as key-value pairs which you can use for content, styling or even functionality.

Size and height should already be set to the correct values based on the selection made during the generator process.

This file is parsed when you run “npm run dev”. Webpack grabs the values from this file and hardcodes them into the compiled creative which you see in the preview.

It’s possible to make changes to this file while the preview [server](./running-building-uploading.md) is running.

> **_Note:_** In older versions of generator-richmedia-temple changes made to the .richmediarc file require stopping 
> and restarting the dev server**                               

Go ahead and change content.bgcolor to something else and save the file. In the terminal, you’ll see the creative getting recompiled. Once done, you can refresh the preview page and see the changes you made reflected in the preview unit.

## Basic .richmediarc concepts

Below are some guides on how you can use these values in your creative.

### Using .richmediarc values in HTML

In your index.html, you can retrieve .richmediarc values using the **data-bind** attribute on HTML elements. This is 
made possible by the databind class which is imported by ./js/Banner.js.



For example:

In .richmediarc:
```
"content": {
...
	"cta": "Click here!"
}
```  

In index.html:


```html
<body>
  <div class="cta" data-bind="text: cta"></div>
</body>
``` 

and

In .richmediarc:
```
"content": {
...
  "bg-img-url": "../shared/images/background_300x250.jpg"
...
}
```

In index.html:
```html
<body>
  <img class="background-image" data-bind="src: bg-img-url"></div>
</body>
```  

### Using .richmediarc values in CSS

In CSS, you can retrieve these values as follows:

```css
var(--{node}-{childNode}-{childNode})
```

For example:

In .richmediarc:
```
"content": {
...
	"bgcolor": "#FFFFFF"
...
}
```
In style.css:
```css
body {
  background-color: var(--content-bgcolor);
}
``` 

and

In .richmediarc:
```
"settings": {
	"size": {
    "width": 300,
    "height": 250
  }
}
```
In style.css:
```css
.banner {
  width: var(--settings-size-width)px;
  height: var(--settings-size-height)px;
}
```
### Using .richmediarc values in javascript

The main javascript file (conveniently named ./js/main.js) imports the .richmediarc files as follows:

```js
import config from "richmediaconfig";
```
and passes this object into the Banner constructor

```js
const banner = new Banner(config);
```
Which also passes the config object to the Animation constructor.

From there, you are able to retrieve pretty much every value from the .richmediarc.

Example:

In .richmediarc:
```
"content": {
...
  "intro": false
...
}
```  
In Animation.js:
```js
export default class Animation {
  constructor(container, config) {
    if (config.content.intro) {
      // play intro
    } else {
      // play main animation
    }
  }
}
```
## Advanced .richmediarc concepts

Below are advanced techniques you can use in the .richmediarc file.

### Inheritance

Sometimes you need to set up multiple .richmediarc files in the same creative. For example, when you’re working on a multilingual project and you want the English version to say “Click Here”, whereas the French version says ‘Cliquez Ici’.

In this case, the most elegant solution would be two .richmediarc files. For example:

.richmediarc.en

.richmediarc.fr


However, there will be a lot of overlap between these two files, if you’re only changing the copy - and not the background colors, the width height, the entry files, etc.

Our system supports inheritance of values, by providing a ‘parent’ file from which to inherit all the values defined in that file. The ‘child’ file can then overwrite only the needed values, thereby completely eliminating any overlap between the parent and child files.

Example

.richmediarc.en (parent file):
```
{
  "settings": {
  "type": "plain",
  "entry": {
    "js": "./script/main.js",
    "html": "./index.html"
},
  "size": {
    "width": 300,
    "height": 250
  }
},
  "content": {
    "text": "Welcome!",
    "cta": "Click here",
    "bgcolor": "#FF0000"
    "bgimg": "./img/bgimage.jpg"
  }
}
```
.richmediarc.fr (child file):
```
{
  "parent": "./richmediarc.en",
  "content": {
    "text": "Bienvenue!",
     "cta": "Cliquez Ici"
  }
}
```
As shown in the example above, in the French .richmediarc, we only specify the parent file, and the new values for text and cta. Everything else is inherited from the parent file.

This method is very useful and scalable, should the need arise to add even more languages or versions.

## Feeds
You are able to link to a google spreadsheet so you can build multiple units with one code base and one .richmediarc.

```
{
  "settings": {
    "entry": {
      "js": "./script/main.js", // required: points to the starting js file.
      "html": "./index.html" // required: points to the main html file.
    },
    "size": {
      "width": 300, // required: width of richmedia unit
      "height": 600 // required: height of richmedia unit
    },
    "contentSource":{
      "url":"https://docs.google.com/spreadsheets/d/1cWkhMxC01WVFqWR616DyN7OPvtatD-ivguK9OSs_msg/edit?usp=sharing",
      "apiKey": "API_KEY_PLACEHOLDER"
    }
  },
  "content": {
    "copy1": "This is the first copy",
    "copy2": "This is the second copy",
    "bgcolor": "#FF0000", 
    "logo": "./img/logo.png"
  }
}
```
When you replaced API_KEY_PLACEHOLDER with your own api key <br><br> https://developers.google.com/sheets/api/guides/authorizing#APIKey

> **_Important:_** The Google sheet access needs to be set to public in order for this to work 

[Go back](getting-started.md)