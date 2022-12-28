# Intro to React

## What is JSX?

```const h1 = <h1>Hello world</h1>;```

It looks like a hybrid of JavaScript and HTML but it is neither, so what is it?

This is *JSX*, a syntax extension for JavaScript, and was written to be used with React. But what does "syntax extension" mean? It means that it is not valid JavaScript which means that web browsers can't read it.

If a JavaScript file contains JSX then that file will have to be *compiled*, meaning that before the file reaches a web browser a *JSX compiler* will translate any JSX into regular JS.

## JSX Elements

```<h1>Hello World</h1>```

It looks exactly like HTML but the only notable difference is that this code will be contained inside a JavaScript file instead of an HTML file.

# JSX Elements and Their Surroundings

JSX elements are treated as JavaScript *expressions*. They can go anywhere that JavaScript expressions can go.

That means that a JSX element can be saved in a variable, passed to a function, stored in an object or array, etc. For example:

```const navBar = <nav>I am a nav bar</nav>;```

This is a JSX element stored in a variable

```
const myTeam = {
  center: <li>Benzo Walli</li>,
  powerForward: <li>Rasha Loa</li>,
  smallForward: <li>Tayshaun Dasmoto</li>,
  shootingGuard: <li>Colmar Cumberbatch</li>,
  pointGuard: <li>Femi Billon</li>
};
```
These are JSX elements stored in an object

## Attributes in JSX

JSX elements can also have *attributes* just like HTML elements can.

The syntax for defining attributes is similar to HTML, it requires a *name*, then an equals sign, followed by a *value* which must be contained inside of quotes, like so:

```my-attribute-name="my-attribute-value"```

A more practical example:

```
<a href='http://www.example.com'>Welcome to the Web</a>;
 
const title = <h1 id='title'>Introduction to React.js: Part I</h1>;
``` 

A single JSX element can also have multiple attributes just like HTML:

```const panda = <img src='images/panda.jpg' alt='panda' width='500px' height='500px' />;```

## Nested JSX

JSX elements can be *nested* inside of other JSX elements, just like HTML. For example:

```<a href="https://www.example.com"><h1>Click me!</h1></a>```

In this example, the `<h1>` element is nested inside of the `<a>` element. However, we should always use line breaks and indentations to make our code more readable, like so:

```
(
<a href="https://www.example.com">
  <h1>
    Click me!
  </h1>
</a>
)
```
But what's up with the parenthesis `()`? If a JSX expression takes up more than one line, then you must wrap the multi-line JSX expression in parenthesis.

We can also save nested JSX expressions as variables, pass them to functions, etc.

```
 const theExample = (
   <a href="https://www.example.com">
     <h1>
       Click me!
     </h1>
   </a>
 );
```

## JSX Outer Elements

Every JSX expression must have exactly *one* outermost element, for example:

```
const paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```
This code above is a valid JSX expression but the code below *is not*

```
const paragraphs = (
  <p>I am a paragraph.</p> 
  <p>I, too, am a paragraph.</p>
);
```
More simply, the first opening tag and the final closing tag of a JSX expression must belong to the same JSX element.

If you notice that a JSX expression has multiple outer elements then we can wrap the expression in a `<div></div>` to contain it inside one single element.

## Rendering JSX

Everything in the previous sections covered how to *write* JSX elements but how do we *render* them?

To *render* a JSX expression means to make it appear onscreen.

```
ReactDOM.render(<h1>Render me!</h1>, document.getElementById('app'));
```

What is `ReactDOM`? This is the name of JavaScript library that contains several React-specific methods, all of which deal with the [DOM](https://www.w3schools.com/js/js_htmldom.asp)(Document Object Model) in some way or another.

The method `ReactDOM.render()` is the most common way to *render* JSX. It takes a JSX expression, creates a corresponding tree of DOM nodes, and then adds that tree to the DOM.

```<h1>Render me!</h1>``` 

This is the first argument being passed into `ReactDOM.render()`. The first argument should be a JSX expression and it will then be rendered to the screen.

```document.getElementById('app')```

The second argument dictates *where* on the screen the first argument will appear. **The first argument is appended to whatever element is selected by the second element.**

Meaning, `ReactDOM.render()` will look for the HTML element with the attribute `id="app"` and render the first argument in that identified element.

## Passing a Variable to `ReactDOM.render()`

The first argument of `ReactDOM.render()` should *evalulate* to a JSX expression, it does not have to *literally* be a JSX expression, meaning that we can also pass a variable - that has a JSX expression as its value - as the first argument of the `ReactDOM.render()` method.

For example:

```
const toDoList = (
  <ol>
    <li>Learn React</li>
    <li>Become a Developer</li>
  </ol>
);
 
ReactDOM.render(
  toDoList, 
  document.getElementById('app')
);
```

In this example we have a variable `toDoList` that contains JSX elements which is then passed into the `ReactDOM.render` method as the first argument.

## The Virtual DOM

One special thing about `ReactDOM.render()` is that it *only updates DOM elements that have changed*. Meaning that if you render the exact same thing twice in a row, the second render will do nothing.

```
const hello = <h1>Hello world</h1>;
 
// This will add "Hello world" to the screen:
 
ReactDOM.render(hello, document.getElementById('app'));
 
// This won't do anything at all:
 
ReactDOM.render(hello, document.getElementById('app'));
```

This is a very significant feature because only updating the necessary DOM elements is a large part of what makes React so successful.

This is accomplished thanks to something called *the virtual DOM*. More in-depth information about the virtual DOM can be found [here](https://www.codecademy.com/article/react-virtual-dom).

# Advanced JSX

## class vs. className

A lot of JSX's syntax and grammar are similar to HTML but there are subtle differences to keep in mind. One common one is with the attribute `class` vs `className`.

In HTML, the attribute `class` is commonly used to identify certain HTML elements. JSX is similar but you can't use the attribute `class`, instead we need to use `className`.

This is because JSX gets translated into JavaScript and the `class` is a reserved word within JavaScript.

When JSX is *rendered*, the JSX `className` attribute are automatically rendered as `class` attributes.

## Self-Closing Tags

Most HTML elements use tag, an opening(`<div>`) and a closing one (`</div>`). However, some HTML elements such as `<img>` and `<input>` use only one tag.

Tags that belong to a single-tag element are neither *opening* or *closing* tags but rather a *self-closing* tag.

When you write a self-closing tag in HTML, it is *optional* to include a slash immediately before the final angle bracket.

```
<!-- Fine in both JSX and HTML: -->
 
  <br />
 
<!-- Fine in HTML but not JSX: -->
 
  <br>
```
But in JSX *you have to include the slash*. If you write a self-closing tag in JSX and forget the slash, you will return an error.

## JavaScript in Your JSX in Your JavaScript

So far we've only covered writing JSX expressions, which is esentially writing bits of HTML inside of a JavaScript file.

However, what about regular JavaScript written inside of a JSX expression which is written inside of a JavaScript file?

If we were to write

```
ReactDOM.render(
  <h1>2 + 3</h1>,
  document.getElementById('app')
);
```

The screen would render "2+3", not add them together to render "5". This is because the code between the two `<h1>` tags will be read as JSX, *not* as a regular JavaScript. JSX does not add numbers, it reads them as text just like HTML.

If we want the code to be interpreted as JavaScript we need to wrap the code in curly braces `{}`.

```<h1>{2 + 3}</h1>```

This will cause the operation "2 + 3" to be read as JavaScript instead of JSX. The curly braces themselves are not treated as JSX or JS, rather they are *markers* that signal the beginning and end of a JavaScript injection into the JSX - similar to how quotation marks signlar the boundaries of a string.

## Variables in JSX

When you inject JavaScript into JSX, that JavaScript is part of the same environment as the rest of the JavaScript in your file.

That means that you can access variables while inside of a JSX expression, even if those variables were declared on the outside.

```
// Declare a variable:
const name = 'Gerdo';
 
// Access your variable 
// from inside of a JSX expression:
const greeting = <p>Hello, {name}!</p>;
```

## Variable Attributes in JSX

When writing JSX, it’s common to use variables to set attributes.

Here’s an example of how that might work:

```
// Use a variable to set the `height` and `width` attributes:
 
const sideLength = "200px";
 
const panda = (
  <img 
    src="images/panda.jpg" 
    alt="panda" 
    height={sideLength} 
    width={sideLength} />
);
```

Notice that each attribute gets its own line; this makes the code more readable if you have a lot of attributes on one element.

We can also use an *object's properties* to set attributes as well

```
const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
}; 
 
const panda = (
  <img 
    src={pics.panda} 
    alt="Lazy Panda" />
);
 
const owl = (
  <img 
    src={pics.owl} 
    alt="Unimpressed Owl" />
);
 
const owlCat = (
  <img 
    src={pics.owlCat} 
    alt="Ghastly Abomination" />
);
```

## Event Listeners in JSX

Working in React means constantly working with event listeners but what is an event listener? An event listener is a procedure in JavaScript that waits for an event to occur - like a user clicking their mouse or pressing a key on a keyboard - and then fires off more code based on what event happened.

For example:

```<img onClick={myFunc} />```

An event listener attribute's *name* should be something like `onClick` or `onMouseOver`. The word `on` plus the event that you're listening for. For a complete list of valid event names [click here](http://facebook.github.io/react/docs/events.html#supported-events).

An event listener attribute's *value* should be a function. The above example would be valid if `myFunc` was defined elsewhere. 

Note that in HTML, event listener names are written in all lowercase, such as `onclick` or `onmouseover` but in JSX event listener names are written in camelCase such as `onClick` and `onMouseOver`.

## JSX Conditionals: If Statements That Don't Work

We know how to inject JavaScript into a JSX expression however there is a rule that we need to know: **you can not inject and `if` statement into a JSX expression**

For example, this will not work:

```
(
  <h1>
    {
      if (purchase.complete) {
        'Thank you for placing an order!'
      }
    }
  </h1>
)
```

The reason why is because of the way that JSX is compiled, we won't go into detail here but if you want to read more about it you can read more in the [React Documentation](https://reactjs.org/docs/jsx-in-depth.html).

But what if we want a JSX expression to render only under certain circumstances? We can't use an `if` statement, so what do we do?

One way is to write an `if` statement and *not* inject it into JSX. For example:

```
import React from 'react';
import ReactDOM from 'react-dom';

let message;

if (user.age >= drinkingAge) {
  message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  message = (
    <h1>
      Hey, check out these earrings I got at Claire's!
    </h1>
  );
}

ReactDOM.render(
  message, 
  document.getElementById('app')
);
```
This would work because the conditionals `if` and `else` are *not* injected in between JSX tags. The `if` statement is on the outside so no JavaScript injection is necessary.

This is a common way to express conditionals in JSX.

## JSX Conditionals: The Ternary Operator

A more compact way to write conditionals in JSX is with the *ternary operator* and it works the same way in React as it does in regular JavaScript.

The syntax being:

``` x ? y : z ```

Where `x`, `y`, and `z` are all JavaScript expressions. When the code is executed, `x` is evaluated as either "truthy" or "falsy". If its truthy then `y` is returned and if its falsy then `z` is returned. [Here is a brief refresher if needed](http://stackoverflow.com/questions/6259982/how-to-use-the-ternary-operator-in-javascript)

In practice, it looks like this:

```
const headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);
```
Here we are determining if `age` is greater than or equal to `drinkingAge` and if it is we return "buy drink" and if not we return "do teen stuff".

## JSX Conditionals: &&

Like the ternary operator, `&&` is not React-specific but it does show up in React surprisingly often. This works best in conditionals that will sometimes do an action but other times will do *nothing at all*.

```
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

If the expression on the left of the `&&` evaluates as true, then the JSX on the right  will be rendered. If the expression on the left of `&&` is false, then the JSX to the right will be ignored and not rendered.

## .map in JSX

The array method `.map()` also comes up often in React.

```
const strings = ['Home', 'Shop', 'About Me'];
 
const listItems = strings.map(string => <li>{string}</li>);
 
<ul>{listItems}</ul>
```

In the example above, we start with an array of strings. Then we call `.map()` on the array of strings, which then returns a new array of `<li>`s

On the last line of the example we see that `{listItems}` will evaluate to an array because it's the returned value of the `.map()` method. JSX `<li>`s don't have to be in array like this but they *can* be.

```
// This is fine in JSX, not in an explicit array:
 
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
 
// This is also fine!
 
const liArray = [
  <li>item 1</li>, 
  <li>item 2</li>, 
  <li>item 3</li>
];
 
<ul>{liArray}</ul>
```

## Keys

Sometimes when we make a list in JSX the list items will need to include something called `keys`.

```
<ul>
  <li key="li-01">Example1</li>
  <li key="li-02">Example2</li>
  <li key="li-03">Example3</li>
</ul>
```

`key` is the *name* of a JSX attribute so its *value* should be something unique, similar to an `id` attribute.

`key`s don' do anything that you can see. React uses them internally to keep track of lists. If you don't use keys when you're supposed to, React might accidentally scramble your list items in the wrong order.

Not all lists need to have `key`s, they are only necessary if either one of the following are true:

1. The list-items have memory from one render to the next. For instance, when a to-do list renders, each item must “remember” whether it was checked off. The items shouldn’t get amnesia when they render.

2. A list’s order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.

If neither of these conditions are true then you don't have to worry about using `key`s however if you aren't sure then it never hurts to use them.

But how do we efficiently create unique `key`s? One way that we can create unique `key`s when we use `.map()` is to include `i` as a parameter. For example:

```
const people = ['Rowe', 'Prevost', 'Gare'];

const peopleLis = people.map((person, i) =>
  // expression goes here:
  <li key={'person_' + i}>{person}</li>
);
```

By doing this, everytime the `.map()` function iterates the `i` parameter will also increase. This gives each list item a unique key combining the person's name and their order on the list.

## React.createElement

You can write React code without using JSX at all!

The majority of React programmers do use JSX, and we will use it for the remainder of this tutorial, but you should understand that it is possible to write React code without it.

The following JSX expression:

```const h1 = <h1>Hello world</h1>;```

can be rewritten without JSX, like this:

```
const h1 = React.createElement(
  "h1",
  null,
  "Hello world"
);
```
When a JSX element is compiled, the compiler transforms the JSX element into the method that you see above: `React.createElement()`. Every JSX element is secretly a call to `React.createElement()`.

We won't dive into how it all works here, but if you want to learn more then refer to the [documentation](http://facebook.github.io/react/docs/top-level-api.html#react.createelement)
____________________________________________________________________

# React Components

React applications are made out of *components*, but what is a component? A component is a small, reusable chunk of code that is responsible for *one job* and often that job is to render some HTML.

Take a look at the code below. This code will create and render a new React component:

```
import React from 'react';
import ReactDOM from 'react-dom';
 
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
};
 
ReactDOM.render(
  <MyComponentClass />,
  document.getElementById('app')
);
```

A lot of that code is probably unfamiliar. However, you can recognize some JSX in there, as well as `ReactDOM.render()`.

We'll learn more about that code one piece at a time in the following sections.
____________________________________________________________________

## Import React

```import React from 'react';```

This creates an object named `React` which contains the methods necessary to use the React library.

We'll cover where the React library is imported from and how the importing process works in future sections, for now just know that this is how to do it.

When a JSX element is *compiled*, it transforms into a `React.createElement()` call.

For this reason we *have to* import the React library and save it in a variable named React before you can use any JSX at all. `React.createElement()` must be available in order for JSX to work.
____________________________________________________________________

## Import ReactDOM

In order to create our first component we also need to import the ReactDOM

```import ReactDOM from 'react-dom';```

This also imports a JavaScript object that contains React-related methods - but there's a difference between this and the previous section!

The methods imported from `react-dom` are meant for interfacing with the DOM. In the very first example we encountered `ReactDOM.render()`.

The methods imported from `react` don't deal with the DOM at all - they do not engage directly with anything that isn't part of React.

The DOM is *used* in React applications but it is not *part* of React.  Methods imported from `react` are only for pure React purposes, such as creating components or writing JSX elements.
____________________________________________________________________

## Creating a Component Class

A *React component* is a small, reusable chunk of code that is responsible for one job, which often involves rendering HTML.

We can use a JavaScript class to define a new React component. We can also define components with JavaScript functions - but first we'll focus on *class components*.

All class components will have some methods and properties in common - which we'll cover more later - but rather than rewriting those same properties over and over again every time, we *extend* the `Component` class from the React library,

This way we can use the code that we import from the React library without having to write it over and over again ourselves.

After we *define* our class component, we can use it to *render* as many instances of that component as we want.

So, what *is* `React.component` and how do we use it to make a component class?

`React.Component` is a JavaScript *class*. To create our own component class, we must *subclass* `React.Component`. You can do this by using the syntax:

```class OurComponentNameHere extends React.Component {}```
____________________________________________________________________

## Name a Component Class

When we declare a new component class we *need* to give that component class a name. Furthermore, the component name must beging with a capital latter. This adheres to JS class syntax and there is also a React-specific reason why component class names must be capitalized - but we'll cover that later.
____________________________________________________________________

## Component Class Instructions

In the body of our class (read: React.Component subclass) we create a set of instructions explaining to your component class how it should build a React component.

```
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
```
____________________________________________________________________

## The Render Function

A component class is like a factory that builds components. It builds these components by consulting a set of instructions, which you must provide. 

```
class ComponentFactory extends React.Component {
  // instructions go here, between the curly braces
}
```

There is one property that *must* be inculded in the instructions: *a render method*. The property name is `render` and the value of it will be a function. The term, "render method" can refer to the entire property or to just the function part.

```
class ComponentFactory extends React.Component {
  render() {}
}
```

A render method must contain a `return` statement. Usually, this `return` statement returns a JSX expression.
____________________________________________________________________

## Create a Component Instance

We now have a working *component class*, its ready to follow its instructions and make some React components.

```<MyComponentClass />```

To make a React component, you write a *JSX Element*. Instead of naming the JSX element something like `h1` or `div` we should give it the same name as the *component class*. Then, we will have our *component instance*!

JSX elements can be either HTML-like or *component instances*. JSX uses capitalization to distinguish between the two!

*That* is the React-specific reason why component class names must begin with capital letters. In a JSX element, that capitalized first letter says "I will be a component instance and not an HTML tag".
____________________________________________________________________

## Render a Component

You have learned that a component class needs a set of instructions, which tell the component class how to build components. When you make a new component class, these instructions are the body of your class declaration

```
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
```
`MyComponentClass` has one method named `render` (`MyComponentClass.render()`). 

When we create the actual component `<MyComponentClass />`, it also has access to the method `render` through *inheritance*. We could make a million different `<MyComponentClass />` instances and every one would inherit the same `render` method.

So how do we actually *render* the component on screen?

In order to render a component on screen, the component class must have a method named `render`. Since our class component `MyClassComponent` has this, all thats left to do is to call that method.

To call a component's `render` method, you pass that component to `ReactDOM.render().

```
ReactDOM.render(
  <MyComponentClass />,
  document.getElementById('app')
);
```

`ReactDOM.render()` will tell `<MyComponentClass />` to call *its* render method.

`<MyComponentClass /> will call its render method, which will return the JSX element `<h1>Hello world</h1>. 

Then `ReactDOM.render()` will take that resulting JSX element and add it to the virtual DOM.
____________________________________________________________________

# React Components and Advanced JSX

## Using Multiline JSX in a Component

Any multi-line JSX expression must be wrapped in parenthesis.

```
class QuoteMaker extends React.Component {
  render() {
    return (
      <blockquote>
        <p>
          The world is full of objects, more or less interesting; I do not wish to add any more.
        </p>
        <cite>
          <a target="_blank"
            href="https://en.wikipedia.org/wiki/Douglas_Huebler">
            Douglas Huebler
          </a>
        </cite>
      </blockquote>
    );
  }
};
```

Notice that the entire `return` statement, except the `return` keyword, are wrapped in parentheses. Additionally, remember that any & all nested JSX elements must also be contained within a single outer element - in this case, the `<p>`, `<cite>`, and `<a>` elements are all wrapped inside of a `<blockquote>` element.
____________________________________________________________________

## Use a Variable Attribute in a Component

We can also render a React component using variables, take a look at the example below:

```
const redPanda = {
  src: 'https://upload.wikimedia.org/wikipedia/commons/b/b2/Endangered_Red_Panda.jpg',
  alt: 'Red Panda',
  width:  '200px'
};

class RedPanda extends React.Component {
  render() {
    return (
      <div>
        <h1>Cute Red Panda</h1>
        <img 
          src={redPanda.src}
          alt={redPanda.alt}
          width={redPanda.width} />
      </div>
    );
  }
}
```
Remember that when we use JavaScript injections inside of a JSX element we need to wrap the JavaScript with curly braces.

Often you can, and will, inject JavaScript into JSX inside of a render function. 
____________________________________________________________________

## Put Logic in a Render Function

A `render()` function must have a `return` statement, however, that isn't *all* that it can have.

We can also put simple calculations that need ot happen right before a component renders, here's an example:

```
class Random extends React.Component {
  render() {
    // First, some logic that must happen
    // before rendering:
    const n = Math.floor(Math.random() * 10 + 1);
    // Next, a return statement
    // using that logic:
    return <h1>The number is {n}!</h1>;
  }
}
```

Watch out for this common mistake!
```
class Random extends React.Component {
  // This should be in the render function:
  const n = Math.floor(Math.random() * 10 + 1);
 
  render() {
    return <h1>The number is {n}!</h1>;
  }
};
```
In the example above, the line with the `const n` declaration will cause a syntax error, as it should not be part of the class declaration itself - it should occur in a method like `render()`.
____________________________________________________________________

## Use a Conditional in a Render Function

We can also use *conditional* statements inside of a `render()` function.

```
class TodaysPlan extends React.Component {
  render() {
    let task;
    if (!apocalypse) {
      task = 'learn React.js'
    } else {
      task = 'run around'
    }

    return <h1>Today I am going to {task}!</h1>;
  }
}
```

Notice that the `if` statement is located *inside* of the render function but *before* the return statement.

Also note that the conditional statement *is not* wrapped in parentheses because we are using JavaScript not JSX.
____________________________________________________________________

## Use `this` in a Component

```
class IceCreamGuy extends React.Component {
  get food() {
    return 'ice cream';
  }
 
  render() {
    return <h1>I like {this.food}.</h1>;
  }
}
```

In the example above, `this` refers to an instance of `IceCreamGuy`.

To be more in-depth, `this` refers to the object on which `this`'s enclosing method is called, in this case `.render()`. It is almost inevitable that this object will be an instance of `IceCreamGuy`, but technically it could be something else.

Let's assume that `this` refers to an instance of your component class - as it will be in these examples. `IceCreamGuy` has two methods: `.food` and `.render()`. Since `this` will evaluate to an instance of `IceCreamGuy`, `this.food` will evaluate to a call of `IceCreamGuy`s' `.food` method. This method will, in turn, evaluate to the string "ice cream".

Why don't you need parentheses after `this.food`? Shouldn't it be `this.food()`?

You don't need those parentheses because `.food` is a *getter* method. You can tell this from the `get` keyword.

There's nothing React-specific about getter methods, nor about `this` behaving in this way. However, in React you will see `this` used in this way almost constantly.

`this` in JS can be a difficult concept so here is a good resource for [understanding `this` in JavaScript](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/).
____________________________________________________________________

## Use an Event Listener in a Component

Render functions often contain event listeners, here's an example:

```
render() {
  return (
    <div onHover={myFunc}>
    </div>
  );
}
```

Recall that an event *handler* is a function that gets called in response to an event. In the above example, the event handler function is `myFunc()`.

In React, you define event handlers as *methods* on a component class, like this:

```
class MyClass extends React.Component {
  myFunc() {
    alert('Stop it.  Stop hovering.');
  }
 
  render() {
    return (
      <div onHover={this.myFunc}>
      </div>
    );
  }
}
```
Notice that the component class has two methods: `.myFunc()` and `.render()`. 

`.myFunc()` is being used as an *event handler*. 

`.myFunc()` will be called any time that a user hovers over the rendered `<div> </div>`.
____________________________________________________________________

# Creating a React App

## Getting Ready

In order to use React, we must also have *Node* installed on the computer, since we will be using *Node pacakage manager (npm). To check if Node is installed, run the command 

```node -v```

This will return its version number.

When Node is installed, we automatically get npm installed on the computer as well. However, `npm` is a separate project from `Node.js` and tends to update more frequently. As a result, even if you've installed Node (and therefore npm), its always a good idea to update your npm.

```npm install -g npm@latest```
____________________________________________________________________

## Setting Up The Boiler Plate Application

It is possible to manually create a React app, but Facebook has created a Node package [create-react-app](https://create-react-app.dev/) to generate a boilerplate version of a React application.

Besides providing something that works out-of-the-box, this has the added benefit of providing a consistent structure for React apps that you will recognize as you move between React projects. It also provides an out-of-the-box build script and development server.

We will use *npx*, a package runner tool that comes with npm 5.2+ and higher, to install and run `create-react-app`. This will ensure that the latest version of create-react-app is used.

Open up your terminal.

- If you’ve previously installed `create-react-app` globally via `npm install -g create-react-app`, it is recommended that you uninstall the package first. In your terminal run these commands:
```
npm uninstall -g create-react-app
npx create-react-app myfirstreactapp
```
- If you’ve never installed create-react-app before, you can simply run this command:
```
npx create-react-app myfirstreactapp
```

Note that "myfirstreactapp" can be replaced with whatever name you'd like so long as it does not contain capital letters.

Upon completion, we see some quick tips on how to use the application:

![react app basic commands](https://content.codecademy.com/programs/react/creating-a-react-app/npm_react_commands.png)
____________________________________________________________________

## React App Structure

Our file structure should look like this

```
myfirstreactapp
├── node_modules
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   ├── serviceWorker.js
│   └── setupTests.js
├── .gititgnore
├── package.json
├── package-lock.json
└── README.md
```
create-react-app has taken care of setting up the main structure of the application as well as a couple of developer settings. Most of what you see will not be visible to the visitor of your web app. React uses a tool called webpack which transforms the directories and files here into static assets. Visitors to your site are served those static assets.

Don’t worry if you don’t understand too much about webpack for now. One of the benefits of using create-react-app to set up our React application is that we’re able to bypass any sort of manual configuration for webpack. If you’re interested in delving deeper into it on your own, you can find a [high-level overview of webpack’s core concepts here](https://webpack.js.org/concepts/).

### .gitignore

This is the standard file used by the source control tool git to determine which files and directories to ignore when committing code. While this file exists, create-react-app did not create a git repo within this folder. If you take a look at the file, it has taken care of ignoring a number of items (even .DS_Store for Mac users):

![ignored files in gitignore](https://content.codecademy.com/programs/react/creating-a-react-app/react_gitignore.png)

### package.json

![code within package.json](https://content.codecademy.com/courses/React/react_setup-037-package-json.png)

This file outlines all the settings for the React app

- `name` is the name of your app

- `version` is the current version

- `"private": true` is a failsafe setting to avoid accidentally publishing your app as a public package within the npm ecosystem.

- `dependencies` contains all the required Node modules and versions required for the application. In the picture above, you’ll see six dependencies. The first three, as you may have guessed, are for the purpose of testing. The next two dependencies allow us to use `react` and `react-dom` in our JavaScript. Finally, `react-scripts` provides a useful set of development scripts for working with React. In the screenshot above, the `react` version specified is `^16.13.1`. This means that npm will install the most recent major version matching 16.x.x. In contrast, you may also see something like `~1.2.3` in package.json, which will only install the most recent minor version matching 1.2.x.

- `scripts` specifies aliases that you can use to access some of the react-scripts commands in a more efficient manner. For example, running `npm test` in your command line will run `react-scripts test --env=jsdom` behind the scenes.

- You will also see two more attributes, `eslintConfig` and `browserslist`. Both of these are Node modules having their own set of values. `browserslist` provides information about browser compatibility of the app, while `eslintConfig` takes care of the [code linting](https://stackoverflow.com/questions/8503559/what-is-linting).

### node_modules

This directory contains dependencies and sub-dependencies of packages used by the current React app, as specified by **package.json**. If you take a look, you may be surprised by how many there are.

Running `ls -1 | wc -l` within the `node_modules/` directory will yield more than 800 subfolders. This folder is automatically added to the .gitignore for good reason! Don’t worry, even with all these dependencies, the basic app will only be around 50 KB after being [minified](https://techterms.com/definition/minification) and compressed for production.

### package-lock.json

This file contains the exact dependency tree installed in **node_modules/**. This provides a way for teams working on private apps to ensure that they have the same version of dependencies and sub-dependencies. It also contains a history of changes to package.json, so you can quickly look back at dependency changes.

### public

This directory contains assets that will be served directly without additional processing by webpack. index.html provides the entry point for the web app. You will also see a favicon (header icon) and a manifest.json.

The manifest file configures how your web app will behave if it is added to an Android user’s home screen (Android users can “shortcut” web apps and load them directly from the Android UI). You can read more about it [here](https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/).

### src 

This contains the JavaScript that will be processed by webpack and is the heart of the React app. Browsing this folder, you see the main App JavaScript component (App.js), its associated styles (App.css), and test suite (App.test.js). index.js and its styles (index.css) provide an entry into the App and also kick off the registerServiceWorker.js. This service worker takes care of caching and updating files for the end-user. It allows for offline capability and faster page loads after the initial visit. More of this methodology is available [here](https://developers.google.com/web/fundamentals/primers/service-workers).

As your React app grows, it is common to add a components/ directory to organize components and component-related files and a views/ directory to organize React views and view-related files.

## Starting the React App Development Server

As was stated in the success message when you ran `create-react-app`, you just need to run npm start in your app directory to begin serving the development server. It should auto-open a tab in your browser that points to `http://localhost:3000/` (if not, manually visit that address). You will find yourself looking at a page resembling the following image:

![landing page for create-react-app](https://content.codecademy.com/courses/React/react_setup-038-default-react-app.png)

As stated, any changes to the source code will live-update here. Let’s see that in action.

Leave the current terminal tab running (it’s busy serving the React app) and open `src/App.js` in your favorite text editor. You’ll see what looks like a mashup of JavaScript and HTML. This is *JSX*, which is how React adds XML syntax to JavaScript. It provides an intuitive way to build React components and is compiled to JavaScript at runtime. We’ll delve deeper into this in other content, but for now, let’s make a simple edit and see the update in the browser.

Change the main paragraph text to read `Hello Codecademy!` in App.js and save the file.

If you left the terminal running, you should be able to switch over to your browser and see the update.

Congratulations! You’re now up and running with React. You can now begin adding functionality for your application.

If you’d like to learn more about create-react-app, start with the [documentation on the create-react-app website](https://create-react-app.dev/docs/getting-started).
____________________________________________________________________

# React Developer Tools

We can use the Chrome extension "React Developer Tools" to allow us to inspect React components, view their properties, and interact with them while looking at the application in Google Chrome.

With the extension installed, when you start your React App (`npm start`) and visit the site in Chrome, the React Developer Tools(RDT) extension icon in the Chrome menu bar should change from inactive (grey/white) to active(orange/white) - this indicates that the site you are browsing is a React App in development build.

When a page is using the production build of React, the icon will have a black background with a blue icon.

To open the RDT, first open Chrome DevTools (View > Developer > Developer Tools). On the same banner as Elements, Sources, Console, etc., there will be two new React Tabs *Components* and *Profiler*.

These two tabs will only appear on sites using React (if they're not visible, click on the arrow to expand the tabs selection).

If we click on the components tab

![components tab of React Dev Tools](https://content.codecademy.com/programs/react/react-developer-tools/react-dev-tools-open.png)

Right now, all we can see is `App` itself. But we want to see the contents of `App` as well. In the above image, you’ll see that the cursor is pointing to a gear icon. Click the gear icon to open up the settings, and then click on the Components tab in the pop up window.

By default, there is a filter that is causing the host (DOM) nodes to be hidden. Delete this filter for now and then exit out of the settings window - you can always go back into the settings apply your preferred filters later.

Now, you will see a tree of `App`'s contents. As you hover over the elements on the left, they are highlighted in the rendered view, similar to Chrome DevTools. If you click on the elements in the left side of the window, their properties are exposed on the right side. (If your Chrome DevTools appear vertically on the left/right side of the window, `App` and its contents will appear on top, and their properties will be exposed underneath).

![RDT content tree](https://content.codecademy.com/programs/react/react-developer-tools/react-dev-tools-content-tree.png)

You can also use the search box to locate elements by name:

![RDT search](https://content.codecademy.com/programs/react/react-developer-tools/react-dev-tools-search.png)

With RDT and the console, it is possible to modify rendered React components. This will allow you to experiment with changing component values, calling methods, and testing interaction between components.

You can access and update a component's `state` and `props` inside the Components tab. Click and edit the `props` and `state` from the right side. For `state` to show up, you'll first need to initialize the component with some state from inside your files.

![RDT edit props and state](https://content.codecademy.com/programs/react/react-developer-tools/react-dev-tools-edit-props-state.png)

It also works with React Hooks

![RDT with react hooks](https://content.codecademy.com/programs/react/react-developer-tools/react-dev-tools-edit-hooks.png)

You can also do this by selecting the component, switching over to the console view, and accessing the component using `$r`. By logging `$r`, you could see that this was indeed the component selected.

![RDT console](https://content.codecademy.com/programs/react/react-developer-tools/react-dev-tools-console.png)

For more details and practice on how to use the tools, check out this [interactive tutorial](https://react-devtools-tutorial.now.sh/).
____________________________________________________________________

# Components Interaction

React apps are made out of components, but what makes React special isn’t components themselves. What makes React special is the ways in which components *interact*.

## A Component in a Render Function

Previously we have covered `.render()` methods that return JSX elements, like below:

```
class Example extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
```
Render methods can also return another kind of JSX: *component instances*

```
class OMG extends React.Component {
  render() {
    return <h1>Whooaa!</h1>;
  }
}
 
class Crazy extends React.Component {
  render() {
    return <OMG />;
  }
}
```
The `OMG` component renders an `h1` element with the text "Whooaa!". 

When `Crazy` renders, it gets the return value of `<OMG />` and renders that to the screen.
____________________________________________________________________

## Apply a Component in a Render Function

Previously, we used `ReactDOM.render()` to render a component.

When a component renders another component, what happens is very similar to what happens when we use `ReactDOM.render()`
____________________________________________________________________

## Require A File (`import` A File)

In order for one module (read: file) to access another module's information - like its variables, functions, etc. - we need to import it.

For example, if we have two files **ProfilePage.js** and **NavBar.js** and we want to render a `<NavBar />` component in **ProfilePage.js** then we need to include

```import { NavBar } from './NavBar.js';```

We've also used `import` before but not like this. We know how to import React to our JS files

```import React from 'react';```

The first importance difference between these two examples is the curly braces around `NavBar` - we'll cover that further down the line.

The second important difference involves the contents of the string at the end of the statement - `'react'` vs `'./NavBar.js'`

When we begin the string with a dot `.` or a slash `/`, `import` treats the string as a *filepath*. If your filepath does not have a file extension, (e.g. `./Navbar`) then the `.js` is assumed.
____________________________________________________________________

## `export`

In the previous example, we *imported* NavBar.js into ProfilePage.js. In order to do that we also need to include an *export* statement in **NavBar.js**.

There are a few different ways to use `export`. In this example we will be using a style called "named exports".

When we create an export statement we use the `export` keyword immediately before something that we want to export. That something can be any top-level `var`, `let`, `const`, `function` or `class`.

```
// Manifestos.js:
 
export const faveManifestos = {
  futurist: 'http://www.artype.de/Sammlung/pdf/russolo_noise.pdf',
  agile: 'https://agilemanifesto.org/iso/en/manifesto.html',
  cyborg:   'http://faculty.georgetown.edu/irvinem/theory/Haraway-CyborgManifesto-1.pdf'
};
```
We can also export multiple things from the same file

```
export const faveManifestos = {
  futurist: 'http://www.artype.de/Sammlung/pdf/russolo_noise.pdf',
  agile:  'https://agilemanifesto.org/iso/en/manifesto.html',
  cyborg:   'http://faculty.georgetown.edu/irvinem/theory/Haraway-CyborgManifesto-1.pdf'
};
 
export const alsoRan = 'TimeCube';
```
Then, in a different file we can `import` the things that we `export`ed.

```
// App.js:
 
// Import faveManifestos and alsoRan from ./Manifestos.js:
import { faveManifestos, alsoRan } from './Manifestos';
 
// Use faveManifestos:
console.log(`A Cyborg Manifesto:  ${faveManifestos.cyborg}`); 
```

As stated before, this is known as "named exports". When we use named exports we always need to wrap the *imported* names in curly braces, such as:

```
import { faveManifestos, alsoRan } from './Manifestos';`
```
____________________________________________________________________

# this.props

We know that components can interact with other components, such as rendering another component.

Components can also *pass information* to another component.

Information that gets passed from one component to another are known as *props*, which is short for "properties".

One possible reason for this naming is that props are essentially JavaScript objects, and JS objects contain properties. Furthermore, when we pass props from a component to a child component, the props are sent as an object containing the "properties" of the component.
____________________________________________________________________

## Access a Component's props

Every component has `props`. A component's `props` is an object that holds information about that component.

To see a component's `props` object, you use the expression `this.props`. Here's an example of `this.props` being used inside of a render method:

```
render() {
  console.log("Props object comin' up!");
 
  console.log(this.props);
 
  console.log("That was my props object!");
 
  return <h1>Hello world</h1>;
}
```
____________________________________________________________________

## Passing `props` to a Component

You can pass information to a React component. How? By giving that component an attribute.

```<MyComponent foo="bar" />```

Let’s say that you want to pass a component the message, `"This is some top secret info."`. Here’s how you could do it:

```<Example message="This is some top secret info." />```

In order to pass information to a component we need a *name* for the information that we want to pass.

In the example above, we used the name `message` - but we can use any name that we want.

If we want to pass information that *is not* a string, then we need to wrap that information in curly braces. Here's how you would pass an array:

```
<Example message="This is some top secret info." />
```

We can also pass several pieces of information to a Component, notice that the values that *are not* strings are wrapped in curly braces.

```
<Greeting name="Frarthur" town="Flundon" age={2} haunted={false} />
```
____________________________________________________________________

## Render a Component's props

Often, you will want a component to *display* the information that you pass to it.

Here's how to make a component display passed-in information:

1. Find the *component class* that is going to receive that information
2. Include `this.props.name-of-information` in the component class's *render* method's `return` statement.

For example:

```
class Greeting extends React.Component {
  render() {
    return <h1>Hi there, {this.props.firstName}!</h1>;
  }
}

ReactDOM.render(
  <Greeting firstName='Groberta' />, 
  document.getElementById('app')
);
```
____________________________________________________________________

## Pass props From Component to Component

We learned how to pass a `prop` to a component 

```<Greeting firstName="Esmerelda" />```

And also how to access and display a pass-in `prop`

```
render() {
  return <h1>{this.props.firstName}</h1>;
}
```

But the most common use of `props` is to pass information from one component to a different component.

> `props` is the name of the object that stores passed-in information. `this.props` refers to that storage object. At the same time, each piece of passed-in information is called a prop. This means that `props` could refer to two pieces of passed-in information, or it could refer to the object that stores those pieces of information.

Take a look at how this is accomplished with the two examples below:

```
//Greeting.js

import React from 'react';

export class Greeting extends React.Component {
  render() {
    return <h1>Hi there, {this.props.name}!</h1>; /* When an instance of Greeting is rendered, it will pass in the prop with the name, "name", from *this* instance of the component. */
  }
}

```

```
// App.js

import React from 'react';
import ReactDOM from 'react-dom';
import {Greeting} from './Greeting'; /* Here we import the `Greeting` class from the `Greeting.js` module */

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>
          Hullo and, "Welcome to The Newzz," "On Line!"
        </h1>
        <Greeting name="Steve"/> /* We create an instance of the component "Greeting" and pass it a prop with the name, "name", with the value of "Steve" */
        <article>
          Latest newzz:  where is my phone?
        </article>
      </div>
    );
  }
}

ReactDOM.render(
  <App />, 
  document.getElementById('app')
);
```
____________________________________________________________________

## Render Different UI Based on props

We can do more than just display `props` - we can also use them to make decisions. Take the following code as an example:

```
export class Welcome extends React.Component {
  render() {
    if (this.props.name === 'Wolfgang Amadeus Mozart') {
      return (
      	<h2>
      	  hello sir it is truly great to meet you here on the web
      	</h2>
      );
    } else {
      return (
      	<h2>
      	  WELCOME "2" MY WEB SITE BABYYY!!!!!
      	</h2>
      );
    }
  }
}
```

The `Welcome` component expects to have a `name` prop passed to it and *if* the user is Mozart it will display one message and if not it will display something else.

Note that the value of the `name` prop is *not* displayed in either case, rather it is used to make a decision on what will be displayed.
____________________________________________________________________

## Put an Event Handler in a Component Class

You can, and often will, pass functions as `props`. It is especially common to pass *event handler* functions.

However, we have to *define* an event handler before we can pass one anywhere. How do we do that? By defining an event handler as a method on the component class, just like the *render* method.

```
class Talker extends React.Component {
  talk () {
	// function body
}
  
  render() {
    // return render body
  }
}
```
____________________________________________________________________

## Pass an Event Handler as a prop

You can pass a method/function the exact same way that you pass any other information.

```
// include proper imports here

class Talker extends React.Component {
  talk() {
    let speech = '';
    for (let i = 0; i < 10000; i++) {
      speech += 'blah ';
    }
    alert(speech);
  }
  
  render() {
    return <Button talk={this.talk}/>;
  }
}
```
____________________________________________________________________

## Receive an Event Handler as a Prop

Cool, so we know how to *pass* an event handler into another component but how do get the receiving component to *receive* it?

The same way that you attach an event handler to any JSX element - by giving the element a special attribute, like `onClick` or `onHover`, whose *value* should be the event handler you want to attach.

```
export class Button extends React.Component {
  render() {
    return (
      <button onClick={this.props.talk}>
        Click me!
      </button>
    );
  }
}
```
____________________________________________________________________

## handleEvent, onEvent, and this.props.onEvent

Let's talk about naming conventions.

When we pass an event handler as a prop there are two names that we have to choose - both naming choices occur in the parent component class - that is, in the component class that defines the event handler and passes it.

The first name that you have to choose is the name of the event handler itself. In the previous example, we chose the name `talk`.

The second name that you have to choose is the name of the prop that you will use to pass the event handler - this is the same thing as your attribute name.

In the previous section, our example was 

```return <Button talk={this.talk} />;```

However, this example does not follow typical naming conventions.

When it comes to the name of the event handler function, we want to think about what *type of event* you are listening for. In the previous example, the event type was "click", in this case we should name our *event handler* `handleClick`. If we were listening for a "keyPress" event, then we should name the event handler `handleKeyPress`.

For the name of the prop, it should be the word `on` plus the event type. So, if we are listening for a "click" event, then we name the prop `onClick`. If we are listening for a "keyPress" event, we name the prop `onKeyPress`.

```
class MyClass extends React.Component {
  handleHover() {
    alert('I am an event handler.');
    alert('I will listen for a "hover" event.');
  }
 
  render() {
    return <Child onHover={this.handleHover} />;
  }
}
```
One major source of confusion is the fact that names like `onClick` have special meaning, but only if they’re used on HTML-like elements.

Look at Button.js below. When you give a `<button></button>` an attribute named `onClick`, then the name `onClick` has special meaning. As you’ve learned, this special `onClick` attribute creates an event listener, listening for clicks on the `<button></button>`:

```
// Button.js
 
// The attribute name onClick
// creates an event listner:
<button onClick={this.props.onClick}>
  Click me!
</button>
```

Now look at Talker.js below. Here, when you give `<Button />` an attribute named `onClick`, then the name `onClick` doesn’t do anything special. The name `onClick` does not create an event listener when used on `<Button />` - it’s just an arbitrary attribute name:

```
// Talker.js
 
// The attribute name onClick
// is just a normal attribute name:
<Button onClick={this.handleClick} />
```

The reason for this is that `<Button />` is not an HTML-like JSX element; it’s a *component instance*.

Names like `onClick` only create event listeners if they’re used on HTML-like JSX elements. Otherwise, they’re just ordinary prop names.
____________________________________________________________________

## this.props.children

Every component's `props` object has a property named `children`. 

`this.props.children` will return everything in between a component's opening and closing JSX tags.

So far, all of the components that we've used in our examples have been self-closing tags, such as `<MyComponentClass />` - but they dont have to be! We can write `<MyComponentClass> </MyComponentClass>` and it would still work.

`this.props.children` would then return everything between `<MyComponentClass>` and `</MyComponentClass>`

```
// Example 1
<BigButton>
  I am a child of BigButton.
</BigButton>
// this.props.children would equal "I am a child of BigButton."

// Example 2
<BigButton>
  <LilButton />
</BigButton>
// this.props.children would equal a `<LilButton />` component

// Example 3
<BigButton />
// this.props.children would equal undefined
```
When there are multiple children `this.props.children` returns an array of all the children. If there is only a single child then only a single value will be stored in the `children` property and it will *not* be in an array.
____________________________________________________________________

## defaultProps

What if a component is expecting to be passed a prop but no prop is passed to it?

In this case, the prop would be blank/undefined. It would be better if we could provide some kind of default value instead.

We can accomplish this by giving our component class a property named `defaultProps`

```
class Example extends React.Component {
  render() {
    return <h1>{this.props.text}</h1>;
  }
}

// Set defaultProps equal to an object: 
Example.defaultProps = { text: 'yo' }; 
```
The `defaultProps` property should be equal to an object. Inside the object, write properties for any default `props` that we want to set.

If an `<Example />` does not get passed any text, then it will display "yo".

If it *does* get passed some text, then it will display that passed-in text.
____________________________________________________________________

## Summary

- We can pass a prop by giving an *attribute* to a component instance

- We can access a passed-in prop via `this.props.prop-name`

- We can display a prop of a component by including that prop in the component instance.

- We can use a prop to make decisions about what to display; This logic must be *inside* of the `.render()` method.

- We can define an event handler method inside of the component class just like a `.render()` method

- We can pass an event handler as a prop

- How to receive a prop event handler and attach it to an event listener

- We should name event handlers and event handler attributes according to convention

- `this.props.children` returns all the children of a component. If there are multiple children, an array containing them all gets returned. If there is a single child then only that is returned *not* inside an array.

- We can provide `defaultProp` values using an object containing the default prop key-value pairs.
____________________________________________________________________

## `this.state`

*Dynamic information* is information that can change.

React components often need dynamic information in order to render. For example, imagine a component that displays the score of a team based game - like basketball.

The score will change over time, meaning that the score is *dynamic*.

There are two ways for a component to get dynamic information: `props` and `state`. 
____________________________________________________________________

## Setting Initial State

Unlike `props`, a component's `state` is *not* passed in from the outside. A component decides its own `state`.

To make a component have `state` we must give the component the `state` property. The property should be declared inside of a constructor method, like this:

```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'decent' };
  }
 
  render() {
    return <div></div>;
  }
}
 
<Example />
```
`this.state` should be equal to an object, like the example above. This object represents the initial "state" of any component instance - which will be explained more in a future section.

`constructor` and `super` are features of ES6 for creating instanced objects of a class. It is important to note that React components *always* have to call `super` in their constructors to be set up properly.

In the example above, our `Example` component has a default state which has a key-value pair of `{ mood: 'decent' }`. 
____________________________________________________________________

## Accessing a Component's `state`

To *read* a component's `state`, use the expression `this.state.name-of-property`.

```
class TodayImFeeling extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'decent' };
  }
 
  render() {
    return (
      <h1>
        I'm feeling {this.state.mood}!
      </h1>
    );
  }
}
```
The `render` function in the above example reads the property in its `state`.

Just like `this.props` you can use `this.state` from any property defined inside of a component class's body.
____________________________________________________________________

## Update `state` with `this.setState()`

We can also change a component's state by calling the function `this.setState()` which takes two arguments: an *object* that will update the component's state, and a callback function. However, you basically never need the callback function.

Let's say we have the following component:

```
class Example extends React.Component {
  constructor(props) {
  	super(props);
    this.state = {
      mood:   'great',
      hungry: false
    };
  }
```

And then we call the `this.setState()` function like so:

```this.setState({ hungry: true });```

After that, our `<Example />`'s state would be:

```
{
  mood:   'great',
  hungry: true
}
```

Notice that the `mood` part of the state remains unaffected.

That is because `this.setState()` takes an object and *merges* that object with the component's current state. If there are proeprties in the current state that are not part of the update object, then those properties remain how they are.
____________________________________________________________________

### Call `this.setState()` from Another Function

The most common way to call `this.setState()` is to call a custom function that *wraps* a `this.setState()` call. Take for example:

```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { weather: 'sunny' };
    this.makeSomeFog = this.makeSomeFog.bind(this);
  }
 
  makeSomeFog() {
    this.setState({
      weather: 'foggy'
    });
  }
}
```

We create a method named `makeSomeFog()` which contains a call to `this.setState()`. 

Now, you may have noticed this line:

```this.makeSomeFog = this.makeSomeFog.bind(this);```

This line is necessary because `makeSomeFog()`'s body contains the word `this` - wait... what?

Due to the way that event handlers are bound in JavaScript, `this.toggleMood()` loses its `this` when it is used on line 20 (on the line with the opening `button` tag).

Therefore, the expressions `this.state.mood` and `this.setState` on lines 12 and 13 (within the `toggleMood()` declaration) wont mean what they're supposed to - *unless* you have already bound the correct `this` to `this.toggleMood`.

That is why we must bind `this.toggleMood` to `this` on line 8 (in the `constructor` method).

For more of an in-depth explanation you can consult [the React documentation](https://facebook.github.io/react/docs/handling-events.html) - however, just know that in React, **whenever you define and event handler that uses `this` you need to add `this.methodName = this.methodName.bind(this)` to your constructor function.**

One last note: you **can not** call `this.setState()` from inside the render function - which will be explained in the following section.
____________________________________________________________________

## `this.setState()` Automatically Calls `render`

Any time that you call `this.setState()`, `render()` is **automatically** called as soon as the state has changed.

That is why you can not call `this.setState()` from inside of the `.render()` method!

Since `this.setState()` automatically calls `.render()`, if `render()` called `this.setState()` an infinite loop would be created.
____________________________________________________________________

## Summary

- A component has a `state` which has dynamically changing information
- When we set the initial state of a component we must include `super(argument)` inside of the `.constuctor()` method
	- "argument" is whatever the arguments being passed into the `.constructor()` method are
- A component's state is an object that contains key-value pairs which can be read with `this.state.name-of-state-property`.
- We can also change the properties within a component's state with `this.setState()`
	- If a `state` has multiple key-value pairs and we only change one or some of them, the remaining pairs will be left unchanged.
- We can change a component's state from another function (read: event handler)
	- When we do so, we need to *bind* the keyword `this` in the constructor method using the line `this.methodName = this.methodName.bind(this)`
- When we invoke `this.setState()` it automatically calls `.render()` and for this reason we cannot include `this.setState()` in our `.render()` method - otherwise we create an infinite loop.
____________________________________________________________________

# Stateless Components Inherit From Stateful Components

Let's learn a new *programming pattern*.

This pattern uses two React components: a *stateful* component and a *stateless* component. "Stateful" describes any component that has a `state` property, while "stateless" describes any component that does not.

In this pattern, a *stateful* component will pass its `state` down to a *stateless* component.
____________________________________________________________________

## Build a Stateless Component Class

```
import React from 'react';

export class Child extends React.Component {
  render() {
    return <h1>Hey, my name is {this.props.name}!</h1>;
  }
}
```

Here we have a component class `Child` that expects a `prop` named `name`. It has no default state and uses the `export` keyword so that we can import it to another module.
____________________________________________________________________

## Build a Stateful Component Class

```
import React from 'react';
import ReactDOM from 'react-dom';
import { Child } from './Child';

class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: 'Frarthur'};
  }

  render() {
    return <div><Child name={this.state.name}/></div>;
  }
}

ReactDOM.render(
  <Parent />,
  document.getElementById('app')
)
```

Here, we have a `Parent` component class and since it's supposed to be *stateful* - meaning that it has a set a default state - we need to include a constructor method.

Inside `.constructor()` we invoke `super` which calls `Parent`'s parent (`React.Component) constructor method.

Then, still inside `.constructor()` we set the default state using `this.state`.

In `.render()` we return a `<div>` with a `<Child />` component that has a prop named "name" which we pass the `state` information into.

Finally, we render the component to the screen.
____________________________________________________________________

## We update `state`, not `props`

We learned earlier that a component can change its state by calling `this.setState()` - so how does a component change it's props?

The answer is: it doesn't!

This is potentially confusing. `props` and `state` store dynamic information. Dynamic information can change, by definition. If a component can’t change its `props`, then what are `props` for?

**A React component should use `props` to store information that can be changed, but can only be changed by a *different* component.

A React component should use `state` to store information that the component itself can change.**
____________________________________________________________________

# Child Components Update Their Parents' State

How does a stateless, child component *update* the state of the parent component?

First, the *parent* component class must have a method that calls `this.setState()`. For example:

```
class ParentClass extends React.Component {
  constructor(props) {
    super(props);

    this.state = { totalClicks: 0 };
  }

  handleClick() {
    const total = this.state.totalClicks;

    // calling handleClick will 
    // result in a state change:
    this.setState(
      { totalClicks: total + 1 }
    );
  }
}
```

Next, the parent component must also bind the newly-defined method to the current instance of the component in it's constructor. This ensures that when we pass the method to the child component, it will still update the parent component. We do this by adding

`this.handleClick = this.handleClick.bind(this);` 

to the constructor method of the parent component.

Following that, we can then pass the method from the parent to the child

```
// this is inside of the parent component

render() {
    return (
      <ChildClass onClick={this.handleClick} />
    );
  }
```
Now that the child has received the passed-down event handler function, when a user clicks on the child component, the `.handleClick()` event will fire which will *update* the parent's state.
____________________________________________________________________

# Child Components Update Sibling Components

We just covered our first React programming pattern: a *stateful*, parent component passing down a `prop` to a *stateless*, child component.

Then we learned that the first pattern is actually part of a larger pattern: a stateful, parent component passing down an *event handler* to a stateless, child component. The child component then uses that *event handler* to update its parent's `state`.

Now, we'll expand that second lesson a bit more. A child component can update it's parent's state and then the parent passes that updated state to a *sibling* component.
____________________________________________________________________

## One Sibling to Display, Another to Change

Previously we learned that a component should only have one job.

So if we're going to use a child component to update it's sibling component then each individual component should have one job - e.g. one component should *display* the information and the other one should *change* the information.

```
render() {
    return (
      <div>
        <Child 
          onChange={this.changeName} />
        <Sibling name={this.state.name}/>
      </div>
    );
  }
```

In the example above we have a component, `<Child />` that has a prop `onChange` which holds our event handler function, `.changeName()`.

Then it's sibling component, `<Sibling />` has the prop `name` which gets updated when `<Child /> invokes `.changeName()`
____________________________________________________________________

## Displaying Information in a Sibling Component

Now that `<Sibling />` has the `name` prop being passed down, we can display it like so:

```
render() {
    const name = this.props.name;
    return (
      <div>
        <h1>Hey, my name is {name}!</h1>
        <h2>Don't you think {name} is the prettiest name ever?</h2>
        <h2>Sure am glad that my parents picked {name}!</h2>
      </div>
    );
  }
```

Here we store `this.props.name` in a variable `name` and use JavaScript injection to add it to our rendered JSX elements.
____________________________________________________________________

## Summary

- A *stateful* component class defines a function that calls `this.setState` (Parent)
- The stateful component passes that function down to a *stateless* component. (Parent)
- That *stateless* component class defines a function which calls the passed-down function, and that newly defined function takes an *event object* as an argument. (Child)
- The stateless component class uses this newly defined function as an event handler
- When an event is detected, the parent's state updates. (Child)
- The *stateful* component class passes down its state - this is distinct from the ability to *change* the state - to a different stateless component. (Parent)
- That stateless component class receives the state and displays it. (Sibling)
- An instance of a stateful component class is rendered. One stateless child component displays the `state` (e.g. Text that reads "Hi my name is {name}") and a different stateless child component displays a way to *change* the state (e.g. A drop down menu that has different name options).
____________________________________________________________________

# Authentication and OAuth

Authentication is the process used by applications to determine and confirm identities of users. It ensures that the correct content is shown to users. More importantly, it ensures that incorrect content is secured and unavailable to unauthorized users.

In this article, we’ll discuss a few of the common design patterns for these interactions. You’ll need to have some basic understanding of HTTP requests, since these methods all use HTTP requests to exchange information.

## Password Authentication 

The most common implementation of authentication requires a user to input their username or email and a password. The application’s server then checks the supplied credentials to determine if the user exists and if the supplied password is correct. If the credentials are correct, the user is logged in and able to use the application as that user.

Typically, upon a successful login, the application will respond with an authentication token (or auth token) for the client to use for additional HTTP requests. This token is then stored on the user’s computer, preventing the need for users to continuously log in.

This token generally expires after a certain amount of time, ensuring the correct user is using the application over time as well.

## API Keys

While it is common to think of authentication as the interaction between a human user and an application, sometimes the user is another application.

Many apps expose interfaces to their information in the form of an API (application program interface). For example, the [Spotify API](https://developer.spotify.com/web-api/) provides endpoints for almost all of its functionality. This allows applications to fetch data from the Spotify music catalog and manage user’s playlists and saved music.

Since these external requests could overwhelm a service and also access user information, they need to be secured using authentication.

The most basic pattern for API access from another application is using an API key.

Public APIs usually provide a developer portal where you can register your application and generate a corresponding API key. This key is then unique to your application. When your application makes a request, this key is sent along with it. The API can then verify that your application is allowed access and provide the correct response based on the permission level of your application.

The API can track what type and frequency of requests each application is making. This data can be used to [throttle requests](https://en.wikipedia.org/wiki/Throttling_process_(computing)) from a specific application to a pre-defined level of service. This prevents applications from spamming an endpoint or abusing user data, since the API can easily block that application’s API key and prevent further malicious use of the API by that application.

## OAuth

For many applications, a generic developer-level API key is not sufficient. As mentioned earlier, APIs sometimes have the ability to provide access to user-level data. However, most services only provide this private data if the user enables it.

For example, Facebook doesn’t want Tinder to access all of their users’ data, just the users who have opted in to allowing the sharing of data to better help them find a match in their area.

A basic approach to this problem might be to have the user provide their login credentials to the intermediary application, but this is not very secure and would give full access to the requesting application, when the requesting application might only need a very limited set of privileges to function.

OAuth defines a more elegant approach to this problem. It was developed in November 2006 by lead Twitter developer Blaine Cook and version 1.0 was published in April 2010.

OAuth is an open standard and is commonly used to grant permission for applications to access user information without forcing users to give away their passwords.

An open standard is a publicly available definition of how some functionality should work. However, the standard does not actually build out that functionality.

As a result, each API is required to implement their own version of OAuth and therefore may have a slightly different implementation or flow. However, they’re all based around the same OAuth specification.

This can make using a new OAuth API a little more frustrating. However, with time you will begin noticing the similarities between API authentication flows and be able to use them in your applications with increasing ease. Below is a summary of the standard OAuth flow.

### Generic OAuth Flow

Many applications implementing OAuth will first ask the user to select which service they would like to use for credentials:

![authenticationLogin](https://content.codecademy.com/programs/react/authentication/authentication_login.png)

After selecting the service, the user will be redirected to the service to login. This login confirms the user’s identity and typically provides the user with a list of permissions the originating application is attempting to gain on the user’s account.

If the user confirms they want to allow this access, they will be redirected back to the original site, along with an access token. This access token is then saved by the originating application.

Like a developer API key, this access token will be included on requests by the application to prove that the user has granted access and enable access to the appropriate content for that user. When a user returns to the application, the token will be retrieved and they will not have to re-authenticate.

### OAuth 2

Since OAuth evolved out of Twitter, there were important use cases not originally considered as part of the specification. Eventually, this led to the creation of a new version of the specification, called OAuth 2.

Among other improvements, OAuth 2 allows for different authentication flows depending on the specific application requesting access and the level of access being requested.

OAuth 2 is still an open standard, so each API will have its own flow based on its particular implementation. Below, we’ll discuss a few of the common OAuth 2 flows and how they are used.

### Client Credentials Grant

Sometimes an application will not need access to user information but may implement the added security and consistency of the OAuth 2 specification. This type of grant is used to access application-level data (similar to the developer API key above) and the end user does not participate in this flow.

Instead of an API key, a client ID and a client secret (strings provided to the application when it was authorized to use the API) are exchanged for an access token (and sometimes a refresh token). We will discuss refresh tokens in more depth later.

This flow is similar to our first example, where an email and password were exchanged for an authentication token.

It is essential to ensure the client secret does not become public information, just like a password. As a result, developers should be careful not to accidentally commit this information to a public git repository. Additionally, to ensure integrity of the secret key, it should not be exposed on the client-side and all requests containing it should be sent server-side.

Similar to the previously-mentioned keys, the returned access token is included on requests to identify the client making the requests and is subject to API restrictions.

This access token is often short-lived, expiring frequently. Upon expiration, a new access token can be obtained by re-sending the client credentials or, preferably, a refresh token.

Refresh tokens are an important feature of the OAuth 2 updates, encouraging access tokens to expire often and, as a result, be continuously changed (in the original OAuth specification, access tokens could last for time periods in the range of years). When a refresh token is used to generate a new access token, it typically expires any previous access tokens.

### Authorization Code Grant

This flow is one of the most common implementations of OAuth and will look familiar if you’ve ever signed into a web application with Google or Facebook. It is similar to the OAuth flow described earlier with an added step linking the requesting application to the authentication.

A user is redirected to the authenticating site, verifies the application requesting access and permissions, and is redirected back to the referring site with an authorization code.

The requesting application then takes this code and submits it to the authenticating API, along with the application’s client ID and client secret to receive an access token and a refresh token. This access token and refresh token are then used in the same manner as the previous flow.

To avoid exposing the client ID and secret, this step of the flow should be done on the server side of the requesting application.

Since tokens are tied both to users and requesting applications, the API has a great deal of control over limiting access based on user behavior, application behavior, or both.

### Implicit Grant

The previous two methods cause the client secret key to be exposed, so they need to be handled server-side. Some applications may need to access an OAuth API but don’t have the necessary server-side capabilities to keep this information secure.

The Implicit Grant OAuth flow was designed for this very use case. This flow prompts the user through similar authorization steps as the Authorization Code flow, but does not involve the exchange of the client secret.

The result of this interaction is an access token, and typically no refresh token. The access token is then used by the application to make additional requests to the service, but is not sent to the server side of the requesting application.

This flow allows applications to use OAuth APIs without fear of potentially exposing long-term access to a user or application’s information.

## Conclusion

OAuth provides powerful access to a diverse set of sites and information. By using it correctly, you can reduce sign-up friction and enrich user experience in your applications.
