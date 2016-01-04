---
layout: post
title:  "Creating a React component, using class syntax."
date:   2016-01-03 18:52:03
categories: Posts 6
permalink: /react-class-component
---
Hello and a happy (React) new to you. I hope you all had fun hacking away over the holidays, I know I did. In this post, I am going to show you how to create a few simple React components using the ES2015 class syntax. This way of creating React components is not popular with everyone, but I still think it's good to know and quite enjoy using it. I believe its lack of popularity with some fine folks is due to the ongoing debate about JavaScript being prototypical language, and using class syntax avoids understanding this. I personally like to understand both ends of a spectrum.

Setting up React and Babel takes a little time (as does all setup) fortunately, there are plenty of good bootstrapping projects out there. I will be using my creation, and one I have recently blogged about, you can find it here: [react-boot]

Looking over the source code of my Git repo, you will notice there is already a React component using class syntax named component.jsx. The same component is also below.

{% highlight js%}
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

From the top, I import React using ES2015 imports. Following on, an object name propTypes gets created as a const, this gets used to set the components prop types at the end of the declaration. Setting your components expected prop types is a nice todo, because if you accidentally send an incorrect prop you will see an error. More on props later.



{% highlight js%}
export default class HeaderComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      header: this.props.title
    }
  }
{% endhighlight %}

The next section of the code is how the component is created. Following the [Airbnb] style guide, I like to export the component as it's created (saves forgetting to do it at the end) then, using the ES2015 class keyword we name the component, a convention is to capitalize. As you can see it extends the React base component. If you are familiar with strongly typed language like Java, the next bit will look nice and familiar.

The new React component needs a constructor call to setup, super also needs to be called, as we do extend from the superclass. Then, you can set your state inside an object, 'this' refers to the component. If there is no initial state it can be left blank. In our example I set a property on the state named header, its value if whatever the prop named title is holding, checking the source code we can see this is 'React baby!'. We can then use the title string inside the component.


{% highlight js%}
render() {
  return (
    <div className="header">
      <h1>{ this.state.header }</h1>
    </div>
  )
}
}

{% endhighlight %}


Following on we hit the render method of the component. The method immediately returns the components JSX (html). All elements need to be inside a parent tag, placing the h1 tag inside all lonely would throw an error. Talking of the h1, as you can see it has curly braces inside and a reference to the components state object looking up the header property, this is how you can place dynamic data inside your component. Alternatively, we could have just placed 'this.props.title' inside the braces, and not set any state.


{% highlight js%}
<h1>{ this.props.title }</h1>
{% endhighlight %}

Purposefully glossing over the reasons for when and why to use state or props, but it will all become clear. But, offering a small insight, state is used only inside of the component, props is used when we are passing data down through the parent, child component chain. Once an app is hooked up to flux or reflux, we try to pass all of our applications state down from a Store, into the top most component. Once all state is in the parent component, specific state can be passed as props to the individual components that need it.

Lastly, I set components propsTypes to be the object created at the start.

{% highlight js%}
HeaderComponent.propTypes = propTypes;
{% endhighlight %}

### Thinking React
As mentioned earlier, props are passed down through components, this can only be done if the components are nested. Once they are nested we have a parent child relationship. When thinking about the creation of a new app or site we have to think about chunking it up into pieces, components. This helps us to consider which components may depend on each other, which ones need to be nested.

For example, lets consider a menu list. There would be a Menu component, this would return the ul tag. In addition, there would be a ListItem component, this would return an li tag. For every menu item, a ListItem component would be used, thus building the menu. Lets see how this would look.

{% highlight js%}
import React from 'react';
import Header from './components/Header.jsx';
import Menu from './components/Menu.jsx';

class Main extends React.Component {

 constructor(props) {
   super(props);
 }

 render() {
   return (
     <div className="app">
       <Header title="React Baby!" />
       <Menu />
     </div>
   );
 }
};

export default Main;

{% endhighlight %}

As you can see above, I made some changes to the structure of the app. We no longer wanted to have Header component as the top level mounted component. So a component named Main was made for this. Main, imports Header and makes use of it inside its JSX. So, we can think of Main as our top level component. The component Menu also gets placed inside Main.

See below for the Menu component, and an updated Main.js
{% highlight js%}
// Main.js
import './styles/main.scss';
import React from 'react';
import ReactDOM from 'react-dom';

import Main from './Main.jsx';

main();

function main() {
  const app = document.createElement('div');
  document.body.appendChild(app);
  ReactDOM.render(<Main />, app);
}
{% endhighlight %}

{% highlight js%}
// Menu.jsx
import React from 'react';
import ListItem from './ListItem.jsx';

class Menu extends React.Component {

 constructor(props) {
   super(props);
   this.state = {
     menu: ['Home', 'About', 'Service']
   }
 }

 render() {
   return (
     <div className='navigation'>
       <ul className='navigation__menu'>
         { this.state.menu.map((name, idx) => {
           return <ListItem name={ name } key={ idx }/>
         })}
       </ul>
     </div>
   );
 }
};

export default Menu;
{% endhighlight %}

For ease, I set Mains state to hold a property called menu, this property contains an array of possible menu names. These names will be rendered as the individual menu items through a ListItem component. To achieve this, I use the ES5 Array map method to loop over each value in the array and return a ListItem component for each one. The map method returns an array back, React deals with arrays very well, and renders each component for us.

Giving each ListItem component a prop named name, that takes the value name, name is a string from the array, this comes from the map method. Also, React likes each of its rendered component to have a unique index key, this makes its easier for React to re-render each time.


{% highlight js%}
import React from 'react';

class ListItem extends React.Component {

 constructor(props) {
   super(props);
 }

 render() {
   return (
     <li className="menu-item">
       { this.props.name }
     </li>
   );
 }
};

export default ListItem;
{% endhighlight %}

Last, but not least, the ListItem component. It looks very much the same as previous components. Inside the li tag we place the prop .name, remember, this was past in by Menu, which will be the string from the array.

Running npm start from your Terminal, you should now see a not very well style list of menu names. I hope you found this read useful. As always you can find the updated repo here: [react-component]

[react-boot]: https://github.com/philipjc/webpack-blog-post
[react-component]: https://github.com/philipjc/webpack-blog-post/tree/react-component
[Airbnb]: https://github.com/airbnb/javascript/tree/master/react
