---
layout: page
title: Getting started
---

# Contents

- [Creating a new project](#creating-a-new-project)
- [Adjust a banner step by step](./adjusting-a-banner.md)
- [.richmediarc](./richmediarc.md)
- [Running a development server locally](./running-building-uploading.md)
- [Types of banners](banner-types.md)
- [Package.json](./package-json.md)

## Creating a new project

Its advisable when creating a new richmedia unit to first scaffold the initial project This will save you a lot of
time and effort. More information on how to do this can be found [here](getting-started.md).

In the terminal, make your way to a new project folder of your choosing, i.e. documents/work/my-banner-project

### Step 1

Generate (scaffold) a new banner project. This will generate all the necessary files and folder structure
you need for the project.

$ `yo richmedia-temple`

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608810960/MM_Temple_Server_docs/Screenshot_install_richmedia_scaffold.png" />
</div>

If this is the first time you’re running this command, Yeoman will ask you the following:

```
We're constantly looking for ways to make yo better!

May we anonymously report usage statistics to improve the tool over time?

More info: https://github.com/yeoman/insight & http://yeoman.io

Up to you if you want to send them statistics. Hit either **Y** or **N**.
```

After you make your selection, the following menu appears

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608811575/MM_Temple_Server_docs/Screenshot_richmedia-welcome.png" />
</div>

In this menu you can use the arrow keys to navigate the cursor.

### Step 2

We’re just going to create a standard banner in this guide, so in this case, just hit Enter to select

‘create a banner’.

Enter the name of the project or just hit enter to use the default, which is the folder name.

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608811916/MM_Temple_Server_docs/Screenshot_banner-name.png" />
</div>


### Step 3

Select the first unit you would like the generator to create. Use the arrow keys to navigate and hit Enter
when ready.

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608812165/MM_Temple_Server_docs/Screenshot_select-unit-size.png" />
</div>

Enter the directory where you wish the source files to be placed. Just hit enter to use the default, which is something like “./src/{size}x{width}”


Select the type of banner (refer to [types of banners](./banner-types.md) for more info)

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608812407/MM_Temple_Server_docs/Screenshot_banner-type.png" />
</div>

For the purposes of this guide, select ‘plain’.

The generator will generate the basic template files and install the according node modules as well. This process will take a minute.

When it’s done, you’ll end up with a directory looking something like this

You now should see a few files in the directory that you executed the generator on.

| Filename                     | Description                                                                                                                                                |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| node_modules                 | all the packages / libraries your project uses.                                                                                                            |
| src/300x250/[.richmediarc](./richmediarc.md)   | The configuration file for the richmedia-temple-server, This file is used so that the richmedia-temple-server knows what directories are richmedia units.  |
| src/300x250/script/main.js   | Javascript File this is referenced by the .richmediarc file.                                                                                               |
| src/300x250/script/Banner.js | The banner javascript code.                                                                                                                                |
| src/300x250/index.html       | Main html file, this file is referenced by the .richmediarc file.
| .editorconfig                | configuration file for you editor. So everyone atleasts uses the same basic settings.                                                                      |
| .gitignore                   | configuration file used by git so it knows which files to ignore.                                                                                          |
| .prettierrc                  | A configuration file for prettier printer
| [package.json](./package-json.md)                 | A configuration file for NPM / YARN, one of the most important files in your project.                                                                      |



<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608814657/MM_Temple_Server_docs/Screenshot_project-structure.png" />
</div>


To start developing you need to run a webpack server. Setting up a webpack server is a bit of a hassle thats why the 
[generator](./generator.md) and the [richmedia-temple-server](./devserver.md) do this for you in conjuction with the 
[.richmediarc](./richmediarc.md) 
file.

### Step 4

Make sure everything works by running

$ `npm run dev`(more info [@mediamonks/richmedia-temple-server](./devserver.md) )

(./running-building-uploading.md))

You should now go to the documentation of the

This will start the server. You’ll see something like


<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608814774/MM_Temple_Server_docs/Screenshot_run_dev_server.png" />
</div>

Press **N**

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608814963/MM_Temple_Server_docs/Screenshot_localhost8000.png" />
</div>

Your primary browser will launch, opening [http://localhost:8000/](http://localhost:8000/)

In your terminal, you’ll be able to see the output of webpack, compiling the source code.

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608815327/MM_Temple_Server_docs/Screenshot_webpack-compiling.png" />
</div>

In your browser, the preview environment will load along with a preview of the compiled version of the banner you just created. The banner should display as a simple unit with a red background.

<div style="display: flex; justify-content: center">
<img src="https://res.cloudinary.com/frankie-dev/image/upload/v1608815492/MM_Temple_Server_docs/Screenshot_banner-browser.png" />
</div>

If there are no javascript errors and everything works fine, that’s it!

[Go back to Temple Server](./devserver.md)
