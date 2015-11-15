---
layout: post
title:  "Getting started with Webpack."
date:   2015-11-15 14:02:03
categories: Posts 4
permalink: /getting-started-with-webpack
---

Welcome to 'Getting started with [Webpack]'. This will be a short post about how to get started with an awesome build tool called [Webpack]. If you are familiar with tools such as Gulp or Grunt, you're going to love [Webpack] (I do).

What is it?
[Webpack] is not just another build tool for cleaning up your code before deployment, and then concatenating it all into one file (it can do this, very well) ready to be served up. [Webpack] will take your modules and any dependencies and generate static assets defining said modules. [Webpack] chunks your code and serves it up when it is needed. This can dramatically increase the load times of your applications. Something to note though, code splitting is an opt in feature which we will get into later in the series. For now I would just like to show you how easy it is to set up a development environment for front end development.

I won't go into the details of creating a new project directory, as this one will be very simple. However you will need [Node] installed on your system so we can install [Webpack] and other modules via npm (node package manager), there are plenty of good tutorials on the web to help with this.

From your new folder, perform an 'npm init' follow the instructions. Once this is done, install all the dependencies needed for this tutorial with this command. Optionally you can clone the repo from https://github.com/philipjc/webpack-blog-post.

{% highlight js%}
npm i -D webpack webpack-dev-server webpack-merge html-webpack-plugin node-libs-browser style-loader css-loader webpack-merge

{% endhighlight %}

Inside your project directory, create another folder named app (or whatever you like) and create a javascript file, I named mine <b>main.js</b>. Also, create another folder inside app to represent your styles and create a .css file, might as well give the page some colour!

{% highlight js%}
Project dir
  /app
    main.js
    /styles
      -main.css

{% endhighlight %}

Place this code inside your main.js. Just some simple DOM manipulation to add a h1 element to the page.
{% highlight js%}

function () {
  var header = document.createElement('h1');
  header.innerHTML = 'Welcome to Webpack';
  return header;
}

var body = document.querySelector('body');
var header = document.createElement('div');

header.className = 'header';
document.body.appendChild(header);

var headerElement = document.querySelector('.header');
headerElement.appendChild(Header());

{% endhighlight %}

Now we have these things set up, it's time to add [Webpack]. Inside your Project directory along with node_modules and the package.json, create a file named <b>webpack.config.js</b>. At the top of this file we will include the needed dependencies, so using commonJS syntax;

{% highlight js%}

var path = require('path');
var HtmlwebpackPlugin = require('html-webpack-plugin');
var webpack = require('webpack');
var TARGET = process.env.npm_lifecycle_event;
var ROOT_PATH = path.resolve(__dirname);

{% endhighlight %}

I will go into more detail about the other modules as and when we use them incase you are not familiar.
We define [Webpack] with a simple object structure. Inside this we include what is known as loaders. If we want to process our code through [Babel] for example for ES6 transpiling or preprocess our CSS into [Sass] we run it through a loader.
Another nice benefit of [Webpack] is its development server.

{% highlight js%}

var path = require('path');
var HtmlwebpackPlugin = require('html-webpack-plugin');
var webpack = require('webpack');

var ROOT_PATH = path.resolve(__dirname);

module.exports = {
  entry: path.resolve(ROOT_PATH, 'app/main.js'),
  output: {
    path: path.resolve(ROOT_PATH, 'build'),
    filename: 'bundle.js'
  },

  module: {
    loaders: [
      { test: /\.css$/, loaders: ['style', 'css'], include: path.resolve(ROOT_PATH, 'app') }
    ]
  },

  devServer: {
    port: 4000,
    colors: true,
    historyApiFallback: true,
    inline: true
  },

  plugins: [
    new HtmlwebpackPlugin({ title: 'webpack' }),
    new webpack.HotModuleReplacementPlugin()
  ]
};

{% endhighlight %}

From the top. We require path so we can handle transforming file paths rather than using __dirname.
We require the <b>html-webpack-plugin</b>, this will automatically create our <b>index.html</b> with a html5 doc and place our <b>bundle.js</b> file as a script for us. Then of course require [Webpack] its self. Following this, save our root path utilizing the 'path' module, into a variable named ROOT_PATH to use in the code.

we use module.exports so the CommonJS module system knows what to pass to the outside world.
The <b>entry</b> property shows the path of the files we want [Webpack] to run over, here we have specified <b>app/main.js</b>, but to cover an entire app just remove the <b>main.js</b>.
The <b>output</b> property describes the path to place a directory name build, to store a file named <b>bundle.js</b> that references all of our packaged modules.

{% highlight js%}

module: {
  loaders: [
    { test: /\.css$/, loaders: ['style', 'css'], include: path.resolve(ROOT_PATH, 'app') }
  ]
},

{% endhighlight %}

This is the <b>loaders</b> we pass our code through. Currently we are just processing styles, but in future posts I will extend this to process ES2015 using [Babel], [Sass] and more. I'll describe each property.

- test: Is a regular expression to match file extensions.
- loaders: Are the module you can install as dev dependencies to run your code through.
- include: Is all the file path to your styles. You can also ass an include property to ignore directories.

{% highlight js%}

devServer: {
  port: 4000,
  colors: true,
  historyApiFallback: true,
  inline: true
},

{% endhighlight %}

Here is the Dev server. This is a small [Node] server using [Express] framework. It uses the [Webpack] middleware to serve the [Webpack] bundles. Webpack-dev-server runs in-memory, it automatically refreshes content in the browser while you develop the application.

- port: choose a port to run on, default is 4000.
- colors: Will add some coloring to your terminal output.
- HTML5 History API fallback. Allowing the HTML5 history routes to work.
- inline: This embeds the webpack-dev-server runtime into the bundle allowing Hot Module Replacement to work more easily, this will be great in the future.

There are many more configuration options available, but I am trying to keep this intro short and quickly setup a simple development environment.

{% highlight js%}

plugins: [
  new HtmlwebpackPlugin({ title: 'webpack' }),
  new webpack.HotModuleReplacementPlugin()
]

{% endhighlight %}

There are many plugins for [Webpack] but I have added only these two for now. HtmlwebpackPlugin will create the index.html file needed to run the app for us, holding it in memory. HotModuleReplacementPlugin is what we need to run the hot module replacement which we'll need in the future.

{% highlight js%}
"scripts": {
    "start": "webpack-dev-server",
  },
{% endhighlight %}

Inside your <b>package.json</b> file, place this start command. Once you have all of the above setup, you should be able to run  <i>npm start</i>  from your terminal. Navigate to localhost:4000 and see [Webpack] in all its glory.

Thanks for reading and I hope you find as much enjoyment with using [Webpack] as I do. I look forward to extending this intro further to show you more of Webpacks capabilities.

Find the complete Source code on Github: https://github.com/philipjc/webpack-blog-post


[Webpack]: http://webpack.github.io/
[html-webpack-plugin]: https://www.npmjs.com/package/html-webpack-plugin
[Node]: https://nodejs.org/en/
[Express]: http://expressjs.com/
[Babel]: https://babeljs.io/
[Sass]: http://sass-lang.com/
