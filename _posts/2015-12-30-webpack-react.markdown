---
layout: post
title:  "More Webpack, with a little React & ES2015."
date:   2015-12-30 18:02:03
categories: Posts 5
permalink: /webpack-react-es2015
---
Hello again, welcome to part two post on [Webpack]. This time we will be extending the configuration setup in the last post to utilize JavaScript's newest syntax features, ES2015. We'll also add the necessary dependencies to use React, a framework created by Facebook and open-sourced (incase you still have not heard). Let's dig in.

So, we left off last time with a simple but working webpack.config.js. It utilized Webpack's server and hot reloader for easy development, here are the links to the [Gitrepo] and the [blogpost].

Kicking off, we need to install a bunch more npm modules, in no particular order:
- npm sass-loader
- node-sass
- babel-core
- babel-preset-es2015
- babel-preset-react
- babel-loader

{% highlight js%}
  npm i -D node-sass babel-core babel-preset-es2015 babel-preset-react babel-loader
{% endhighlight %}

If you're following on from the previous blog post, you may get an npm error, asking to update Webpack to v1.12.6, I updated this branch to the latest which was 1.12.9. The above dependencies will allow us to run styles through Sass, and our JavaScript through [Babel], a JS pre-processer. Because browsers are not fully up-to-date with JavaScript's newest features, running our code through Babel converts ES2015 code back to ES5. This means we can write JS with module imports, let keyword, arrow functions, even classes if we wish! Go ahead and update the module property in the webpack.config.js file to the below code.

{% highlight js%}

module: {
  loaders: [
    { test: /\.scss$/,
      loaders: ['style', 'css', 'sass'],
      include: path.resolve(ROOT_PATH, 'app')
    },
    {
      test: /\.jsx?$/,
      loader: 'babel',
      query: {
        presets: ['react', 'es2015']
      },
      include: path.resolve(ROOT_PATH, 'app')
    }
  ]
}

{% endhighlight %}

For the styles all we have done is added the sass-loader (and it's dependencies). As mentioned before the loaders array will read from right to left following the unix pipe process. The output of the sass-loader (which will be css) enters as input to the css-loader which in-turn is input for the style-loader.

As for ES2015, this is where we need all the Babel dependencies. First we set up a new object with a test case inside the loaders array. The loader will be the Babel-loader of course. Since Babel v6, more of the Babel code has been split and refactored, this means we now have separate dependencies to run ES2015 and React code through our preprocessor, with the presets, babel-preset-es2015 and babel-preset-react. Now we can update the code to use ES2015, woop!

{% highlight js%}
// This is Main.js

import './styles/main.scss';
import Header from './component';

let body = document.querySelector('body');

let header = document.createElement('div');
header.className = 'header';
document.body.appendChild(header);

let headerElement = document.querySelector('.header');
headerElement.appendChild(Header());

{% endhighlight %}

{% highlight js%}
// This is component.js

export default function () {
  var header = document.createElement('h1');
  header.innerHTML = 'Welcome to Webpack';
  return header;
}

{% endhighlight %}

The code now uses ES2015 import and export features, this makes using well structured, abstracted code much easier to use in our projects. I have also made use of the let keyword for assigning variables, this can be overkill, but if you understand how they work I think it's fine. In short, hoisting is not as much of a concern anymore, where you assign a variable in code, is where it is read. Also they help us with scoping issues a lot more. Well that wasn't to bad, now for a little React!

{% highlight js%}
 npm i -S react react-dom
{% endhighlight %}

Install two more dependencies, the React framework itself and it's counter part for browsers, ReactDOM for DOM manipulations. You can read more about abstraction choice here, [reactblog], in short it's going to make React more versatile and less bloated for different platforms, and allow us to share React components across platforms. Once installed, notice they were saved as dependencies to the project, not development dependencies, update your code to the below snippets.

{% highlight js%}
// main.js

import './styles/main.scss';
import React from 'react';
import ReactDOM from 'react-dom';

import HeaderComponent from './component.jsx';


main();

function main() {

  const app = document.createElement('div');
  document.body.appendChild(app);
  ReactDOM.render(<HeaderComponent title="React Baby!" />, app);

}

{% endhighlight %}

Looking at the above snippet, using the ES2015 import syntax, we include the needed dependencies, including our component.js file, notice this is now imported with the new name, HeaderComponent, you will see why in that files code. Then we make and append the div element as before. Using ReactDOM's render method, the HeaderComponent get's attached to the div, passing in a 'title' property with the value 'React Baby!'. We will be able to access this property in the HeaderComponent.

{% highlight js%}
// component.js

import React from 'react';

const propTypes = {
  title: React.PropTypes.string
};

export default class HeaderComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      header: this.props.title
    }
  }

  render() {
    return (
      <div className="header">
        <h1>{ this.state.header }</h1>
      </div>
    )
  }
}

HeaderComponent.propTypes = propTypes;

{% endhighlight %}

In the above snippet, you will see a React component name HeaderComponent (this is why we imported this name in main.js) created with the es2015 class syntax. As with other languages that use the class syntax, the class calls a constructor function to instantiate itself, then calls super to access it's parent constructor, passing props. This is standard React class creation. In addition, we set some initial state through an object, I am accessing the property passed in from main.js via 'this.props' I can then set this as the components state for use within the component. Once the initial setup is complete, we enter the body of the component, the first thing we see is the render method.

{% highlight js%}
render() {
  return (
    <div className="header">
      <h1>{ this.state.header }</h1>
    </div>
  )
}
{% endhighlight %}

Inside here is where we place our JSX, think of it as html returned from a function. The html will be what renders onto the UI. Some things to note, (not going into too much detail, as this is not a post about creating React components) to set a class on an element, we need to use 'className' instead of just 'class', because 'class' is a reserved word in React. The html/JSX must always be wrapped in a parent element, if I was to remove the h1's outer div, we'd see an error. And best of all, we have accessed the components state by interpolating it into the h1 with curly braces, this becomes very powerful, imagine updating the 'header' state value, what do you think would happen? :)


With this code put together, you should see a React blue background, with the title 'React Baby!'. Here's the new Git repo, [newbloglink]. I really hope you found this post useful, it was designed to extend the Webpack code from the previous post to allow us to use React and ES2015 in future posts so we can dig into React some more. Take care, and bye for now.

[Webpack]: http://webpack.github.io/
[https://github.com/philipjc/webpack-blog-post]: https://github.com/philipjc/webpack-blog-post
[Babel]: https://babeljs.io/
[Gitrepo]: https://github.com/philipjc/webpack-blog-post
[blogpost]: http://philipjc.me/getting-started-with-webpack/
[reactblog]: https://facebook.github.io/react/blog/page2/
[newbloglink]: https://github.com/philipjc/webpack-blog-post/tree/es6-react
