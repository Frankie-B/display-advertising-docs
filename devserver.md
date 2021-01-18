---
layout: page
title: Richmedia Development Server
subtitle: All documentation you need for the richmedia temple server
---

Here you will find all the information you are looking for. And if not please contribute.

First lets setup everything, for that please follow the steps on documentation page for the [generator](./generator.md)

Once you have setup the generator you can move on to the below documentation to learn how to create display 
advertising units.

- [Getting Started](./getting-started.md)
- [Adjusting a banner](./adjusting-a-banner.md)
- [.richmediarc](./richmediarc.md)
- [Temple server - run, build and upload](./running-building-uploading.md)


### What is the richmedia temple server?
To explain this as fast as possible, the _**RTS**_ (richmedia temple server) is a build and development server to 
develop and build richmedia units as fast as possible.

It does this by setting up a [Webpack]( https://webpack.js.org/ ) environment where ever it finds a [.richmediarc](../richmediarc.md) 
file. Why? Because its faster to just use the same webpack and webpack.config for every display advertising unit, instead of 
creating one for every single unit.

The .richmediarc file has some added features that are explained [here](./richmediarc.md) like being 
able 
to link a feed to a richmedia unit so you can build hundreds of units without having to duplicate any code. Or be able to 
read the data available in the richmediarc in the css file.

[Go back to home page](./index.html)
