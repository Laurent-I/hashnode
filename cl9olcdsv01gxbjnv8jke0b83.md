---
title: "Tips for React Beginners"
seoTitle: "Tips and tricks for junior react developers"
seoDescription: "Get to know some cool tricks you can use as a ReactJS junior developer and write more and better readable code."
datePublished: Tue Oct 25 2022 19:18:44 GMT+0000 (Coordinated Universal Time)
cuid: cl9olcdsv01gxbjnv8jke0b83
slug: tips-for-react-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1666724523583/4mlRQDfbC.jpg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1666724922296/35zAy5BVZ.jpg
tags: web-development, reactjs, beginners

---




# INTRODUCTION

When I first started using React.js, It was pretty hard for me and I reached at a point where I quit it because it was annoying for me. 
But I came to realize that it was actually pretty simple that problem was that I kept mixing up the code and using poor code structure which made it hard to debug the code which brought so much frustration.
So here are some tips for react beginners which can help you learn react easily 

![1xlblr.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1665907177618/bsPXqBqOs.jpg align="left")


### 1. SEPARATION OF CODE

This must be among the most common best practices among react developers. The reason is pretty simple and straightforward. 
Since react is based on components, separating the code makes the components more understandable and the code becomes more readable plus it makes it easier to debug your code


![debug.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1665907733841/lmJhBd1Bj.jpg align="left")

Another benefit of separating your is that it makes it more reusable. Since we are developers we hating repeating the same thing over and over again (*at least for me that is how it is* ). We like DRY things more the WET things. (*get it!*). It is always better to have one component per file but not a must in order to make it easier to debug easily.

### 2. NAMING 
Naming components is among the easiest things which makes it easy to ignore (atleast that was how it was for me). When naming react components it is always a good idea to start the component name with a **capital letter **because a tag which starts with a **small letter** is treated as an HTML Tag by the complier. This a common error most junior react developers face. (or at least for me). 
If were you need to know more about naming components in depth and fall in love with the names of your components I would advise reading [React components naming conventions](https://medium.com/@wittydeveloper/react-components-naming-convention-%EF%B8%8F-b50303551505). But I would emphasize on writing clear and understandable names which start with Capital letters (Pascal Case) for the sake of being clear.


### 3. DESTRUCTURING PROPS
Before we begin if don't what destructuring is: This not a react feature but simply a JavaScript feature and was introduced in ES6. It’s a JavaScript feature that allows us to extract multiple pieces of data from an array or object and assign them to their own variables.
Example:
This is a real object which we had to access each property individually

```
const person = {
  firstName: "Irakarama",
  lastName: "Laurent",
  city: "Kigali"
}
console.log(person.firstName) // Irakarama
console.log(person.lastName) // Laurent
console.log(person.city) // Kigali
```
Destructuring lets us simply the code like this:

```
const { firstName, lastName, city } = person;
```
And now we don't need the *person.* prefix to access properties of an object

```
console.log(firstName) // Irakarama
console.log(lastName) // Laurent
console.log(city) // Kigali
```
Destructuring props really shines in react because it makes writing props easy and makes them more readable.Lets take an example of a todo app I am working on. I want to pass some data through props to the <Todos/> component.


```
props  = {
{
    id: "e1",
    title: "Learn React",
    date: new Date(2020, 7, 14),
  },
  { id: "e2", title: "Study for test", date: new Date(2021, 2, 12) }
}
```
This makes pretty ugly JSX code and makes us sometimes pass down more data than we actually need.

```
const TodoList = (props) => {
  return (
    <ul>
        <TodoItem
          id={props.id}
          key={props.id}
          title={props.title}
          date={props.date}
        />
    </ul>
  );
};

export default TodoList;
```

Destructuring can help drop all the props. and make the code more readable

```
const TodoList = ({id, title, date}) => {
  return (
    <ul>
        <TodoItem
          id={id}
          key={id}
          title={title}
          date={date}
        />
    </ul>
  );
};

export default TodoList;
```
Sometimes it necessary to pass down the data down in props if we need access to all of the data at the same time for rendering or something else.

### 4. CLEANING UP THE DOM
This is not really a must but if we want good semantic good it is advised to clean up the DOM. In react it easy to populate the DOM with uneccessary divs which leads to a situation known as the **"The Div Soup" **. The div soup is when front-end web developers (you know the ones that write the HTML, CSS, and Javascript?) wrap every HTML element they possibly can in enough <div> elements to make your eyes bleed. In react it is to wrap a <div> around all the elements in the return statement. Note: It doesn't have to be a div; it can be any wrapper component or tag.

![div-soup-vs-custom-elements.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666703656118/Gf3YNoGuX.png align="left")

We can solve this bad practice by Using **React.Fragment** or **Wrapper** Components like this :
```
const Wrapper = (props) => {
  return props.children;
};
export default Wrapper;
```
This will prevent from rendering to many and unnecessary divs or other tags.

### CONCLUSION
At the of the day it is really up to you whether to use these tricks but I strongly recommend using them because they definitely helped me when I was started learning react and I they were super helpful. Please do feel free to criticise or suggest anything down below in the comments.
